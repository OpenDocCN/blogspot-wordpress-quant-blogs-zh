<!--yml
category: 未分类
date: 2024-05-18 05:24:22
-->

# Magmasystems Blog: The Night of the Living Config Files

> 来源：[http://magmasystems.blogspot.com/2005/10/night-of-living-config-files.html#0001-01-01](http://magmasystems.blogspot.com/2005/10/night-of-living-config-files.html#0001-01-01)

My colleague

[Pinakin](http://pinakin-uk.blogspot.com)

blogged today about config file hell in his project.

This brought a chuckle to me. We went through precisely the same thing at the last project. For one part of our system, we were forced to use a framework that was built by an outside consulting firm that had done some work for my client, a big financial powerhouse. This framework used the service locator paradigm to manage services. Each service had its own XML-based config file, complete with the absolute paths to all of the various DLLs encoded. This outside company also had the nasty habit of changing the namespaces of the various assemblies with each major release of the framework. Needless to say, every major release brought some headaches on our side as we scrambled to find all of the various assemblies that were no longer loading.

We saw some mistakes in the implementation of this outside framework. If you are writing systems that use the service locator pattern, there are some things that you need to be aware of.

1) Sequencing. Certain services must be loaded before others if there are dependencies between services. For example, if you have a logging service, and this logging service uses an exception-handling service if the log file cannot be created, then the exception handling service must be loaded in prior. A mistake that this framework made was to read all of the service agent configuration info into a hashtable and then iterate through the hashtable to instantiate each service. Well, hashtables are iterated in a quasi-random fashion, so you can certainly run into sequencing issues as you instantiate each service.

2) Default behavior. If a "non-crucial" service cannot be loaded, do you abort the program? For example, if the logging service cannot be loaded, just turn off logging (unless the business requirements are such that logging must be always functional due to auditing rules). Do something reasonable if as service cannot be loaded. Don't just come back with a cryptic error message. I have spent more time tracing Assembly.Load() errors than I care to imagine.