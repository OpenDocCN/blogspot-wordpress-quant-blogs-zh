<!--yml
category: 未分类
date: 2024-05-18 05:48:31
-->

# Camel in a Vertx Web Application | Tales from a Trading Desk

> 来源：[https://mdavey.wordpress.com/2014/06/26/camel-in-a-vertx-web-application/#0001-01-01](https://mdavey.wordpress.com/2014/06/26/camel-in-a-vertx-web-application/#0001-01-01)

Mixing interesting technologies to PoC possible solution is always interesting.  I’ve become a lot more interested in Apache Camel over the last time period.  When I realised there was a Camel Vertx component, and had time to open IntelliJ, I thought I’d build a quick and dirty application to look at using Apache Camel from an up-stream integration workflow, and websocket’s for down-stream browsers.  Although the code is ropy, it hopefully provide some food for thought.

Easiest way to being with Vertx maybe to [generate](http://vertx.io/maven_dev.html) a project with Maven.

[Smartjava,](http://www.smartjava.org/) Pretech and hasCode provides a few interesting articles to assist:

*   Create a simpe RESTful [service](http://www.smartjava.org/content/create-simpe-restful-service-vertx-20-rxjava-and-mongodb) with vert.x 2.0, RxJava and mongoDB
*   Browser to browser [communication](http://www.smartjava.org/content/browser-browser-communication-vertx-websockets-and-html5) with Vert.x, websockets and HTML5
*   Apache Camel + ActiveMQ [Example](http://www.pretechsol.com/2013/08/apache-camel-activemq-exampe.html)
*   Spring JmsTemplate and MessageListener [Example](http://www.pretechsol.com/2013/12/spring-jmstemplate-and-messagelistener.html)
*   Creating a Websocket Chat [Application](http://www.hascode.com/2013/11/creating-a-websocket-chat-application-with-vert-x-and-java/) with Vert.x and Java

The code is “rushed”.  Enhancements:

*   Camel [aggregating](http://www.amazon.com/Apache-Camel-Developers-Cookbook-Cranton/dp/1782170308) of messages – example use case could possibly be messages from a number of trade repositories that need to be seen in a users blotter
*   Camel transformation – Java and XML to JSON, as the upstream integrated systems are most likely not going to be JSON’d
*   [Famo.us](http://famo.us/) + [Angular.js](https://github.com/Famous/famous-angular) to improve the basic UI

```
package com.mycompany;

import org.apache.activemq.ActiveMQConnection;
import org.apache.activemq.ActiveMQConnectionFactory;
import org.apache.camel.CamelContext;
import org.apache.camel.builder.RouteBuilder;
import org.apache.camel.component.jms.JmsComponent;
import org.apache.camel.impl.DefaultCamelContext;
import org.apache.commons.io.FileUtils;
import org.vertx.java.core.Handler;
import org.vertx.java.core.eventbus.EventBus;
import org.vertx.java.core.eventbus.Message;
import org.vertx.java.core.http.HttpServer;
import org.vertx.java.core.http.HttpServerRequest;
import org.vertx.java.core.http.RouteMatcher;
import org.vertx.java.core.json.JsonArray;
import org.vertx.java.core.json.JsonObject;
import org.vertx.java.platform.Verticle;

import javax.jms.*;
import java.io.File;
import java.io.IOException;

public class CamelWebVerticle extends Verticle {
    final ConnectionFactory connectionFactory = new ActiveMQConnectionFactory("admin", "admin", ActiveMQConnection.DEFAULT_BROKER_URL);

    public void start() {
        createCamelRouting();
        createActiveMQConsumer();

        final HttpServer httpServer = vertx.createHttpServer();
        final RouteMatcher routeMatcher = createURLRouteMatcher();
        httpServer.requestHandler(routeMatcher);

        final JsonObject config = new JsonObject().putString("prefix", "/eventbus");
        final JsonArray inboundPermitted = new JsonArray();
        inboundPermitted.add(new JsonObject().putString("address", "msg.client"));

        final JsonArray outboundPermitted = new JsonArray();
        outboundPermitted.add(new JsonObject().putString("address", "msg.server"));
        outboundPermitted.add(new JsonObject().putString("address", "msg.client"));

        vertx.createSockJSServer(httpServer).bridge(config, inboundPermitted, outboundPermitted);
        setupEventBusListener();

        httpServer.listen(8888, "localhost");
        container.logger().info("Webserver started, listening on port: 8888");
        container.logger().info("Verticle started");
    }

    private void setupEventBusListener() {
        final EventBus eb = vertx.eventBus();

        // Register Handler 1
        eb.registerLocalHandler("msg.client", new Handler<Message<JsonObject>>() {
            @Override
            public void handle(Message<JsonObject> message) {
                container.logger().info("Handler 1 (Local) received: "
                        + message.body().toString());
            }

        });

        // Register Handler 2
        eb.registerHandler("msg.client", new Handler<Message<JsonObject>>() {
            @Override
            public void handle(Message<JsonObject> message) {
                container.logger().info("Handler 2 (Shared) received: "
                        + message.body().toString());
            }

        });

        eb.registerHandler("blotter.updates", new Handler<Message<String>>() {
            @Override
            public void handle(Message<String> message) {
                container.logger().info("Sent back data");
                message.reply("Data Ack!");
            }
        });

    }

    private void createActiveMQConsumer() {
        try {
            final Connection connection = connectionFactory.createConnection();
            connection.start();
            // Create a Session
            final Session session = connection.createSession(false, Session.AUTO_ACKNOWLEDGE);
            // Create the destination
            final Destination destination = session.createQueue("testMQDestination");
            // Create a MessageProducer from the Session to the Queue
            final MessageConsumer consumer = session.createConsumer(destination);
            consumer.setMessageListener(new MessageListener() {
                @Override
                public void onMessage(final javax.jms.Message message) {
                    System.out.println("Received " + message.toString());

                    if (message instanceof TextMessage) {
                        final  TextMessage textMessage = (TextMessage) message;
                        // Send update to web client via eventbus
                        vertx.eventBus().send("msg.server", new JsonObject().putString("text", "Async message via ActiveMQ from OMS confirmed order submitted"));
                    }
                }
            });
        } catch (Exception e) {
            System.out.println(e);
        }
    }

    private void createCamelRouting() {
        try {
            final CamelContext context = new DefaultCamelContext();
            context.addComponent("test-jms", JmsComponent.jmsComponentAutoAcknowledge(connectionFactory));
            context.addRoutes(new RouteBuilder() {
                public void configure() {
                    from("test-jms:queue:testMQ").to("test-jms:queue:testMQDestination");
                }
            });

            context.start();

        } catch (Exception e) {
            System.out.println(e);
        }
    }

    private RouteMatcher createURLRouteMatcher() {
        final RouteMatcher routeMatcher = new RouteMatcher();
        routeMatcher.get("/getBlotterSOW", new Handler<HttpServerRequest>() {
            public void handle(final HttpServerRequest req) {

                final JsonObject resp = new JsonObject();
                resp.putString("text", "SOW from DB of trades");

                req.response().headers().add("Content-Type", "application/json; charset=utf-8");
                req.response().end(resp.toString());

                vertx.eventBus().send("msg.server", new JsonObject().putString("text", "Blotter SOW snapshot"));
            }
        });

        routeMatcher.get("/", new Handler<HttpServerRequest>() {
            public void handle(final HttpServerRequest req) {
                final File f = new File("src/main/resources/web/index.html");
                System.out.println(f.getAbsolutePath());
                try {
                    // get the data from the filesystem and output to response
                    String data = FileUtils.readFileToString(f);
                    req.response().setStatusCode(200);
                    req.response().putHeader("Content-Length", Integer.toString(data.length()));
                    req.response().write(data);
                    req.response().end();
                } catch (IOException e) {
                    // assume file not found, so send 404
                    req.response().setStatusCode(404);
                    req.response().end();
                }
            }
        });

        routeMatcher.get("/submitOrder", new Handler<HttpServerRequest>() {
            public void handle(final HttpServerRequest req) {
                try {
                    // Create a Connection
                    final Connection connection = connectionFactory.createConnection();
                    connection.start();
                    // Create a Session
                    final Session session = connection.createSession(false, Session.AUTO_ACKNOWLEDGE);
                    // Create the destination
                    final Destination destination = session.createQueue("testMQ");
                    // Create a MessageProducer from the Session to the Queue
                    final MessageProducer producer = session.createProducer(destination);
                    producer.setDeliveryMode(DeliveryMode.NON_PERSISTENT);
                    // Create a messages
                    final TextMessage message = session.createTextMessage("New Order from a client");
                    producer.send(message);
                    session.close();
                    connection.close();
                    System.out.println("Message sent to ActiveMQ");

                    final JsonObject resp = new JsonObject();
                    resp.putString("text", "order sent");
                    req.response().headers().add("Content-Type", "application/json; charset=utf-8");
                    req.response().end(resp.toString());
                } catch (Exception e) {
                    System.out.println(e);
                    e.printStackTrace();
                }
            }
        });

        routeMatcher.noMatch(new Handler<HttpServerRequest>() {
            public void handle(final HttpServerRequest req) {
                final File f = new File("src/main/resources/web/"+req.path());
                System.out.println(f.getAbsolutePath());
                try {
                    // get the data from the filesystem and output to response
                    String data = FileUtils.readFileToString(f);
                    req.response().setStatusCode(200);
                    req.response().putHeader("Content-Length",Integer.toString(data.length()));
                    req.response().write(data);
                    req.response().end();
                } catch (IOException e) {
                    // assume file not found, so send 404
                    req.response().setStatusCode(404);
                    req.response().end();
                }
            }
        });

        return routeMatcher;
    }
}

```

```
<html>
<head>
    <title>ActiveMQ Vertx Camel Web PoC</title>
</head>

<body>

<form onsubmit="return false;">
    <input type="button" id="connectButton" value="Open connection"/>
</form>

<div id="submitForm">
    <form onsubmit="return false;">
        Message:<input type="text" id="sendMessage" value="Equity Order"/>
        <input type="radio" name="submissionType" value="publish"> Publish
        <input type="radio" name="submissionType" value="send" checked> Send
        <input type="button" id="submitButton" value="Submit"/>
        <br>
        <br>
        <input type="button" id="submitOrder" value="Order"/>
        <input type="button" id="getBlotterSOW" value="Blotter SOW"/>
    </form>
</div>

<br>
<br>
<br>

Messages received on browser handler:<br>
<hr>
<div id="received" class="innerbox" style="width: 400px; height: 275px;">
</div>

<script src="js/jquery-1.7.1.min.js"></script>
<script src="js/sockjs-0.2.1.min.js"></script>
<script src="js/vertxbus.js"></script>
<script>
		var eb = null;
		var addressName = 'msg.server';
		var addressClientName = 'msg.client';

		function submitMessage(type, address,  message) {
			if (eb) {
				var json = {text: message};
				if (type == 'send') {
					eb.send(addressClientName, {text: 'Send message: ' + message});
				} else {
					eb.publish(addressClientName, {text: 'Publish message: ' + message});
				}
			}
		}

		function browserHandler(msg, replyTo) {
			$('#received').append(msg.text + "<br>");
		}

		function subscribe(address) {
			if (eb) {
				eb.registerHandler(address, browserHandler);
				$('#subscribed').append($("<code>").text("Address:" + address));
				$('#subscribed').append($("</code><br>"));
			}
		}

		function unsubscribe(address) {
			if (eb) {
				eb.unregisterHandler(address, browserHandler);
			}
		}

	  	function closeConn() {
			if (eb) {
				eb.close();
			}
			$('#connectButton').val("Open Connection");
			$("#connectButton").on('click.openConnection', function() {
				openConn();
			});
		}

	  	function openConn() {
	  	  	eb = new vertx.EventBus("http://localhost:8888/eventbus");

	  	  	eb.onclose = function() {
				eb = null;
				$('#submitForm').hide();
			};

			eb.onopen = function() {
				$('#connectButton').val('Close Connection');
				$("#connectButton").off('click.openConnection');
				$('#connectButton').on('click.closeConnection', function() {
					$("#connectButton").off('click.closeConnection');
					closeConn();
				});

				$('#submitForm').show();
                subscribe(addressName);

			};
		}

		$(document).ready(function() {
			$('#submitForm').hide();

			$("#submitButton").click(function() {
				submitMessage($("input[@name=submissionType]:checked").val(), addressName, $("#sendMessage").val());
			});

			$("#submitOrder").click(function() {
                $.ajax({
                        type: "GET",
                        url: "submitOrder",
                        data: "",
                        success: function(data) {
                            browserHandler(data);
                        }
                    });
		    });

			$("#getBlotterSOW").click(function() {
                $.ajax({
                        type: "GET",
                        url: "getBlotterSOW",
                        data: "",
                        success: function(data) {
                            browserHandler(data);
                        }
                    });
		    });

            closeConn();
        });
	</script>

</body>
</html>

```

~ by mdavey on June 26, 2014.

Posted in [Data](https://mdavey.wordpress.com/category/data/), [Java](https://mdavey.wordpress.com/category/languages/java/)