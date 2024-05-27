<!--yml

category: 未分类

date: 2024-05-18 05:55:23

-->

# Vertx Work Queue Playing | Tales from a Trading Desk

> 来源：[`mdavey.wordpress.com/2014/01/04/vertx-work-queue-playing/#0001-01-01`](https://mdavey.wordpress.com/2014/01/04/vertx-work-queue-playing/#0001-01-01)

## Vertx Work Queue Playing

Got board late one night, so thought I’d muck around with Vertx [mod-work-queue](https://github.com/vert-x/mod-work-queue).  The runmod feature of Vertx is nice, and avoids the madness of having to find [modules](http://mvnrepository.com/artifact/io.vertx) on the web:

> vertx runmod io.vertx~mod-work-queue~2.0.0-final

Best is to pass some conf params 🙂 and also run in cluster mode:

> {
> 
> “address”: “trading.test”
> 
> }
> 
> vertx runmod io.vertx~mod-work-queue~2.0.0-final -conf mod-work-queue.conf -cluster matt

Which gives me a cluster running work-queue on a default address:

> Starting clustering…
> 
> No cluster-host specified so using address 192.168.0.3

So now to my processor code.  Due to the lateness of the hour, I got stuck on how the [acceptedReplyAddress](https://github.com/vert-x/mod-work-queue) should work:

```

var vertx = require('vertx');
var eventBus = require('vertx/event_bus');
var console = require('vertx/console');
var container = require('vertx/container');

console.log('Trading Verticle has been started');

vertx.eventBus.send("trading.test.register", {
"processor": "processor1"
}, function(reply) {
if (reply && reply.status === "ok") {
console.log('Processor1 Registered for trading');
}
});

vertx.eventBus.registerHandler("processor1", function(message, replier) {
console.log('Process trading work ' + JSON.stringify(message));

var msg = message.message;
console.log('Message was ' + msg);

// Send the reply
replier({});
});

var myHandler = function(message) {
console.log('Received ack');
}

vertx.eventBus.registerHandler('test.acceptedReplyAddress', myHandler);

eventBus.send('trading.test', {
accepted_reply: "test.acceptedReplyAddress",
message: 'FIX <35>'});

```

~ by mdavey on January 4, 2014.

Posted in [未分类](https://mdavey.wordpress.com/category/uncategorized/)
