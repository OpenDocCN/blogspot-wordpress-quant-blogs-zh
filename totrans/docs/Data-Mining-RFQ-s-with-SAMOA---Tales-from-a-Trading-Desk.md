<!--yml
category: 未分类
date: 2024-05-18 05:47:40
-->

# Data Mining RFQ’s with SAMOA | Tales from a Trading Desk

> 来源：[https://mdavey.wordpress.com/2014/08/06/data-mining-rfqs-with-samoa/#0001-01-01](https://mdavey.wordpress.com/2014/08/06/data-mining-rfqs-with-samoa/#0001-01-01)

## Data Mining RFQ’s with SAMOA

Decided to throw a few [RFQ’s](http://fixwiki.org/fixwiki/RFQRequest) into [SAMOA](http://samoa-project.net/).  Here’s the simple [ARFF](http://www.cs.waikato.ac.nz/ml/weka/arff.html) file I used:

```

@relation rfqs

@attribute CurrencyPair string
@attribute Notional numeric
@atrribute ClientName string
@attribute Quote numeric
@attribute RFQAccepted {0,1}

@data
'USDEUR', 5000, 'Client A', 43.33, 1

```

Firing up SAMOA with the following command line

> bin/samoa local target/SAMOA-Local-0.2.0-SNAPSHOT.jar “PrequentialEvaluation -s (ArffFileStream -f rfq.arff) -f 10 -l (classifiers.trees.VerticalHoeffdingTree -p 4)”

Which I believe has trained the SAMOA classifier to identify instances that are either likely to be an accept or reject RFQ.  Not sure yet what the prediction would be based on further data – would I be able to predict a clients RFQ outcome?

~ by mdavey on August 6, 2014.

Posted in [Data](https://mdavey.wordpress.com/category/data/)