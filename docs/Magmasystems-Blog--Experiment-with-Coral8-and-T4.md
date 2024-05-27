<!--yml

category: 未分类

date: 2024-05-18 04:53:46

-->

# Magmasystems Blog: Coral8 和 T4 的实验

> 来源：[`magmasystems.blogspot.com/2009/05/experiment-with-coral8-and-t4.html#0001-01-01`](http://magmasystems.blogspot.com/2009/05/experiment-with-coral8-and-t4.html#0001-01-01)

斯科特非常信仰一个叫做

CodeSmith

自动产生代码工具。在我们的团队中，他用它来修改 Coral8 schema 并产生

反序列化器

。

反序列化器

，还有我们称之为"

服务代理

". 问题在于斯科特是唯一的

CodeSmith

许可证，所以只有斯科特的机器能生成代码。几个月前，我在一篇博客文章中偶然发现了 T4 工具，并且向斯科特要求转换

CodeSmith

to T4\.上生成空检查代码。现在，代码生成由 Microsoft 在 Visual Studio 中免费包含的工具完成，现在每个人都可以尝试自动代码生成。

几周前，我在 Visual Studio 杂志上看到了 T4 的一篇文章，然后我发现克里斯

Donnan

正在尝试 T4。

因此，我决定在上周末花一个小时编写我的 T4 Coral8 类生成器。我没打算阅读 T4 手册，但我印象深刻的是我在非常短的时间内可以搞出的东西。这为每一个 Coral8

CCS

在特定目录中的文件。

这不是世界级的代码.... 我生成

可空

类型，我没打算在

可空

领域。但是，随意修改它。

我肯定会使用 T4 来生成类和

反序列化器

/

derserializers

为 Orinoco。

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

©2009 Marc Adler - 版权所有。

所有意见均为个人观点，与我雇主无关。
