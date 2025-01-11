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

Background thread(Deamon thread) collects it.

push vs pull

If we push the data points , need to implement retry on all sources(causes redundancy) in case issue from collection service.
If collection service pulls ,retry burden shifted to collection service.

What if collection service failed to get after retry attempts?
A)inform support team as mail to fix the source

So push model is best.


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


Statistical nalysis : sales trends
analoly detection : fraud detection like spikes,drops
clustering : customer segmentation
prediction : future forecasting
optimization : dynamic price adjustments
time series decompation : seasonal trends
correlation : ads spend vs sales







