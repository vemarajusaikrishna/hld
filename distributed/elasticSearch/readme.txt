Elasric has five components

1)Index
2)Document
3)Mapping
4)Filed
5)Data type


Example

"properties":{
"title":{"type":"text"}, 
"description":{"type":"text"},
"publish_date":{"type":"date"},
"description":{"type":"text"},
"author":{"type":"keyword"},
"categories":{"type":"keyword"},
"price":{"type":"float"}
"reviews":{
"type":"nested",
 "properties":{
       "rating":{"type":float}
       "comment":{"type":"text"}     
 }


text:Can do full text search(partial match can give results)
keyword : (perfect match needed.So we need to make as dropdown on UI)
date:can do sorting or range quieries
integer or float: can do range quiries (price less than 13$) or sorting
}
}


APIS:

PUT /books/_Mapping

"properties":{
"title":{"type":"text"}, 
"description":{"type":"text"},
"publish_date":{"type":"date"},
"description":{"type":"text"},
"author":{"type":"keyword"},
"categories":{"type":"keyword"},
"price":{"type":"float"}
"reviews":{
"type":"nested",
 "properties":{
       "rating":{"type":float}
       "comment":{"type":"text"}     
 }

PUT /books/_doc

{
"title":"Learn python in 90 days", 
"description":"Can teach you python in 90 days"
"publish_date":"22-05-2022",
"author":"Sai Krishna",
"categories":["Education"],
"price":{"type":"float"}
"reviews":{
 "properties":{
       "rating":"3.5"
       "comment":"Excellent book"    
 }

How to handle concurrent updates on same doc?
Use optimistic locking ,version number

GET /books/search
1)search for books 
