<!--yml

类别：未分类

日期：2024-05-18 05:14:15

-->

# Magmasystems 博客：CAB 和工作项

> 来源：[`magmasystems.blogspot.com/2006/11/cab-and-workitems.html#0001-01-01`](http://magmasystems.blogspot.com/2006/11/cab-and-workitems.html#0001-01-01)

**工作项**

一个

**工作项**

在 CAB 术语中，它被认为代表一个“用例”。忽略这个。它实际上只是一个包含其他类型对象以及一些状态信息的容器。

一个 CAB 应用程序有一个工作项树。主要的 CabApplication 类包含对根工作项的引用，它是由

**根工作项**

属性。给定一个工作项，您可以向上移动一个级别到其父工作项，或者通过访问工作项向下移动到下一个级别。

**工作项**

集合。

回想一下，主应用程序类是这样定义的：

**类 CABQuoteViewerApplication：FormShellApplication**

在泛型的参数列表中的第一个参数是将成为我们整个应用程序的`RootWorkItem`的工作项类型。所有其他的工作项都将是这个`RootWorkItem`的子项。一个工作项可以访问其任何子项的属性；然而，兄弟姐妹工作项不能直接访问彼此的属性。

工作项还包含各种其他集合。它有如下集合：

+   工作区

+   智能部件

+   命令

+   事件主题

+   服务

+   项目（您可以将任何对象放入这个集合中，包括状态、视图等）

一个工作项可以包含一个

**状态**

。这是一个命名集合，包含名称/值对。当状态中的值发生变化时会触发事件。当工作项被保存时，其状态会与其一起保存。

您可以激活/去激活一个工作项，终止它，并持久化它（保存和加载）。

有一个名为

***OnRunStarted***

()，您可以重写它以创建视图、读取数据等。

**工作项扩展**

一个

**工作项扩展**

是一种扩展工作项行为的方法，而无需更改工作项的代码或诉诸于工作项的子类化。它是一个类，只是接收与关联工作项发生的某些事件。这些事件包括：

初始化

运行开始

激活

去激活

终止

要扩展工作项，您需要创建一个工作项扩展的子类。然后，您需要创建该类的对象；这个对象与底层的工作项相关联。然后，您只需处理工作项发生的某些事件。

````

 public class QuoteViewWorkItemExtension : WorkItemExtension
{
  public QuoteViewWorkItemExtension() {}

  protected override OnActivated()
  {
    PerformanceTimer.StartPerformanceTiming();
  }

  protected override OnDeactivated()
  {
    PerformanceTimer.StopPerformanceTiming();
  }
}
````

使用这个新的工作项扩展，您需要做以下操作：

```
 QuoteViewWorkItemExtension wix = new QuoteViewWorkItemExtension();
Wix.Initialize(myWorkItem); 
```

这个概念与 Spring.Net 等 AOP 容器提供的“建议”非常相似，只不过你没有任何运行时代码注入。

©2006 Marc Adler - 版权所有
