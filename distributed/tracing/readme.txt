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



 

