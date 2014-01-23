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

To check the server status:
```
sbin/rabbitmq-ctl status
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

There are 4 types of exchanges: direct, fanout, topic, and headers (stay away from due to performance).

By default, queues and exchanges are not persistent.  You must set the "durable" flag to True for them to be persistent AND set the "delivery mode" to 2 (Need to see what this constant really means or is aliased to).  But persistent exchanges/queues have a performance hit.

When you publish msgs to an exchange, each msg on the channel gets a unique id.  IDs start with 1.  The Producer must keep track of the numbers as they are NOT returned with the basic_publish command.

Instead of persistent exchanges/queues, the Producer should use "confirms" to guarantee delivery to RabbitMQ.
```
channel.confirm_delivery()  #to put the channel in confirm mode
```

