<!--yml
category: 未分类
date: 2024-05-12 19:32:37
-->

# x86 __cdecl & __stdcall parameter marshalling | Coding the markets

> 来源：[https://etrading.wordpress.com/2014/07/23/x86-__cdecl-__stdcall-parameter-marshalling/#0001-01-01](https://etrading.wordpress.com/2014/07/23/x86-__cdecl-__stdcall-parameter-marshalling/#0001-01-01)

## x86 __cdecl & __stdcall parameter marshalling

### July 23, 2014

Suppose you have a third party Win32 DLL, but don’t have access to the source code. The DLL exports a well known init function that makes callbacks into your code to register more functions. So you can call Win32’s [LoadLibrary](http://msdn.microsoft.com/en-gb/library/windows/desktop/ms684175%28v=vs.85%29.aspx) to load up the DLL, and you can use [GetProcAddress](http://msdn.microsoft.com/en-gb/library/windows/desktop/ms683212%28v=vs.85%29.aspx) to get hold of a pointer to the init func. You can invoke the init function from your code because you know the function prototype – the number and type of parameters. Then you get callbacks into a Register function you supply, which gives your code the names of other functions exported by the third party DLLs, as well as the number and type of parameters. Excel developers will recognise the description of the XLL function registration mechanism. So, given the names of those functions you can use GetProcAddress to get function pointers for them. But how do you invoke them? You don’t have function declarations available at compile time in your code. The functions don’t use varargs, so you can’t use va_start and va_end to figure out the params at run time.

The only way to resolve this dilemma is to kick down to assembler, and hand code some x86 that follows the Win32 calling conventions, which are well explained [here](http://unixwiz.net/techtips/win32-callconv.html) and [here](http://en.wikipedia.org/wiki/X86_calling_conventions). So here’s the code I wrote to invoke arbitray functions exported from a DLL. I used a couple of great resources to refresh my ASM chops, which have become very rusty after years of neglect: this [primer](http://www.cs.virginia.edu/~evans/cs216/guides/x86.html) and this [x86 instruction set reference](http://x86.renejeschke.de/). It’s in inline assembler, together with the C++ preamble that sets up parameters to simplify the assembler.

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