Functional Requirements

Publish messages : A producer able to publish a message to queue
Consume message:Aconsumer should able to consume a message.
Queueing : Messages should be able to queueing of messages to handle high concurrency
Routing: messages should be routed to correct consumer
Acknowledgement:Consumer able to acknowlwdge the message delivery to prevent message loss or confirm delivery
Message Delivery:should follow semantics like at least once , at most once delivery,exactly once
Message Failure : retry the message delivery
Message recovery: Use WAL file for message recovery.
Ordering:Priorty,FIFO


Non functional requirements

Scalability:System should scale horizontally incase of load increase
High availblity: All queue should be highly available
latency:
fault tolerance: Consumer should be able to consume even though if queue goes down.
Re processing:If consumer goes down the messages should be re processed from last message.
Durability: messages should be durable

Capcity estimation:

10 million messages/day
10 million/100000
100 messages / sec

What is the retention policy?
30 days

each message 10KB
100kb*10^6=1000gb=1TB
30TB of storage is required


SQL   : write heavy , ACID for transactions, fixed schema
No SQL: read heavy , eventual consistency,horizontal scalable
WAL   : extreme fast writes , durability,offsets for each message,extreme througput,used for recovery of partition.


Configuration storage
1)Queue ->consumer groups-one - many
2)ConsumerGroups - consumer - one - many
3)Persmission-consumer one - one
4)Authentication-
Base properties:name,descrition
Capacity and data management:
size  of queue,limit exceed,retention policies
Access control : permissions, authentication
So use SQL for configuration 


State 
use sql

NoSQL-use for message write

But before writing to noSQL ,use WAL
WAL uses append only log from which data stores to DB

Each partion uses its own WAL file if it recovers for message pulling





fault tolerance:partioning

single point of failure
not high ly avaible

subset of data









