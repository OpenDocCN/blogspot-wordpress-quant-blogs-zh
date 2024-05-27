<!--yml

category: 未分类

日期：2024 年 05 月 12 日 19:33:41

-->

# CPU 缓存大小 | 编码市场

> 来源：[`etrading.wordpress.com/2012/09/21/cpu-cache-size/#0001-01-01`](https://etrading.wordpress.com/2012/09/21/cpu-cache-size/#0001-01-01)

## CPU 缓存大小

### 2012 年 9 月 21 日

这是我 2009 年写的一些代码，用于确定 Windows 主机上的 L1 和 L2 缓存大小。它通过填充一个内存区域，使其中的随机指针指向同一区域，来运行。随机化打败了 CPU 基于步幅的尝试来预测下一个缓存访问。内存区域的大小按二的幂递增，并记录时间。这些时间应该显示出内存区域大小耗尽 L1 和 L2 缓存的时候。这段代码说明了为什么控制内存局部性对于编写友好的缓存代码是如此重要。

```
#include <iostream>
#include <cmath>
#include <windows.h>

typedef unsigned __int64 ui64;
typedef int* iptr;

const int _1K = 1 << 10;
const int _16M = 1 << 24;

iptr aray[_16M/sizeof(iptr)];

inline ui64 RDTSC( ) {
   __asm {
      XOR eax, eax        ; Input 0 for CPUID, faster than mv
      CPUID            ; CPUID flushes pipelined instructions
      RDTSC            ; Get RDTSC counter in edx:eax matching VC calling conventions
   }
}

int main( int argc, char** argv)
{
    // Ensure we're running on only one core
    DWORD proc_affinity_mask = 0;
    DWORD sys_affinity_mask = 0;
    HANDLE proc = GetCurrentProcess( );
    GetProcessAffinityMask( proc, &proc_affinity_mask, &sys_affinity_mask);
    std::cout << "proc_affinity_mask=" << proc_affinity_mask << ", sys_affinity_mask=" << sys_affinity_mask << std::endl;
    if ( proc_affinity_mask > 1) {
        if ( proc_affinity_mask & 2)
            proc_affinity_mask = 2;
        else
            proc_affinity_mask = 1;
        SetProcessAffinityMask( proc, proc_affinity_mask);
    }

    // avoid interrupts 
    SetPriorityClass( proc, REALTIME_PRIORITY_CLASS);

    // stepping up thru the candidate cache sizes
    for ( int bytes = _1K; bytes <= _16M; bytes *= 2) {

        // populate the array with ptrs back into the array
        int    slots = bytes/sizeof(iptr);
        int    slot = 0;
        iptr    start_addr = reinterpret_cast<iptr>( &aray[0]);
        iptr    end_addr = start_addr + slots;
        iptr    rand_addr = 0;
        iptr    addr = 0;

        std::cout << "slots=" << std::dec << slots << ", start_addr=" 
            << std::hex << start_addr << ", end_addr=" << end_addr << std::endl;

        // clear memory first so we can spot unpopulated slots below
        for ( addr = start_addr; addr < end_addr; addr++)
            *addr = 0;

        for ( addr = start_addr; addr < end_addr; addr++) {
            // pick a random slot in the array
            slot = int( float( slots) * float( rand( ))/ float( RAND_MAX));
            rand_addr = start_addr + ( slot == slots ? 0 : slot);

            // look for the next empty slot - nb we may need to wrap around
            while ( *rand_addr) {
                rand_addr++;
                if ( rand_addr >= end_addr)
                    rand_addr = start_addr;
            }
            *rand_addr = reinterpret_cast<int>( addr);
        }

        // sanity check
        for ( addr = start_addr; addr < end_addr; addr++) {
            if ( !*addr)
                std::cout << "empty slot at " << std::hex << addr << std::endl;
        }

        // now we're ready to ptr chase thru the array
        int accesses = int( 1e6);
        addr = aray[0];
        ui64 start_time = RDTSC( );
        for ( int i = 0; i < accesses; i++)
            addr = reinterpret_cast<iptr>( *addr);
        ui64 end_time = RDTSC( );

        ui64 cycles = end_time - start_time;
        float rw_cost = float( cycles)/float( accesses);
        std::cout << "size=" << std::dec << bytes << ", cycles=" 
                    << cycles << ", cost=" << rw_cost << std::endl;
    }

    return 0;
}

```
