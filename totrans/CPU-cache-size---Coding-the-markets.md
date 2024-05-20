<!--yml
category: 未分类
date: 2024-05-12 19:33:41
-->

# CPU cache size | Coding the markets

> 来源：[https://etrading.wordpress.com/2012/09/21/cpu-cache-size/#0001-01-01](https://etrading.wordpress.com/2012/09/21/cpu-cache-size/#0001-01-01)

## CPU cache size

### September 21, 2012

Here’s some code I wrote back in 2009 to figure out the L1 and L2 cache sizes on a Windows host. It works by populating an area of memory with randomized pointers that point back into that same area. The randomization defeats stride based attempts by CPUs to predict the next cache access. The size of the memory region is stepped up in powers of two, and timings taken. The timings should show when the region size exhausts the L1 and L2 caches. This code illustrates why control of memory locality is so important in writing cache friendly code.

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