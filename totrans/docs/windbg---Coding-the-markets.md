<!--yml
category: 未分类
date: 2024-05-12 19:29:47
-->

# windbg | Coding the markets

> 来源：[https://etrading.wordpress.com/windbg/#0001-01-01](https://etrading.wordpress.com/windbg/#0001-01-01)

### **A collection of windbg links, tips and tricks**

#### Introductory material

#### Tips & tricks

*   Your PDBs must match your DLLs and EXEs. Even if you’ve built with the same set of compiler switches, they won’t match if they’re not from the same build, as the compiler injects a checksum that windbg checks. You can find some hacky ways around this on stackoverflow. But if it’s at all possible to rebuild and generate a matching set of bins and PDBs do so. You’ll find a huge amount of stuff in windbg starts just working when bins and PDBs match: breakpointing on C++ method names, variable inspection, automatic viewing of source code when stepping up and down the stack with “.frame N” etc.
*   Clear down registry keys to reset windbg. For instance, if you can’t get the command window to issue g, bp, bl etc, then using regedit to clear keys can help. Delete everything under HKCU\Software\Microsoft\Windbg
*   If you’re debugging a 32 bit binary, use the 32 bit debugger. Don’t attempt to make the 64 bit debugger work in 32 bit mode with the .effmach x86 command
*   The .expr command will tell you if you’re using MASM or C++ style symbols. Use “.expr /s c++” to flip into C++ symbol mode if not already in that mode. Setting breakpoints and examining variables will be much easier.
*   Type conflict error at ‘<EOL>’: I get this sometimes setting a breakpoint when I get a module name wrong. Check your ‘bp module!class::method’ syntax. The module is the same as the DLL name, without the .dll suffix.

#### windbg commands

```
  g to go
  k, kb, kd for stack. kp for stack with params, kn with frame nums. ~*kvn
  .frame n   navigate to stack frame n
  .restart
  .lastevent
  .effmach x86  tell 64bit windbg to work with 32bit exe
  ~  thread info
  ~. current thread info 
  ~* list threads
  ~N kp stack for thread N. N is not a TID, it's an index  
  l+t go into source mode
  bl: list breakpoints, bc *: clr all bps
  dv  show locals
  lm  list modules and what dbg symbols they have loaded
  .lines  is line number info loaded ?
  .expr  which expression evaluator
  .expr /s c++  use c++ expr eval
  x <module>!<symbol>   display symbols loaded
  x sc!*                list all symbo ls in sc.dll
  uf <module>!<symbol>  disassemble a symbol
  .reload               force windbg to walk image path loading DLLs
  bp officeloader!desktop_win32::extendLoaderEnvironment
  bm officeloader!tools::resolveLink
  bc  clear BPs
  bd  disable BPs
  .reload /f /i MyDll.dll
  .reload /unl MyDll.dll
  .reload                 reload all modules
  !sym noisy              track symbol problems
  ?  eval expr
  ?? eval C++ expr
     eg ?? aName.mpData
        ?? aName.mpData->maStr
  du  dump unicode  eg du aName.mpData->maStr
  p/F10 step over
  t/F11 step in
  gu               go up - step out
  .load SOS        load up .Net dbg support
  .load sosex.dll  load 
  !clrstack        .Net stack
  !DumpDomain      to list loaded .Net modules
  !bpmd ExcelDna.Integration ExcelDnaUtil.GetApplicationFromWindow
  !peb  display process environment block
  sxe 0x800706ba   break on first chance 0x800706ba exception
  sxe av           break on first chance access violation
  sxd av           disable break on first chance exception
```

### Sys Internals

SysInternal’s tools Process Explorer and Process Monitor are essential debugging tools. Here are some common debugging scenarios they can resolve quickly…

*   Process Explorer
    *   Windows gives you “permission denied” when you attempt to overwrite a DLL. You’ve got write permission, so you know some running process must have that DLL loaded. But which one? Use PE’s Find/Find Handle or DLL menu option
*   Process Monitor
    *   DLL hell: which DLLs are loading, and why? And which are failing to load? depends.exe can tell you a lot, but it won’t help with runtime behaviour. With event filters set to file system and Registry, PM will show you which ProgId and ClassId entries are checked in the registry, and which paths on the FS a binary is looking at.