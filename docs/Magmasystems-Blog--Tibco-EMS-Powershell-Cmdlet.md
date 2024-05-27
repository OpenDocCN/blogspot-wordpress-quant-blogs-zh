<!--yml

类别：未分类

日期：2024-05-18 05:01:45

-->

# Magmasystems 博客：Tibco EMS PowerShell 命令行工具

> 来源：[`magmasystems.blogspot.com/2008/06/tibco-ems-powershell-cmdlet.html#0001-01-01`](http://magmasystems.blogspot.com/2008/06/tibco-ems-powershell-cmdlet.html#0001-01-01)

一个用于获取关于您的 Tibco EMS 主题（或特定主题）信息的 PowerShell 命令行工具。

```

using System;
using System.Management.Automation;
using TIBCO.EMS.ADMIN;

namespace MarcsPowershellCmdlets
{
    [Cmdlet(VerbsCommon.Get, "TibcoTopics", SupportsShouldProcess = true)]
    public class GetTibcoTopicsCmdlet : Cmdlet
    {
        #region Parameters
        [Parameter(Position = 0,
         Mandatory = false,
         ValueFromPipelineByPropertyName = true,
         HelpMessage = "The URL of the Tibco EMS broker")]
        [ValidateNotNullOrEmpty]
        public string URL
        {
            get; set;
        }

        [Parameter(Position = 1,
         Mandatory = false,
         ValueFromPipelineByPropertyName = true,
         HelpMessage = "The UserName of the Tibco EMS broker")]
        [ValidateNotNullOrEmpty]
        public string User
        {
            get; set;
        }

        [Parameter(Position = 2,
         Mandatory = false,
         ValueFromPipelineByPropertyName = true,
         HelpMessage = "The Password of the Tibco EMS broker")]
        [ValidateNotNullOrEmpty]
        public string Password
        {
            get; set;
        }

        [Parameter(Position = 3,
         Mandatory = false,
         ValueFromPipelineByPropertyName = true,
         HelpMessage = "The name of the topic the look at")]
        [ValidateNotNullOrEmpty]
        public string Topic
        {
            get;
            set;
        }
        #endregion

        protected override void ProcessRecord()
        {
            try
            {
                if (string.IsNullOrEmpty(this.URL))
                    this.URL = "tcp://localhost:7222";
                if (string.IsNullOrEmpty(this.User))
                    this.User = "admin";

                Admin admin = new Admin(this.URL, this.User, this.Password);
                TopicInfo[] topics = admin.Topics;

                if (string.IsNullOrEmpty(this.Topic))
                {
                    this.WriteObject(topics, true);
                }
                else
                {
                    foreach (TopicInfo topic in topics)
                    {
                        if (topic.Name.Equals(this.Topic, StringComparison.InvariantCultureIgnoreCase))
                        {
                            this.WriteObject(topic);
                            break;
                        }
                    }
                }

                admin.Close();
            }
            catch (Exception)
            {
                Console.WriteLine("Cannot connect to the Tibco EMS broker");
            }
        }
    }
}

```

©2008 Marc Adler - 版权所有
