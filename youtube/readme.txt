
Functional Requirements:
------------------------
1)Able to upload video
2)Able to search video
3)Watch video
4)live streaming of video
5)Feed generation
5)Recommendations

Non functional
--------------------
1)High availability:
------------------
Multi region and multi AZ deployment of storage services improves high availbilty of video data.
When watching a video or live streaming any server down is not goodSo we need to maintain high avaiblity
2)Durability and persistance(SQl and object storage)
-----------------
videos uploaded should be durabale and stored in a persistant storage for future .

3)Consistency
-------------------
strong consustency:(QL spanner)
when video uploaded ,it should be reflected immediately in channel 
Eventual consistency:
-------------------
When video made as public or uploaded newly ,no need to reflect immediately for others in their search query.
Reviews ,comments,likes count,views count not immediately relflect to others.
Latency:
------------------
when video should load immediately(CDN cache)
Scalablity:
-----------------
Every year the video base growing by 1billion.So system should give same performance (geo based sharding).
Fault tolerance:
-----------------


Capacity estimation:
---------------------

2billion DAU 
Each user watches at least 10 videos per day.
20billion videos/day = 200k videos/sec

upload : view = 1:100

upload rate = 2k videos/sec

storage capcity
---------------
Youtube sypports multiple resolutions like 1080 ,2160,4xxx,720,320,144,480
A user uploaded 20 mins of video in 480 rate consumes - 1GB of memory

2160   - 4GB
1080  - 2GB
480    - 1GB
320    - 0.5
144    - 0.25
-------------
8GB = total

2000*8GB = 16TB /sec
replication factor for durability = 3 AZs = 48TB/sec

why video chunks?
for ABR

How to identify the nearest local CDN ?
1. User request:
When a user requests a video on YouTube, their request is sent to a DNS server. 
2. Anycast routing:
The DNS server identifies the geographically closest CDN PoP based on the user's IP address and directs the request to that server. 
3. Content delivery:
The selected CDN server then serves the video content to the user from its cache, minimizing the distance data needs to travel. 










