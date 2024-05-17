<!--yml
category: 未分类
date: 2024-05-18 06:09:59
-->

# StreamInsight CTP2 available on MSDN | Tales from a Trading Desk

> 来源：[https://mdavey.wordpress.com/2009/08/19/streaminsight-ctp-available-on-msdn/#0001-01-01](https://mdavey.wordpress.com/2009/08/19/streaminsight-ctp-available-on-msdn/#0001-01-01)

## StreamInsight CTP2 available on MSDN

Documentation and samples available [here](http://go.microsoft.com/fwlink/?LinkId=160598). I never saw CTP1, no idea who that went to. The StreamInsight Event Flow Debugger tool is included in the release.

![streaminsight](img/8db7ad7bed10c4acf74079f5ba31e3ae.png "streaminsight")

StreamInsight can either be hosted or run in standalone mode (StreamInsightHost.exe). Three development models are supported – all support the definition of the query logic through LINQ expressions 🙂 . The models are:

*   Explicit – provides a full-service complex event processing (CEP) application environment by allowing the application developer to explicitly create and register all of the objects required to transform and process events coming into and going out of the CEP server
*   Implicit – provides an easy-to-use environment that hides much of the complexity associated with the explicit model
*   IObservable/IObserver – provides an alternative to using input and output adapters as the producer and consumer of event sources and sinks

The ObjectModel sample appear to have a few issues:

Creating CEP Server
Creating CEP Application
Registering Event Type
Registering Adapter Factories
Registering LINQ query template
Registering bound query
Start query

Diagnostic View for ‘cep:/Server/EventManager’:
All Events Count: 3
All Events Memory (bytes): 69632
Diagnostic View for ‘cep:/Server/PlanManager’:
Query Count: 3
Stream Count: 17
Operator Count: 16
Diagnostic View for ‘cep:/Server/Application/ObjectModelSample/Query/TrafficSens
orQuery’:
Query State: Aborted
Start Time: 19/08/2009 07:00:52
End Time: 19/08/2009 07:00:52
Query Exception: Microsoft.ComplexEventProcessing.Engine.OperatorExecutionExcep
tion: The adapter ‘locationInput’ of type ‘CepSamples.InputAdapters.TextFileEdge
Input’, query ‘TrafficSensorQuery’, failed to start. —> System.FormatException
: String was not recognized as a valid DateTime.
at System.DateTimeParse.Parse(String s, DateTimeFormatInfo dtfi, DateTimeStyl
es styles)
at System.Convert.ToDateTime(String value, IFormatProvider provider)
at CepSamples.InputAdapters.TextFileEdgeInput.CreateEventFromLine(String line
) in c:\temp\cep\Samples\InputAdapters\TextFileInputAdapter\TextFileEdgeInput.cs
:line 257
at CepSamples.InputAdapters.TextFileEdgeInput.ProduceEvents() in c:\temp\cep\
Samples\InputAdapters\TextFileInputAdapter\TextFileEdgeInput.cs:line 144
at CepSamples.InputAdapters.TextFileEdgeInput.Start() in c:\temp\cep\Samples\
InputAdapters\TextFileInputAdapter\TextFileEdgeInput.cs:line 66
at Microsoft.ComplexEventProcessing.Adapters.Adapter.ThreadProcStart(Object t
hisPtr)
— End of inner exception stack trace —
Stream Count: 0
Operator Count: 0
Total Incoming Event Count: 2
Total Consumed Event Count: 2
Total Produced Event Count: 1
Total Outgoing Event Count: 1
Last Incoming Event System Time: 19/08/2009 07:00:52
Last Consumed Event System Time: 19/08/2009 07:00:52
Last Produced Event System Time: 19/08/2009 07:00:52
Last Outgoing Event System Time: 19/08/2009 07:00:52
Total Consumed Events Latency (milliseconds): 32
Total Produced Events Latency (milliseconds): 44
Total Outgoing Events Latency (milliseconds): 47
Last Produced CTI Timestamp: 01/01/0001 00:00:00
Stream Event Count: 0
Stream Memory Including Events (bytes): 0
Operator Index Event Count: 0
Operator Event Memory (bytes): 0
Operator Index Memory (bytes): 0
Total Number of Times Operator Scheduled: 4
Total Operator CPU Usage (milliseconds): 0

~ by mdavey on August 19, 2009.

Posted in [Uncategorized](https://mdavey.wordpress.com/category/uncategorized/)
Tags: [Microsoft](https://mdavey.wordpress.com/tag/microsoft/)