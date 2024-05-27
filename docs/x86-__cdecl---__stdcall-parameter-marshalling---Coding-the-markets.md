<!--yml

类别: 未分类

日期: 2024 年 5 月 12 日 19:32:37

-->

# x86 __cdecl & __stdcall 参数传递 | 编码市场

> 来源：[`etrading.wordpress.com/2014/07/23/x86-__cdecl-__stdcall-parameter-marshalling/#0001-01-01`](https://etrading.wordpress.com/2014/07/23/x86-__cdecl-__stdcall-parameter-marshalling/#0001-01-01)

## x86 __cdecl & __stdcall 参数传递

### 2014 年 7 月 23 日

假设你有一个第三方的 Win32 DLL，但没有访问源代码的权限。该 DLL 导出一个众所周知的 init 函数，该函数回调到您的代码中以注册更多函数。因此，您可以调用 Win32 的 [LoadLibrary](http://msdn.microsoft.com/en-gb/library/windows/desktop/ms684175%28v=vs.85%29.aspx) 来加载 DLL，您可以使用 [GetProcAddress](http://msdn.microsoft.com/en-gb/library/windows/desktop/ms683212%28v=vs.85%29.aspx) 获取 init 函数的指针。您可以从您的代码中调用 init 函数，因为您知道函数原型 - 参数的数量和类型。然后，您将回调到您提供的 Register 函数，该函数提供了第三方 DLL 导出的其他函数的名称，以及参数的数量和类型。Excel 开发人员将识别出 XLL 函数注册机制的描述。因此，鉴于这些函数的名称，您可以使用 GetProcAddress 获取它们的函数指针。但是如何调用它们呢？您的代码在编译时没有可用的函数声明。这些函数不使用 varargs，因此您无法在运行时使用 va_start 和 va_end 来确定参数。

解决这个困境的唯一方法是降级到汇编语言，并手工编写一些遵循 Win32 调用约定的 x86 代码，这些约定在这里 [well explained](http://unixwiz.net/techtips/win32-callconv.html) 和 [here](http://en.wikipedia.org/wiki/X86_calling_conventions) 有很好的解释。因此，这是我编写的代码，用于调用从 DLL 导出的任意函数。我使用了几个很好的资源来恢复我生疏已久的 ASM 技能：这个 [primer](http://www.cs.virginia.edu/~evans/cs216/guides/x86.html) 和这个 [x86 instruction set reference](http://x86.renejeschke.de/)。它是内联汇编，连同设置参数以简化汇编的 C++ 序言一起。

```
bool cc_cdecl = true;                         // stdcall if false
int parmBytes = ( parmCount - 1) * 4;         // parmCount includes ret val, so subtract 1
int parmPop = ( cc_cdecl ? parmBytes : 0);    // number of bytes to pop off the stack after call
void* rvInt = 0;                              // for receiving int or ptr return value
double rvDbl = 0.0;                           // for a float return value from ST(0)
int paddr = ( int)parms;                      // parms is void** array of parameters. Cast to int
                                              // to prevent implicit ptr deref by asm
```

```
// Then asm code to do a cdecl or stdcall dispatch and call xf.
__asm {                      // push parms onto stack in reverse order
        push eax             // save eax
        mov eax, paddr       // point to start of parms
        add eax, parmBytes   // point to last parm
    pp: push [eax]           // stack a parm
        sub eax, 4           // point to next parm
        cmp eax, paddr       // have we hit the start yet?
        jg pp                // if eax > parms goto pp
        call xf              // invoke the function!
        add esp, parmPop     // pop parms if cdecl
        mov rvInt, eax       // int or ptr retvals are in eax
        fst rvDbl            // float ret vals are in st0
        pop eax              // restore eax
 }
```
