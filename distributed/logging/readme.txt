
Functional Requiremrnts:-
----------------------
1)Able to write the logs genrated from any serviced or machine
2)Able to read the logs 
3)What kind of log filter capability is required for visibility?
4)Do you want to get monitoring befits like (alerts and alarms) based on some specific exception?
Monitor log data for specific patterns or error messages, triggering alerts when predefined conditions are met
5)What is rentention period of log system?






Non functional Requirements
-------------------------
1)High availblity: infrastructure should up every time
2)consistency : eventual consistency (with some latency)
2)very minimal data loss: 
                 broker property(persistant broker no data loss and non persistnt broker has data loss)
                 consumer shoudl be (durable  or no)
                 backpressure because of spike in production rate 10X (agent installed with buffer and use log files)
                 
3)scalablity : do horizontal scaling if traffic spikes may be 10 times the normal
4)Low latency : When the data is logged in every server or application ,it should be availble for consumption with low latency.
5)Durable logging
6)Persistant logging

With the Persistent messages, broker will save messages to disk, but depends on what kind of subscribers it has, if no durable subscribers then with some implementations, messages are deleted once delivered.
a "durable subscriber" is a subscriber that retains its subscription even when disconnected from the broker, meaning it will receive any messages sent to the topic while it was offline when it reconnects, while a "non-durable subscriber" only receives messages when actively connected and loses any messages sent during its downtime
Published As	                   Nondurable Subscriber         	Durable Subscriber
NON_PERSISTENT	              1. Missed if inactive
                              2. Missed if broker failures	   1. Missed if broker failures
PERSISTENT	                  1. Missed if inactive
                              2. Missed if broker failures	Always Delivered

enter image description here

parquet files: Acolumnar file foramt used for efficient storage for long term storage doing batch processing , analytics queries to run;

Use cases

1)Column based compression for efficeint storage for long term storage
2)Batch processing: While working on historical data for trend analysis, makes faster tansformations and aggregations as it is in columnar foramt
3)Run analyhtics queries : optimize query perfromance;


Log data is used for historical analysis (always batch processing only monthly,weekly,yearly)


capacity planning
-----------------

assume generating 100 billion messages per day from thousands of servers

1 message = 200 bytes
100 * 10^9/10^5 seconds

1000k messages/sec = 1million/second

data capcity:
------------
100 * 10^9*200 bytes
20 TB of data every day


1 million messages/sec
20 TB per day
Factors that affect the number of brokers needed
Message size: The size of the messages being sent can affect the latency of Kafka. 
Ingress volume: The number of queries per second (QPS) can affect the latency of Kafka. 
Storage capacity: The amount of storage capacity available in the existing brokers can affect how many additional brokers are needed.(20000GB/1PB) = 20 brokers
Network capacity: The amount of network capacity available in the existing brokers can affect how many additional brokers are needed.

Problems

No replication 
-----------
broker failure - data loss
high back pressure - data loss

operability

broker replacement -> need to reboot all the depending services to pick up latest broker list.


Problemes:

Kafka enabled replication:

1)Cannot randomly pick kafka brokers to write
2)Always need to find the kafka broker where leader partion resides.

Replication:

cannot copy

backpressure reasons

1)consumer lag suddenly
2)high spike in production rate

consumer loag reason
1)Insuffienct cosumer capcity(consumer capcity <= partions in topic)
2)Slow processing

How to handle backpressure?

create the log files and install agent to read it at constant rate and send at constant rate to kafka.May be more log files generated at spike load.

Agent requirementds
-------------
reliable : always up and running 
minimum computation resource usage on server
supports various file formats text,etc
high throughput , low latency
fairness schedulinhg



advantages
------------
applications write to files
agent monitors the file and uploads logs to kafka

isolates application from agent failure
isolates applications from kafka failure


problems with syslog forwarding without agent
-------------------
spike push can leads to backpressure in kafka
kafka failure effects the sending application

production support
-------------
dynamic configuration updates detection
adjustable log uplading latency
auditing:to know the data log
heartbeat mechanism: to know the health status


compoenents of agent
----------
configuration deection
log file update event monitoring
log file reading
network transportation to kafka

> 100Mb/sec upload speed


