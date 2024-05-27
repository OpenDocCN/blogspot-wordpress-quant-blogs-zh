<!--yml

类别：未分类

日期：2024 年 05 月 18 日 05:48:31

-->

# Camel in a Vertx Web Application | 交易台的故事

> 来源：[`mdavey.wordpress.com/2014/06/26/camel-in-a-vertx-web-application/#0001-01-01`](https://mdavey.wordpress.com/2014/06/26/camel-in-a-vertx-web-application/#0001-01-01)

将有趣的技术混合起来进行 PoC（概念验证）可能总是有趣的。在过去的一段时间里，我对 Apache Camel 的兴趣增加了很多。当我意识到有一个 Camel Vertx 组件，并且有时间打开 IntelliJ 时，我想我会构建一个快速而简单的应用程序，用于查看如何使用 Apache Camel 进行上游集成工作流程，以及使用 websocket 用于下游浏览器。尽管代码有点粗糙，但希望它能提供一些思路。

开始使用 Vertx 最简单的方法可能是使用 Maven [生成](http://vertx.io/maven_dev.html) 一个项目。

[Smartjava](http://www.smartjava.org/)、Pretech 和 hasCode 提供了一些有趣的文章来帮助：

+   使用 vert.x 2.0、RxJava 和 mongoDB 创建一个简单的 RESTful [服务](http://www.smartjava.org/content/create-simpe-restful-service-vertx-20-rxjava-and-mongodb)

+   使用 Vert.x、Websockets 和 HTML5 进行浏览器间的 [通信](http://www.smartjava.org/content/browser-browser-communication-vertx-websockets-and-html5)

+   Apache Camel + ActiveMQ [示例](http://www.pretechsol.com/2013/08/apache-camel-activemq-exampe.html)

+   Spring JmsTemplate 和 MessageListener [示例](http://www.pretechsol.com/2013/12/spring-jmstemplate-and-messagelistener.html)

+   使用 Vert.x 和 Java 创建一个 Websocket 聊天 [应用程序](http://www.hascode.com/2013/11/creating-a-websocket-chat-application-with-vert-x-and-java/)

代码是“仓促”的。增强：

+   Camel [聚合](http://www.amazon.com/Apache-Camel-Developers-Cookbook-Cranton/dp/1782170308) 消息 - 示例用例可能是需要在用户 blotter 中查看来自多个交易库的消息

+   Camel 转换 - 将 Java 和 XML 转换为 JSON，因为上游集成系统很可能不会使用 JSON

+   [Famo.us](http://famo.us/) + [Angular.js](https://github.com/Famous/famous-angular) 以改进基本的用户界面

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

作者：mdavey，于 2014 年 6 月 26 日发布。

Posted in [数据](https://mdavey.wordpress.com/category/data/)，[Java](https://mdavey.wordpress.com/category/languages/java/)
