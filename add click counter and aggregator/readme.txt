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


