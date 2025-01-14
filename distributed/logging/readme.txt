
Functional Requiremrnts:-
----------------------



Non functional Requirements
-------------------------
1)High availblity: infrastructure should up every time
2)Minimal data loss: through pipe line
3)scalanlity : do horizontal scaling if traffic spikes may be 10 times the normal
4)Low latency : When the data is logged in every server or application ,it should be availble for consumption with low latency


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

