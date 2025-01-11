icsMetrics and alarms
--------------------

3)What type of metrics do you want to collect?

4)want realtime streaming or batch of data points?

3)DO you want to build alerts based on rule voilations of any metrics?


---------
Non functional requirements

1)Highly scalable 
2)durable (keep the metrics data in multi AZ and multi region .so that they are durable)
3)consistency
4)metrics data should be persistance (use time series data store)
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

Background thread(Deamon thread) collects it.

push vs pull

If we push the data points , need to implement retry on all sources(causes redundancy) in case issue from collection service.
If collection service pulls ,retry burden shifted to collection service.

What if collection service failed to get after retry attempts?
A)inform support team as mail to fix the source


Q)what is the frequency of pushing data points?
A)Every 5 seonds as batch or realtime

Q)Where the metrics collected till 5 seonds stored?
A)In memory or cache

Q)If in memory, how to recover the metrics data collected till 4s if the server gort crashed after 4 seconds?
A)save in WAL file and read it after recovery

do reltime sedning of metrics to avoid crash problem,


Statistical analysis:

Mean median mode average vaiance
moving average
Example : Average order value for product
Usage : we can find the spending of a customer on that product and can decide for more marketing and discounts if orders are less than threshold.

Predictive:

2023 1000 units sale of a product
2024 2000 units sale of prodcut
2025  how much units?
These futuristic prediction keeps the inventory prediction

Clustering

grouping of  customers based on similar purchase behaviour.

customer A : 100 purchases,500 rs
B           : 150  , 750rs
C           : 10 , 12rs
D            : 50 , 23rs

(A,B) - high value customer
(C) -> low values customer
(D)-> medium

what is ue of knowing?

We can offer discounts for low value buting customer to attract.

Amaoly detection:
-----------------

sudden spikes in sales
sudden drop in sales

sudden spike in purchase value of product .check if it is correct ?

-----------------
correlation:
2 metrics are compared

customer acquanitance this year for product A
sales this year for procyt A

if(Customer acqua cost > sales) -> take some deicions

-------------------
optimization

maximize the profits and minimize the expenditure by adjusting price,inventory

Example
High demand for product but low stoc -> so increase the price

-------------------
Time series decomposition

Ex:Sales peek every november

Trend : sales growing every yaers
seasonality : regular sales spike during holiday season
noise : irregualr sales dips due to markt disruptions

to meet seasonal demands
to know market disruptions before

Redcommenations

colllaborative filtering
content basaed filtering
matrix factorzation

-----------------------------


Statistical nalysis : sales trends
analoly detection : fraud detection like spikes,drops to prevent losses
clustering : customer segmentation to offer more discounts to attraction
prediction : future forecasting -> be ready to match the demand
optimization : dynamic price adjustments -> 
time series decompation : seasonal trends 
correlation : ads spend vs sales -> comparaison


----------------------------
CPU percentage as example
Data cleaning:

    1)Drop the negative and null values
    2)Discard incomplete records
    3)reove duplicate entries
Data foramtting
  convert the timestamps to single standard foramt UTC or ISO
  convert the flaot value to percenqages
Data organising
  group similar metrics related to same server
  organize data by server or region etc
Data sorting




Db sharding
----------------
shard key :timestamp + matrixKey

what if use only matrix key?

A)The metrics are classififed into 2 types 
High frequency metrics 
low frequney metrics

Now metric is mapped to one shard always.

high frequency metrics perform more writes on one shard
low frequency metrics perform low writes on one shard

This leads to uneven write load distribution causes hotsopts and overutilized and underutilization of servers happens.

what if use only timestamp?

A)Lets take we write every second.
In one second 10 million metrics generated for all metric types 
One one shard only one million operations happens.
Next second may be another shard but every second only one shard.So at peak times we get 1 billion metrics ,this goes to one shard and breaks the shard.

Here write distribution itself not occurning .Atleast some distribution happening in above case.

So use timestamp + metrickey











