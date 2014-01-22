learningRabbitMQ
================

I'm using RabbitMQ In Action to learn RabbitMQ:
```
http://manning.com/videla/
```

Download RabbitMQ:
```
http://www.rabbitmq.com/install-standalone-mac.html
```  

Copy/move to wherever you want it to be installed.

To Start the RabbitMQ server:
```
sbin/rabbitmq-server
```

Concepts:

Producers create msgs and publish to an exchange (which gets routed to a queueu).

```
1. Establish a connection.
2. Open a channel.
3. Declare an exchange.
4. Create a msg.
5. Publish msg to exchange with a routing_key.
```

Consumers subscribe to a queue and recv msgs.

```
1. Establish a connection.
2. Open a channel.
3. Declare an exchange.
4. Declare a queue.
5. Bind the queue to the exchange with the routine_key.
6. Consume the msg(s).
```

