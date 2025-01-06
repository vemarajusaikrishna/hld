Notification service

1)What type of notification do you want to support?

Promotional 
      product launches,deals ,discounts
user-triggered
      order confiramtions,success payment,failed payment,order ancelled
System alerts
      server down
Event based
      calender events,upcomming appointments,remainders
security 
      login attempts,password changes
Transactional
      subscription renewables,cancelled,uprade
      payment dues,payment remainders

what are the delivery channels you want to support?

SMS
Push
EmaIL
WhatsApp
FACEBOOK

DO you want to support bulk noifications?

Scenarios:
1)When celebrity posts a photo,send notifications to all followers.
2)When user A likes user B post,send notification to user B.
3)When user A comment of the post of user B , send notifcation to user B.

-------------------------

Capacity estimation:












----------------------------

Preferences schema

Categories 

categoryId
name
isActive
createdOn
updatedeOn

Deliver channels

channelId
name
createdOn
updatedOn

category - channel - one - many

CategoryChannels
id
categoryId  
channelId
createdOn
updatedOn
UNIQUE(categoryId,cannelId)- toprevent duplicates


User

userId
username
language
email
phoneNumber
dob
timeZOne


Preferences

preferenceId
userId
categoryId
channelId
isEnabled
frequency(relTIme,daily,weekly,digest)
doNotDisurb_start
donotDisturbEnd
createdOn
updatedOn
(userId,categoryId,channeld) UNIQUE - to prevent duplicated preferences


notificationLog

notificatinId
userId
categoryId
channelId
sentAt
createdOn


ratelimiter

id
scopeId
scopeType(USER,channel,category,global)
tier(normal,premium)
window(HOURLY,DAILY,WEEKLY)
limit


1  null user          normal 10 dailiy
2  123  category      normal 1   daily
3  124  channel       all   100  minute
---------------

Notificationpriorty

Security:OTP,securityBreach,legal updates,complaince issue(time sensitive) -> high prioty
Transactional , user triggered -> medimpriorty
promotional -> low prioruty

Eaxh priortyone topic is created.

Notiifcations that require
AtLeast once-> retry done until limit.Failure after limit exceed keep in dead letter queue ,implement idmpotency to handle duplicates
Exactly once->Use idempotency key , to ensume message delivered exctly once
Atmost once->no retry,no further action in case failed delivery







