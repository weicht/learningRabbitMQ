learningRabbitMQ
================

I'm using RabbitMQ In Action to learn RabbitMQ:
```
http://manning.com/videla/
```

Download RabbitMQ and unzip it:
```
http://www.rabbitmq.com/install-standalone-mac.html
```  

I put the rabbitmq_server-3.2.2 folder in my /Applications folder.

Then symlink all the /Applications/rabbitmq_server-3.2.2/sbin/rabbit* executables into /usr/local/sbin/ (remember to sudo the ln -s commands)

Note: I chose /usr/local/sbin only because when I had previously tried installing RabbitMQ with homebrew, it put v3.2.1 in there.  So, I had to move that version out of the way and I decided to put the latest there as well.
```
lrwxr-xr-x  1 root         admin   58 Jan 25 19:15 rabbitmq-defaults@ -> /Applications/rabbitmq_server-3.2.2/sbin/rabbitmq-defaults
lrwxr-xr-x  1 root         admin   53 Jan 25 19:15 rabbitmq-env@ -> /Applications/rabbitmq_server-3.2.2/sbin/rabbitmq-env
lrwxr-xr-x  1 root         admin   57 Jan 25 19:16 rabbitmq-plugins@ -> /Applications/rabbitmq_server-3.2.2/sbin/rabbitmq-plugins
lrwxr-xr-x  1 root         admin   56 Jan 25 19:15 rabbitmq-server@ -> /Applications/rabbitmq_server-3.2.2/sbin/rabbitmq-server
lrwxr-xr-x  1 root         admin   54 Jan 25 19:17 rabbitmqadmin@ -> /Applications/rabbitmq_server-3.2.2/sbin/rabbitmqadmin
lrwxr-xr-x  1 root         admin   52 Jan 25 19:17 rabbitmqctl@ -> /Applications/rabbitmq_server-3.2.2/sbin/rabbitmqctl
```

Next I added /usr/local/sbin to my PATH within .bash_profile
```
PATH="./:/usr/local/bin:/usr/local/sbin:${PATH}"
export PATH
```

To Start the RabbitMQ server (should be in PATH):
```
rabbitmq-server
```

To check the server status (should be in PATH):
```
rabbitmq-ctl status
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





References
==========
http://www.rabbitmq.com/install-standalone-mac.html

https://github.com/rabbitinaction/sourcecode

