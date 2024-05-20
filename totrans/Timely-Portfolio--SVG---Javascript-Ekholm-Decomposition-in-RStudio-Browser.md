<!--yml
category: 未分类
date: 2024-05-18 14:51:09
-->

# Timely Portfolio: SVG + Javascript Ekholm Decomposition in RStudio Browser

> 来源：[http://timelyportfolio.blogspot.com/2014/10/svg-javascript-ekholm-decomposition-in.html#0001-01-01](http://timelyportfolio.blogspot.com/2014/10/svg-javascript-ekholm-decomposition-in.html#0001-01-01)

Our topics this week seem unrelated, but in an effort to bridge the two

another random project – make website in R for these SVGs of Portland Vector Bridges
result: [Portland Bridges in SVG](http://timelyportfolio.github.io/portland_vector_bridges)
code: [R to make simple site](https://github.com/timelyportfolio/portland_vector_bridges/blob/gh-pages/code.R) 
Ekholm decomposition

Responsive SVG in the browser

let’s build a website in R with htmltools to calculate the Ekholm decomposition in Javascript using this nifty [simple-statistics.js](http://www.macwright.org/simple-statistics/) from the brilliant [Tom Macwright](http://www.macwright.org/about/).  The result will not be beautiful and I’ll leave out a fancy interactive chart, but that is intentional to reduce the amount of code and dependencies.

[![r_ekholm_js](img/a2ae6406e023f42e2fc7dd246b201dac.png "r_ekholm_js")](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEj1AX6MabEEEt5WLuFOSRo2tOQvD6RKsjx_oBoheQaG1_NsEWyXa3tXR0koXTK6-NaIFpfUb4eFHmjnSD10o1yeKSqtW2BCl97VKndLOl4emrUxOjanoTp7yIwIC0mDlHc8xYd9K3EQ5A/s1600-h/r_ekholm_js%25255B3%25255D.gif)

I wonder what I’ll get into next week.

[Github Repo](http://github.com/timelyportfolio/rCharts_factor_analytics)

```
library(htmltools)
library(pipeR)
library(jsonlite)
library(Quandl)
library(xts)

# use Quandl Kenneth French Fama/French factors
# http://www.quandl.com/KFRENCH/FACTORS_D
#f <- Quandl("KFRENCH/FACTORS_D",type = "xts", start_date="2010-12-31") / 100

tagList(
  #pull in the bridge to span all the week's topics
  #Portland Vector Bridges http://timelyportfolio.github.io/portland_vector_bridges
  tags$div( style = "height:15%;width:100%"
    ,readLines(
      "http://timelyportfolio.github.io/portland_vector_bridges/Burnside Bridge.svg"
    ) %>>% HTML
  )
  ,tags$h1( "Sparsest Test in Javascript of Ekholm")
  , tags$div( style = "width:100%"
    ,tags$div( style = "background-color:red;"
     ,"Note: Date range currently limited to one year, but there is a fairly easy workaround
      for the next version."
    )
    ,tags$div(
      style = "display:inline-block; width: 25%;float:left;"
      ,"Mutual Fund Symbol", tags$input( id = "mfsymbol" )
      ,tags$br()
      ,"Start Date "
      , tags$span( style="font-size:75%;fill:lightgray", "(2013-08-29)" )
      , tags$input( type = "date", id = "stdate" )
      ,tags$br()
      ,"End Date"
      ,tags$span( style="font-size:75%;fill:lightgray", "(2014-08-29)" )
      , tags$input( type = "date", id= "enddate" )
      ,tags$br()
      ,tags$input(
        type="submit", id = "calc", value = "Calculate"
      )
      ,tags$br()
    )
    , tags$div(style = "display:inline-block;height:100%;width:60%;margin-left:30px"
      , tags$textarea(id = "results", style="width:100%; height:150px")
    )
  )
  ,tags$script(sprintf(
'
  var french = %s;
' 
  , toJSON(data.frame("Date"=index(f),f)) %>>% HTML
  ))
  ,tags$script(
'
    function calculateEkholm( data ) { // data in form of x,y or fund-rf, mkt-rf
       /* get an error with regression.js
 var myReg = regression(
 "linear",
 data
 )
 */

         // so use the great simple-statistics library
       var myReg = ss.linear_regression().data(data);

       //get residuals
       var resid = data.map(function(p){return myReg.line()(p[0]) - p[1]});

       //regress residuals^2 on (mkt-rf)^2
       var myReg2 = ss.linear_regression().data(
         data.map(function(d,i){
           return [ Math.pow(d[0],2), Math.pow(resid[i],2) ]
         })
       )
       //coefficients ^ 1/2 will give us ActiveAlpha and ActiveBeta
       var activeAlpha = Math.pow( myReg2.b(), 0.5 );
       var activeBeta = Math.pow( myReg2.m(), 0.5 );

       //now do the next step to get ActiveShare and SelectionShare
       var selectionShare = Math.pow(activeAlpha, 2 ) / ( ss.variance(data.map(function(d){return d[1]})) * (data.length - 1) / data.length )
       var timingShare = Math.pow(activeBeta, 2 ) * ss.mean( data.map(function(d){return Math.pow(d[0],2)}) ) / ( ss.variance(data.map(function(d){return d[1]})) * (data.length - 1) / data.length )

       //pass correlation result also
       var correlation = ss.sample_correlation(data.map(function(d){return d[0]}),data.map(function(d){return d[1]}));

       return { 
         regression: myReg,
         correlation: correlation,
         activeAlpha: activeAlpha,
         activeBeta: activeBeta,
         selectionShare: selectionShare,
         timingShare: timingShare
       }
    }

  // thanks https://gist.github.com/fincluster/6145995
   function getStock(opts, type, complete) {
        var defs = {
            desc: false,
            baseURL: "http://query.yahooapis.com/v1/public/yql?q=",
            query: {
                quotes: \'select * from yahoo.finance.quotes where symbol = \"{stock}\" | sort(field=\"{sortBy}\", descending=\"{desc}\")\',
                historicaldata: \'select * from yahoo.finance.historicaldata where symbol = \"{stock}\" and startDate = \"{startDate}\" and endDate = \"{endDate}\"\'
            },
            suffixURL: {
                quotes: "&env=store://datatables.org/alltableswithkeys&format=json&callback=?",
                historicaldata: "&env=store://datatables.org/alltableswithkeys&format=json"
            }
        };

        opts = opts || {};

        if (!opts.stock) {
            complete("No stock defined");
            return;
        }

        var query = defs.query[type]
          .replace("{stock}", opts.stock)
          .replace("{sortBy}", defs.sortBy)
          .replace("{desc}", defs.desc)
          .replace("{startDate}", opts.startDate)
          .replace("{endDate}", opts.endDate)

        var url = defs.baseURL + query + (defs.suffixURL[type] || "");

        return url;
    }

    d3.select("#calc").on("click",function(){
      calculateFund(
        d3.select("#mfsymbol")[0][0].value,
        d3.select("#stdate")[0][0].value,
        d3.select("#enddate")[0][0].value
      )
    })

    function calculateFund( symbol, startdate, enddate ) {

      d3.json(getStock({stock:symbol.toUpperCase(),startDate:startdate,endDate:enddate},"historicaldata"), function(e1,fund){

          if( e1 || !fund.query.results ) {
            updateResults ( {e1:e1, e2:e2, queryresults: "query problems"} );
          } else {
            var fund_factor = [];

            //manipulate data to join fund with factors
            //would be nice to have a xts merge in javascript

            // query.results.quote will have the data stripped of meta
            // also we will sort date ascending
            fund = fund.query.results.quote
                .sort(function(a,b){
                  return d3.ascending(
                    d3.time.format("%Y-%m-%d").parse(a.Date),
                    d3.time.format("%Y-%m-%d").parse(b.Date)
                  )
                } );

            // now lets go period by period with fund.map
            fund.map( function(per, i){
              if( i > 0 ) {
                var frenchThisPer = french.filter(function(d){return d.Date == per.Date})[0];
                fund_factor.push([
                  //Date: per.Date,
                  //FundPrice: 
                  per.Adj_Close / fund[ i - 1 ].Adj_Close - 1 - frenchThisPer["RF"],
                  //Rm_Rf:
                  +frenchThisPer["Mkt.RF"],
                  //Rf: +frenchThisPer["RF"]/100
                ])
              }
            })

            updateResults( calculateEkholm( fund_factor ) );
          }

      })
    }

    function updateResults( ekholmCalc ){
      var ekhArr = [];
      Object.keys(ekholmCalc).map(function(k){
        ekhArr.push( [ k,": ", ekholmCalc[k] ].join("") )
      })
      d3.select("#results").text(ekhArr.join("\\n"))
    }
 ' %>>% HTML )
) %>>%
  attachDependencies(
    list(
      htmlDependency(
        name="d3"
        ,version="3.4"
        ,src=c("href"="http://d3js.org/")
        ,script="d3.v3.min.js"
      )
      ,htmlDependency(
        name="simple_statistics"
        ,version="0.1"
        ,src=c("href"=
           "http://timelyportfolio.github.io/rCharts_factor_analytics/js"
        )
        ,script = "simple_statistics.js"
      )
    )
  ) %>>% html_print
```