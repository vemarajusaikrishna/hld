Functional Requirements;

1)Viewers can add comments to live vide
2)Viewers can see the comments in near rel time
3)Vievers can see the old comments at the time of initial join.

out of scope
-------------
Vievers can reply on the comments
vievers can react to the commnets.


Core Entities:
-------------

Comment
User
Video


API


create comment
POST /comment/{videoId}

Get all comments

GET  /comments/{videoId}?cursor=<last_comment_Id>&direction=<after/before>&pageSize=50

cases:
-----
When the user scroll the page up
GET  /comments/{videoId}?cursor=<last_comment_Id>&direction=before&pageSize=50
When the user scroll the page dow
GET  /comments/{videoId}?cursor=<last_comment_Id>&direction=after&pageSize=50




