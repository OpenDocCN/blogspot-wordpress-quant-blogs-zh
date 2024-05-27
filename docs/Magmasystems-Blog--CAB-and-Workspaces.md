<!--yml

类别：未分类

date: 2024-05-18 05:14:28

-->

# Magmasystems 博客：CAB 和工作区

> 来源：[`magmasystems.blogspot.com/2006/11/cab-and-workspaces.html#0001-01-01`](http://magmasystems.blogspot.com/2006/11/cab-and-workspaces.html#0001-01-01)

**工作区**

你可能熟悉各种自动安排包含窗口的布局管理器。如果你是 Java 开发者，你可能习惯于像 FlowLayout 管理器和 GridLayout 管理器这样的布局管理器。布局管理器与容器协同工作。容器持有控件，而布局管理器在将控件添加到容器时定位和调整控件。

在 CAB 中，我们有

**工作区**

和

**SmartParts**

。工作区是用于容纳 SmartPart 的容器。工作项包含零个或多个工作区，所以你可以有工作区在工作区中。

大多数 CAB 应用程序需要在主窗体中创建一个根工作区。

CAB 中的不同工作区类型：

+   **窗口工作区**

    用于容纳 SmartPart 的原始区域

    对于 MdiWorkspace，将自动创建一个表单来容纳 SmartPart

+   **DeckWorkspace**

    以重叠方式堆叠 SmartParts

+   **MdiWorkspace**

    常规 MDI 容器，派生自窗口工作区

+   **TabWorkspace**

    标签窗口

+   **区域工作区**

    允许布局窗口区域，适用于实现类似 Outlook 的布局

添加区域有两种方法。一种是在 Visual Studio .Net 设计器中，将工作区从工具箱拖到窗体上。

![](http://photos1.blogger.com/x/blogger/138/258/1600/544680/CABToolbox.jpg)

另一种方法是在 FormShellApplication 中动态创建工作区

*AfterShellCreate()*

override.

以下是一个使用第二种方法创建各种类型工作区的示例（为了本文，代码被“展开”了）：

```

using System;
using System.Windows.Forms;
using CABQuoteViewer.WorkItems;
using Microsoft.Practices.CompositeUI.SmartParts;
using Microsoft.Practices.CompositeUI.WinForms;

namespace CABQuoteViewer
{
    class CABQuoteViewerApplication : FormShellApplication<QuoteViewerWorkItem, MainForm>
    {
        private IWorkspace m_workspace;
        private QuoteViewerWorkItemExtension m_quoteWorkItemExt;

        /// <summary>
        /// The main entry point for the application.
        /// </summary>
        [STAThread]
        static void Main()
        {
            new CABQuoteViewerApplication().Run();
        }

        protected override void BeforeShellCreated()
        {
            base.BeforeShellCreated();

            if (this.RootWorkItem != null)
            {
                this.m_quoteWorkItemExt = new QuoteViewerWorkItemExtension();
                this.m_quoteWorkItemExt.Initialize(this.RootWorkItem);
            }
        }

        protected override void AfterShellCreated()
        {
            base.AfterShellCreated();
            this.CreateWorkspace("Deck");
        }

        private void CreateWorkspace(string wsTypeName)
        {
            if (wsTypeName == "Mdi")
            {
                this.m_workspace = new MdiWorkspace(this.Shell);
                this.RootWorkItem.Workspaces.Add(this.m_workspace, "ClientWorkspace");
            }
            else if (wsTypeName == "Tab")
            {
                this.m_workspace = this.RootWorkItem.Workspaces.AddNew<TabWorkspace>("ClientWorkspace");

                TabWorkspace tabWorkspace = this.m_workspace as TabWorkspace;
                tabWorkspace.Dock = DockStyle.Fill;
                this.Shell.Controls.Add(tabWorkspace);
            }
            else if (wsTypeName == "Deck")
            {
                this.m_workspace = this.RootWorkItem.Workspaces.AddNew<DeckWorkspace>("ClientWorkspace");

                DeckWorkspace deckWorkspace = this.m_workspace as DeckWorkspace;
                deckWorkspace.Dock = DockStyle.Fill;
                this.Shell.Controls.Add(deckWorkspace);
            }
            else if (wsTypeName == "Zone")
            {
                this.m_workspace = this.RootWorkItem.Workspaces.AddNew<ZoneWorkspace>("ClientWorkspace");

                ZoneWorkspace zoneWorkspace = this.m_workspace as ZoneWorkspace;
                zoneWorkspace.Dock = DockStyle.Fill;
                this.Shell.Controls.Add(zoneWorkspace);
            }
            else
            {
                throw new Exception("Cannot create workspace");
            }
        }
    }
}
```

当你向工作区添加 SmartPart 时，你可以传递提示，告诉工作区如何布局和装饰 SmartPart。工作区类有用于

+   显示 SmartPart（这也将 SmartPart 添加到工作区中）

+   隐藏 SmartPart

+   激活 SmartPart

+   关闭 SmartPart

当在工作区中激活 SmartPart 或关闭 SmartPart 时，会触发一些事件。

您可以在 CAB 中创建新的自定义工作区，稍后的文章将涵盖这一点。

©2006 Marc Adler - 版权所有
