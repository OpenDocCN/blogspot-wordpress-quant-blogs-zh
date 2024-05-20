<!--yml
category: 未分类
date: 2024-05-18 05:20:27
-->

# Magmasystems Blog: Services for the Wall Street Stack

> 来源：[http://magmasystems.blogspot.com/2006/05/services-for-wall-street-stack.html#0001-01-01](http://magmasystems.blogspot.com/2006/05/services-for-wall-street-stack.html#0001-01-01)

I have blogged before about the need for a standardized Wall Street Stack. At my current client, there are several different frameworks that have been built over the years, but no framework has gained enterprise-wide acceptance.

These are the services that are generally needed for a complete application framework. If you can think of any other, let me know.

**Authentication**

- logging in to various databases, web servers, internal systems, etc. Best implemented through an enterprise-wide authentication service (using the user's Kerberos token, etc)

**Authorization**

(Entitlements) - what actions can a user perform within an application and what data is a user entitled to see. Best accomplished through an enterprise-wide system.

**Logging**

- log interesting things that happen in an application. Log4Net is a good framework.

**User Preferences**

- load and save the state of the UI

**User Data**

- each application may want to persist the last state of the application when the user logged off

**Configuration**

- Each application should be configurable through a series of XMl files.

**General Services Manager**

- drives the entire service locator framework

**Applet Management**

- load applets from .NET assemblies

**Internal Event Broker**

- lightweight communication between applets

**Data and Persistence layer**

- ways to load, query, update and cache data. Should be configurable so that we can go through different transport layers

**Service Agents**

- processed async notifications that come to us through subscriptions.

**Shell**

- handles initialization of the application, calls all of the various services, provides presentation services for the applets

**UI**

- menu manager, status bar manager, navbar manager, toolbar manager

**Security/Cryptography**

- does the data need to be encrypted and decrypted? (passwords, sensitive data)

**Exception Handling**

- provides a unified way of handling errors that occur in shell and the various applets

**Threading**

- model for async processing

©2006 Marc Adler - All Rights Reserved