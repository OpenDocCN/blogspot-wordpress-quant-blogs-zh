<!--yml

category: 未分类

date: 2024-05-18 05:14:35

-->

# Magmasystems Blog：CAB 应用程序类层次结构

> 来源：[`magmasystems.blogspot.com/2006/11/cab-application-class-hierarchy.html#0001-01-01`](http://magmasystems.blogspot.com/2006/11/cab-application-class-hierarchy.html#0001-01-01)

**CAB Application Classes**

下图显示了 CABApplication 类的层次结构。前三个类不应该被派生。在几乎所有类中，基于 WinForms 的应用程序将从 FormShellApplication 派生。

![](http://photos1.blogger.com/x/blogger/138/258/1600/637361/CabApplication%20hierarchy.jpg)

CAB 应用程序将由基础驱动

**CabApplication**

类。这个类完成了启动 CAB 应用程序的大部分工作。

CabApplication 类唯一的字段是根

**WorkItem**

，正如名称所示，它是整个应用程序工作项树的根节点。稍后我会讨论 WorkItems。

CabApplication 的构造函数什么也不做；这是

**Run**

（由应用程序的 Main()函数调用）引导整个应用程序的()方法。Run()方法将执行以下操作：

+   创建预定义的服务

+   验证用户。

+   读取包含应用程序要加载的所有插件模块列表的配置文件（*ProfileCatalog.xml*）。

    每个模块可以有一个可选的角色列表。只有当前用户属于该角色时，才会加载该模块。如果模块没有与之关联的角色信息，则将加载该模块。

+   创建 Shell（即：主窗体）

+   加载所有允许加载的模块。

    在从 ModuleInit 类派生的模块的每个类中，所有标记有[ServiceDependency]属性的字段都会被创建。

    所有标记有[Service]属性的类都会被添加到应用程序的服务列表中。

+   对应用程序的根 WorkItem 调用 RootWorkItem.Run()。

+   在 FormShellApplication 类中，调用 WinForm 的 Application.Run()方法启动 WinForm 应用程序。

**The Derived Application Classes**

The

**CabShellApplication**

类通过扩展 CabApplication 来扩展

+   通过将其添加到 RootWorkItem 的项目列表中来保持对 Shell（我们的 MainForm）的引用。

+   添加 BeforeShellCreated 和 AfterShellCreated 虚拟方法。这些方法可以在您的应用程序类中重写。

The

**WindowsFormApplication**

通过扩展 CabShellApplication 类来扩展

+   使用 WindowsForm 可视化程序

+   添加一些 UI 和命令例程服务

The

**FormShellApplication**

类仅覆盖 Start()方法并调用熟悉的 WinForms 方法

Application.Run(mainform)

.

©2006 Marc Adler - 版权所有
