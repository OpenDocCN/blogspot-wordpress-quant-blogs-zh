<!--yml
category: 未分类
date: 2024-05-18 05:14:35
-->

# Magmasystems Blog: The CAB Application Class Hierarchy

> 来源：[http://magmasystems.blogspot.com/2006/11/cab-application-class-hierarchy.html#0001-01-01](http://magmasystems.blogspot.com/2006/11/cab-application-class-hierarchy.html#0001-01-01)

**CAB Application Classes**

The hierarchy of the CABApplication classes is shown in the diagram below. The top three classes should never be derived from. In almost all classes, your WinForms-based application will derive from FormShellApplication.

[![](img/e2bb983832bd11fa12dbe0ca781cee0e.png)](http://photos1.blogger.com/x/blogger/138/258/1600/637361/CabApplication%20hierarchy.jpg)

A CAB Application will be driven by the base

**CabApplication**

class. This class does most of the work to get the CAB application started.

The only field that the CabApplication class has is the root

**WorkItem**

, which as the name implies, is the root node of the entire application’s WorkItem tree. I will discuss WorkItems later.

The constructor of CabApplication does nothing; it is the

**Run**

() method (which is called by your application’s Main() function) that bootstraps the entire application. The Run() method will do the following:

*   Create the pre-defined services

*   Authenticate the user.

*   Reads the config file (*ProfileCatalog.xml*) that contains a list all of the plug-in modules that the app wants to load.
    Each module can have an optional list of Roles. The module will be loaded only if the current user belongs to that role. If a module has no role information associated with it, then the module will be loaded.

*   Creates the Shell (ie: the MainForm)

*   Loads all of the modules that are permitted to be loaded.
    In each class in the module that derived from the ModuleInit class, all fields that are tagged with the [ServiceDependency] attribute are created.
    All classes tagged with the [Service] attribute are added to the application’s list of services.

*   RootWorkItem.Run() is called for the applications root WorkItem.

*   In the FormShellApplication class, the WinForm’s method Application.Run() is called to start the WinForm app.

**The Derived Application Classes** 

The

**CabShellApplication**

class extends the CabApplication by

*   Keeping a reference to the Shell (our MainForm) by adding it to the RootWorkItem’s list of items.

*   Adding BeforeShellCreated and AfterShellCreated virtual methods. These methods can be overridden in your application class.

The

**WindowsFormApplication**

extends the CabShellApplication class by

*   Using a WindowsForm Visualizer

*   Adding some UI and command-routine services

The

**FormShellApplication**

class merely overrides the Start() method and calls the familiar WinForms method

Application.Run(mainform)

.

©2006 Marc Adler - All Rights Reserved