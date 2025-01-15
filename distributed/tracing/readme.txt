Need to build DAG of calls called trace
Each call is span
show the trace in web interface
what is the permitted  sampling?
0.1% (traces are captured out of the total number of requests within a system)
span 
   startTIme
   endTime

=================================================
capacity estimation
---------------------
Assume 1000 services
1 service runs on 100 machines
1 machine gets 100 RPS

How many QPS per service?

1 service can give 10k queries per second

How many spans are captured per service?

10K * (0.1) = 100 spans/sec

100k/sec spans for all services

How many spans per 1 year retention period?

100k * 24*60*60*365= 100k*31 million = 31*10^5*10^6

3000billion spans/year needs

How many characters in spanId?

18 characyers in spanId

(26+9)^9 is sufficient for 3k billion spans
but take double = 18 characters

How much data per span?

2 timestamps(8 bytes,unix epoch)
18 characters(8 bytes each)
-----
200 bytes approx.

request+reponse data = 2kb
10 logs messages = 10*200=2kb

5 kb per span

How much data for app spans?

3*10^12*5*10^3

15PB of storage

Distributed tracing problems
 
1)Linking between spans across service
   As the functionality is pread across multiple machines and services,calling service should send the trace context to caller service to maintain the parent-child link.
A)Proppagation of  context(spanId and traceId) across service bounaries
2)Need to capture network latency anf network failure

3)Span loss:
    network failure:
    spans may not preoperly received or sent beacuse of network failures.SO implement retry 
    service failure:
           If a service failied before sending the span,implement fallback mechanisms
    

4)Trace reconstruction for end - end flow analysis:
   As spans are spread acrosos multiple machines,
A)span aggreagation

5)storage problem due to huuge span volume
  In single node , only 4 spans per trace example

100 RPS - 100*4 = 400 spans

4 services generates extra 3 service call spans 

total 4+3 = 7 spans per request
100*7 = 700 spans now

span count increases exponentially dow to distributed nature.s
A)apply samping(only a portion of spans are collected for latency analysis)

consitency

6)clock drift 

horizontal scaling:
7)when a new instance spins or old instance dead, need to do auto service registry and de registry with tracing service
A)service discvoery
2)

spanSchema
-----------
traceId
spanId
parentSpanid:
operationName:validateToken()
serviceId : ABC
startTimestamp
endTimestamp:
tags:
{
http.method:GET
http.url : /users/profile
http.status: 200
errorMesssage:
}




Queries
TraceLookup queries:
-------------------

1)Query by trace id:
------------------
select * from traces where traceId = "12345"

2)Query all traces by service name by time range:
--------------------
select * from traces where serviceId = "CPG" where startTimestanp >= 2025-02-12 9:00:12 and endTimestamp <= 2025-02-12 10:00:00;

Query all traces by service name by time range with error code = 500:
---------------
3)select * from traces where httpStatus = 500 and serviceId = "SAD" where startTimestanp >= 2025-02-12 9:00:12 and endTimestamp <= 2025-02-12 10:00:00;


Latency analysis
--------------

measure the avg,min,max latrncy of requests by specific service
seelct AVG(duration) from spans where serviceName = "CXS" and 
}

end - end latency
select sum(duration) from spans where spans where traceId = "adad"

latency threshold

select * from traces where MAX(duration) > 500


sampling

1)Fixed sampling
2)Random sampling
3)Adaptive
4)Tail

Fixed means fixed value irrespective or anything
Tail:
    After request completion, the decision is taken for every trace
          latrncy > 500 (want to analyze slow transactions oly)
          erros like 5xx(particular error request only)

Adaptive:
    traffic : sampling decreases(at peak hours decreases,low traffic sampling increases)
    latency : sampling increases
    error rate : sampling increases
Depends on system metrics so integration with metrics system is required








 

