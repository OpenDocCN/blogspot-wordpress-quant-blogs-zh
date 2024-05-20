<!--yml
category: 未分类
date: 2024-05-18 05:14:28
-->

# Magmasystems Blog: CAB and Workspaces

> 来源：[http://magmasystems.blogspot.com/2006/11/cab-and-workspaces.html#0001-01-01](http://magmasystems.blogspot.com/2006/11/cab-and-workspaces.html#0001-01-01)

**Workspaces**

You might be familiar with various kinds of layout managers that automatically arrange the windows that the manager contains. If you are a Java developer, you might be used to layout managers like the FlowLayout manager and the GridLayout manager. The layout manager works in conjunction with a container. The container holds the controls, and the layout manager positions and sizes the controls as they are added to the container.

In CAB, we have

**Workspaces**

and

**SmartParts**

. A Workspace is a container for holding SmartParts. A WorkItem contains a list of zero or more Workspaces, so you can have workspaces within workspaces.

Most CAB applications will need to create a root Workspace within the main form.

The different kinds of Workspaces in CAB are:

*   **WindowWorkspace**
    Vanilla area for holding SmartParts
    For an MdiWorkspace, will automatically create a Form to hold a SmartPart

*   **DeckWorkspace**
    Stacks SmartParts in an overlapping manner

*   **MdiWorkspace**
    Regular MDI container, derives from WindowWorkspace

*   **TabWorkspace**
    Tabbed Windows

*   **ZoneWorkspace**
    Allows tiling of window areas, good for implementing an Outlook type layout

There are two ways of adding zones. One is to use the Visual Studio .Net designer, and drag a workspace from the Toolbox onto a form.

[![](img/6c503ef627683a385d14b1aa152dbf98.png)](http://photos1.blogger.com/x/blogger/138/258/1600/544680/CABToolbox.jpg)

The other way is to dynamically create the workspace in the FormShellApplication’s

*AfterShellCreate()*

override.

Here is an example of creating various types of workspaces using the second method (the code is “unwound” for the sake of this article):

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

When you add a SmartPart to a Workspace, you can pass along hints that tell the Workspace how to layout and decorate the SmartPart. The Workspace class has functions for

*   Showing a SmartPart (which also adds the SmartPart to the Workspace as well)
*   Hiding a SmartPart
*   Activating a SmartPart
*   Closing a SmartPart

There are events that get fired when a SmartPart is activated within a Workspace, and when a SmartPart is closing within a Workspace.

You can create new, custom workspaces in CAB, and a later article will cover this.

©2006 Marc Adler - All Rights Reserved