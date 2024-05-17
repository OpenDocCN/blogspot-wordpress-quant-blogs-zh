<!--yml
category: 未分类
date: 2024-05-18 04:53:46
-->

# Magmasystems Blog: Experiment with Coral8 and T4

> 来源：[http://magmasystems.blogspot.com/2009/05/experiment-with-coral8-and-t4.html#0001-01-01](http://magmasystems.blogspot.com/2009/05/experiment-with-coral8-and-t4.html#0001-01-01)

Scott was a big believer in a tool called

CodeSmith

to automatically generate code. In our group, he used it to take a Coral8 schema and generate

serializers

,

deserializers

, and something that we call "

ServiceAgents

". The problem was that Scott had the only

CodeSmith

license, so only Scott's machine was able to do the code generation. A few months ago, I had stumbled upon the T4 tool in a blog post, and I had asked Scott to switch over from

CodeSmith

to T4\. Now, the code generation is done by a free tool that Microsoft includes in Visual Studio, so now everyone can experiment with automatic code generation.

A few weeks ago, I found an article in Visual Studio magazine about T4, and then I saw that Chris

Donnan

was experimenting with T4.

So, I decided to spend an hour last weekend and code up my own T4 Coral8 class generator. I did not bother to read the T4 manual, but I was impressed with what I could rig up in a very short time. This generates a class for every Coral8

CCS

file in a certain directory.

This isn't world-class code .... I generated

nullable

types and I did not bother to generate null-checking code on the

nullable

fields. But, feel free to modify it.

I will certainly use T4 to generate classes and

serializers

/

derserializers

for Orinoco.

```

<#@ template language="C#" #>
<#@ assembly name="System.Xml" #>
<#@ import namespace="System.IO" #>
<#@ import namespace="System.Xml" #>
<#@ import namespace="System.Collections.Generic" #>

using System;
using Coral8.Transport;
using Coral8.Value;

<# 
    DirectoryInfo dir = new DirectoryInfo(@"v:\dev\CEP\C8Projects\Schemas");
    foreach (FileInfo file in dir.GetFiles("*.ccs"))
    {
        string sSchemaFile = file.Name.Replace(".ccs", "").Replace("-", "");
        List<Info> colInfo = new List<Info>();
        using (StreamReader reader = new StreamReader(file.FullName))
        {
            XmlDocument xmldoc = new XmlDocument();
            xmldoc.Load(reader);
            XmlNodeList columns = xmldoc.GetElementsByTagName("Column");
            foreach (XmlNode node in columns)
            {
                string colName = node.Attributes["Name"].Value;
                string type = node.Attributes["xsi:type"].Value;
                string netType = "unknown";
                string c8FieldType = "unknown";

                if (type.StartsWith("String"))
                {
                    netType = "string";
                    c8FieldType = "StringFieldValue";
                }
                else if (type.StartsWith("Int"))
                {
                    netType = "int?";
                    c8FieldType = "IntegerFieldValue";
                }
                else if (type.StartsWith("Long"))
                {
                    netType = "long?";
                    c8FieldType = "LongFieldValue";
                }    
                else if (type.StartsWith("Time"))
                {
                    netType = "DateTime?";
                    c8FieldType = "TimeFieldValue";
                }    
                else if (type.StartsWith("Float"))
                {
                    netType = "double?";
                    c8FieldType = "FloatFieldValue";
                }    
                else if (type.StartsWith("Bool"))
                {
                    netType = "bool?";
                    c8FieldType = "BooleanFieldValue";
                }    
                else if (type.StartsWith("Xml"))
                {
                    netType = "string";
                    c8FieldType = "XmlFieldValue";
                }

                colInfo.Add(new Info(colName, netType, c8FieldType));
            } // end foreach node
        } // end using
#>

#region <#= sSchemaFile #> Serializer
public class <#= sSchemaFile #>
{
<# 
        foreach (Info info in colInfo)
        {
#>
    public <#= info.NetType #> <#= info.Name #>;
<#
        }
#>        
    public void ToObject(Tuple tuple)
    {
<# 
        foreach (Info info in colInfo)
        {
            if (info.C8FieldValue == "TimeFieldValue")
            {
#>        
        this.<#= info.Name #> = new DateTime(((<#= info.C8FieldValue #>) tuple.GetFieldValue("<#= info.Name #>")).Value.Value);
<#
            }
            else
            {
#>        
        this.<#= info.Name #> = ((<#= info.C8FieldValue #>) tuple.GetFieldValue("<#= info.Name #>")).Value;
<#
            }
        }
#>        
    }

    public Tuple ToTuple()
    {
        Tuple tuple = new Tuple();
<# 
        foreach (Info info in colInfo)
        {
            if (info.C8FieldValue == "TimeFieldValue")
            {
#>        
        tuple.SetFieldValue("<#= info.Name #>", new <#= info.C8FieldValue #>(this.<#= info.Name #>.Value.Ticks));
<#
            }
            else if (info.C8FieldValue == "StringFieldValue" || info.C8FieldValue == "XmlFieldValue")
            {
#>
        tuple.SetFieldValue("<#= info.Name #>", new <#= info.C8FieldValue #>(this.<#= info.Name #>));
<#            
            }
            else
            {
#>        
        tuple.SetFieldValue("<#= info.Name #>", new <#= info.C8FieldValue #>(this.<#= info.Name #>.Value));
<#
            }
        }
#>

        return tuple;
    }
}
#endregion
<#
    }
#>
<#+
    public class Info
    {
        public string Name;
        public string NetType;
        public string C8FieldValue;

        public Info(string name, string type, string val)
        {
            this.Name = name;
            this.NetType = type;
            this.C8FieldValue = val;
        }
    }
#>

```

©2009 Marc Adler - All Rights Reserved.

All opinions here are personal, and have no relation to my employer.