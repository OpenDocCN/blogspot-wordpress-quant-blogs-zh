<!--yml

category: 未分类

date: 2024-05-18 04:58:50

-->

# Magmasystems Blog: The SQLDependency Object and Entitlements

> 来源：[`magmasystems.blogspot.com/2008/09/sqldependency-object-and-entitlements.html#0001-01-01`](http://magmasystems.blogspot.com/2008/09/sqldependency-object-and-entitlements.html#0001-01-01)

Our

CEP

Servers have to run 24x6\. When our server starts up, it reads some tables in our

SQL

Server 2005 database that contains information about users and the alerts that they are entitled to see. We don't want most of our users to be able to see alerts that occur because of order messages, but we do want our users to see alerts that occur from execution reports.

If we had to query the database for the entitlements on every single alert that flows through our system, we would take a tremendous hit in performance. Therefore, we cache the entitlements in memory and cache the result sets.

We want to be able to change our entitlements on-the-fly, while the server is running. We want to add and delete users, change the method of notification for a user (

Tibco

,

SMS

, email, messenger, etc), and add new alerts to our system. We could restrict all changes to the underlying entitlements tables so that the changes would have to made made through an Administrative GUI, but because of the environment inside our company, we cannot. Someone might add a user through the Admin GUI, and others might decide to go right into our

SQL

Server database and add some new rows to our tables.

We need a way to detect when the

entitlement

tables have changed within our

SQL

Server database while our server in running, and have those changes reflected in the operation of our system. We cannot afford to bring our system down, make the changes to the entitlements, and restart our system. We also don't want to wait until the end of the week for the "green zone" period, where we can safely bring down our system, make the changes, and restart the system.

SQL

Server 2005 has a class called

SqlDependency

. This class can be used as an interface between

SQL

Service Broker and a .NET application to inform the .NET application when a certain query's result set has changed.

Most of the literature on the

SqlDependency

class revolves around using it in an ASP.NET application. There are also a bunch of things that you need to be aware of, such as restrictions on the syntax of the query that you give to the

SqlDependency

class. It took a little bit of digging and experimentation for me to get this stuff to work, but after a little while, we found that it did the job nicely.

I have enclosed the source code to a simple

EntitlementTableWatcher

class that shows you how to use

SqlDependency

. I have also include some links to URLs that I found useful. If you have any comments about the code, or if you find any bugs, please let me know and I will correct them.

```

  #region Entitlements Table Watcher
  internal class EntitlementTableChangedWatcher : DisposableObject
  {
      // http://msdn.microsoft.com/en-us/library/ms379594.aspx is a good article by Developmentor

      private readonly EntitlementModel m_entitlementModel;
      private SqlConnection m_connection;
      private SqlDependency m_dependency;
      private SqlCommand m_command;
      private SqlDataReader m_reader;

      public EntitlementTableChangedWatcher(EntitlementModel entitlementModel)
      {
          SqlDependency.Stop(ConnectionString);
          SqlDependency.Start(ConnectionString);

          this.m_connection = new SqlConnection(ConnectionString);
          this.m_connection.Open();

          this.m_entitlementModel = entitlementModel;
      }

      protected override void Free(bool disposedByUser)
      {
          if (disposedByUser)
          {
              this.CleanupCommand();
              if (this.m_connection != null)
              {
                  this.m_connection.Dispose();
                  this.m_connection = null;
              }
              SqlDependency.Stop(ConnectionString);
          }

          base.Free(disposedByUser);
      }

      private void CleanupCommand()
      {
          // In case we entered here from the callback, we need to clean up the last command so that
          // we can issue a new command.
          if (this.m_reader != null)
          {
              this.m_reader.Dispose();
              this.m_reader = null;
          }
          if (this.m_command != null)
          {
              this.m_command.Notification = null;
              this.m_command.Dispose();
          }
      }

      public void PollForNotifications()
      {
          try
          {
              // In case we entered here from the callback, we need to clean up the last command so that
              // we can issue a new command.
              this.CleanupCommand();

              // Create a new SqlCommand object.
              // http://msdn.microsoft.com/en-us/library/aewzkxxh.aspx contains rules for the syntax of the query.
              // Make sure that the command has no notification object associated with it
              this.m_command = new SqlCommand("SELECT Column1, Column2 FROM dbo.Subscription", this.m_connection)
                                   {Notification = null};

              // Create a dependency and associate it with the SqlCommand.
              this.m_dependency = new SqlDependency(this.m_command);
              this.m_dependency.OnChange += this.OnDependencyChange;

              // We want to send a fresh SELECT command to SQL Server on startup and after we receive a notification.
              // We use the DataReader to drain the result set resulting from the query. SQL Server will execute 
              // this command, and set up the entire Query Notification plumbing. SQL Server will execute
              // this command internally every once in a while, and will send a one-time event to us when it detects that the
              // query has changed. It is up to us to manually subscribe for further events.
              this.m_reader = this.m_command.ExecuteReader();
              while (this.m_reader.Read())
                  ;
          }
          catch (Exception exc)
          {
              Logger.Log.Error("Problem in the Server's entitlement table watcher", exc);
          }
      }

      void OnDependencyChange(object sender, SqlNotificationEventArgs e)
      {
          // This event firing is a one-time thing ... we have to manually
          // reset everything in order to receive another event
          SqlDependency dependency = (SqlDependency) sender;
          dependency.OnChange -= this.OnDependencyChange;

          // Process the event
          if (e.Type == SqlNotificationType.Change)
          {
              this.m_entitlementModel.ClearEntitlementsCache();
          }

          // Go back and wait for another event
          this.PollForNotifications();
      }
  }
  #endregion

```

©2008 Marc Adler - All Rights Reserved.

All opinions here are personal, and have no relation to my employer.
