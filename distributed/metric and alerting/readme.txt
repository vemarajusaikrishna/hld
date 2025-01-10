Metrics and alarms
--------------------


1)Collect the metrics from clients
2)Show data on the metrics in realtime
3)page the on call engineer when certain rules about the metrics are et


---------
Non functional requirements

1)Highly scalable 
2)durable
3)consistency
4)
-----------

capacity estination


1billion data points  collected

1million/sec


-------------
componenets

1)source
2)data collection
3)data transmission
4)data storage
5)query service
6)Data analysis
7)visualization
8)Alerting on data
-------------

How to collect the data points from source?

Background thread(Deamon thread runs)

push vs pull

If we push the data points , need to implement retry on all sources(causes redundancy) in case issue from collection service.
If collection service pulls ,retry burden shifted to collection service.

What if collection service failed to get after retry attempts?
A)inform support team as mail to fix the source



