
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





