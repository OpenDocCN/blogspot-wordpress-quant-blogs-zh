<!--yml

类别：未分类

日期：2024-05-12 19:29:47

-->

# windbg | 编码市场

> 来源：[`etrading.wordpress.com/windbg/#0001-01-01`](https://etrading.wordpress.com/windbg/#0001-01-01)

### **windbg 链接、技巧和窍门集锦**

#### 入门材料

#### 贴士与技巧

+   你的 PDB（调试信息文件）必须与你的 DLL（动态链接库）和 EXE（可执行文件）相匹配。即使你使用相同的编译器开关构建了它们，如果它们不是来自同一次构建，它们也不会匹配，因为编译器会注入一个 windbg 检查的校验和。你可以在 stackoverflow 上找到一些绕过这个问题的方法。但如果可能的话，重新构建并生成一套匹配的 bins 和 PDBs 吧。你会发现，当 bins 和 PDBs 匹配时，windbg 中的许多功能都会奇迹般地开始正常工作：在 C++ 方法名上设置断点、变量检查、在“ .frame N”中上下跟踪堆栈时自动查看源代码等。

+   清理注册表键以重置 windbg。例如，如果你无法让命令窗口发出 g、bp、bl 等命令，则使用 regedit 清除键可以有所帮助。删除 HKCU\Software\Microsoft\Windbg 下的所有内容。

+   如果你正在调试一个 32 位二进制文件，请使用 32 位调试器。不要尝试使用 .effmach x86 命令将 64 位调试器工作在 32 位模式下。

+   .expr 命令会告诉你是否使用了 MASM 或 C++ 风格的符号。如果还没有处于那种模式，使用“ .expr /s c++”来切换到 C++ 符号模式。设置断点和检查变量会更容易。

+   在‘<EOL>’处出现类型冲突错误：有时我在设置断点时，如果模块名称写错了，就会出现这种情况。检查你的‘bp module!class::method’语法。模块与 DLL 名称相同，不包括 .dll 后缀。

#### windbg 命令

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

### Sys Internals（系统内部工具）

SysInternal 的工具进程资源管理器和进程监视器是必不可少的调试工具。以下是它们可以快速解决的一些常见调试场景…

+   进程资源管理器

    +   当你尝试覆盖一个 DLL 时，Windows 会给出“权限被拒绝”的错误。你有写权限，所以你知道某个运行中的进程必须已加载了该 DLL。但是是哪个进程呢？使用 PE 的 Find/Find Handle 或 DLL 菜单选项。

+   进程监视器

    +   DLL 地狱：哪些 DLL 正在加载，以及为什么？哪些加载失败了？depends.exe 可以告诉你很多信息，但它不会帮助你处理运行时行为。设置事件过滤器为文件系统和注册表，PM 将显示你在注册表中检查了哪些 ProgId 和 ClassId 条目，以及一个二进制文件正在查看哪些文件系统路径。
