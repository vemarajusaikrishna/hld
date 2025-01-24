Add click counter and aggregator?

youtube videoclicks/instagram post clicks/add clicks/website clicks/app clicks

TO monitor their add performance and tune their add campaign

FUnctional Requirements
----------------------
Able to capture add click events
Able to query add click events

Non functional 
---------------
High availability
Eventual consistency
charge


Capcity estimation
------------------
1 million unique adds
1 billion clicks /day on all adds

100 bytes per click

what are the clicks per second?

1 billion/100k = 10,000/sec

How much bandwidth?

10,000*100 bytes

1000 kb
1 MB/sec

How much storage per 1 year?

1 billion * 365 days * 100 bytes

36500 MB
36.5 TB

problems:
gauranteed click capture\
A)use persistant durable message broker
backpressure
scale the parttions based on backpressure metric
noisy neighbour
consumer failure
concurrent clicks on same add
Idempotent clicks
DB scalability(shard key)
Trade off 
----------
real time(FLink but not exact sliding window aggregation with window time )/near real time(use micro batching with spark 1 minute granularity)/batch click aggregation(Load data into HDFS and uses map reduce with 10 minute granularity with exact count )


How much storage per 10 year?

365 PB

low latency analytical queries < 1s
  - use pre- aggreagated results with read optimized db
Scale the reads with 10k /sec
 - used horizontal scaling , shrarding of streams with appdIds
  sharding of DBs with shard keys
Fault tolerance:
 - enabled hprizontal scaling on services
 - created multi broker cluster of broker
 - enable retention period of 7 days for flink to re consume from las flushed offset for small windows and enable check pointing for larger windows
 - enable high availability for DB (reader and writer instance)
click data integrity:
 - use lambda architecture: 
       erroneous speed calculation layer uses exact slow processing layer to correct the erroneous calculations.

       
 



addId+timestamp=shard key


Here ordered delivery not required
need perssitant broker

kafka streams offer additional mechanisms to handle backpressure
contolliing the flow of data

consujer lag

message overflow heepns when production rate > cosumer rate



