<!--yml
category: 未分类
date: 2024-05-12 19:41:32
-->

# RPC server | Coding the markets

> 来源：[https://etrading.wordpress.com/2008/08/18/rpc-server/#0001-01-01](https://etrading.wordpress.com/2008/08/18/rpc-server/#0001-01-01)

## RPC server

### August 18, 2008

Just finished the first cut of my RPC server, which is coded in Python. Client JavaScript code running in the browser subscribes to Liberator subjects, which invokes a subscription request in the RPC server. The server sends cached static data back up to the client on the Liberator subject. The data is sent as a serialized Python dictionary. So on the server side we can just apply str() to the Python dict. When the data arrives in the browser we can do a JavaScript eval() to turn it into a JavaScript object. Simple and flexible !