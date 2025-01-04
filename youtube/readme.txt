
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

------------------------------------------------------
Upload process
----------------
1)User send a upload request to upload server
2)upload server the persist the upload url.
3)Upload server return presigned url of s3 to user.
4)User goes to s3 and performs multipart upload.
5)If upload completes , user sends acknowledgement to upload server
6)upload service change the status from pending to complete.


Videometadata:-

videoId
title
description
createdBy
createdOn
duration
language
locationUrl
status : pending/completed
why video chunks?
for ABR
---------------------------------------------------------------------------

How to identify the nearest local CDN ?
1. User request:
When a user requests a video on YouTube, their request is sent to a DNS server. 
2. Anycast routing:
The DNS server identifies the geographically closest CDN PoP based on the user's IP address and directs the request to that server. 
3. Content delivery:
The selected CDN server then serves the video content to the user from its cache, minimizing the distance data needs to travel. 


How to decreaes latency in video delivery?
Initial Upload: When a video is uploaded to YouTube, it is first processed and stored in a central data center.

Replication to Regional Data Centers: YouTube proactively replicates content to regional data centers and cache locations, often before users in those regions explicitly request the video. This preemptive approach helps improve the delivery speed and reduces latency for viewers.

Caching for Popular Content: For videos that gain popularity or are expected to be popular (like trending videos), YouTube may push those videos to multiple cache locations in advance. This ensures that when users in different regions request the video, it can be delivered quickly without needing to retrieve it from the original data center.

On-Demand Caching: For less popular or niche content, videos may initially be stored only in the central data center. If a user requests such content from a specific region, YouTube will then cache it in the nearest data center. This on-demand approach helps optimize storage and bandwidth usage.










