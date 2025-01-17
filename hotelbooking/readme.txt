BookMyshow


1)User should be able to enter checkinDaete and checkOutdate location adults ,children
2)After user selects,system should fetch list of hotels 
3)Now,user should be able to filter the results based on filters like flexible checkIn,PaymentModes,price range,ratings,user ratings,amenities
4)User should be able to sort the results based on price ,rating
5)After user clicks on the hotel,system should display all the inventory(roomTypes) available of hotel
7)After user selects a roomType,it should fetch roomDetails and fill guest details and clicks proceed to payment
8)system should direct the user to payment page
9)After payment success,user get payment,booking notifcations.

Admin 

Create /update/delete/get Hotel
Create /update/delete/get Rooms
Create/update/delete/get  room pricing
Create/delete bookings based on bookingId
fetch booking by bookingId,userId,hotelId on a date basis
Track payment for a booking
manage refunds

Non functional requirements

latency:

Highly available :

seat arrangement ,payment service,booking service should be highly available
booking history functionality may not be highly available
review/comments may not be highly available.

Search service:






Capacity estimation
Total 100k hotels
1 hotel - 4 (standar,delux,ultra delux,suite) room types
1 room type - 10 rooms
1 room - 2 adults 1 child

total - 100k*4*10 = 4Million rooms
Assume weekdays - 60 % occuppancy
Assume weendends - 90% occupancy
Average - 75% occupancy

People book rooms for one night,2 night, 3 nights
take 2 nights

1)Request comes to booking service

2)update the inventory 
3)update the bokking


what happens if inventory update success and booking update fail?
revenue loss because the rooms are locked-owner loss

3)update the inventory 
2)update the booking?

what happens if booking update success and inventory update fail?
double bookings will occur .customer loss


2PC

3)update the inventory  prepare
2)update the booking?   prepare

3)update the inventory  commit
2)update the booking  commit

Now problem of partial transaction issue failed?

But if coordinator fails,no one send the commit message means single point of failure
records consistently stay in locked phase


So use consensus based algorithm(Paxos and raft)?
Raft is consensus based algorithm.
All participants should aware of the decision made by leader.So if leader fails , followers will continue the task

When a transaction comes to coordinator,leader nodes uses quoram based replication and commits if quoram sends the acknowledgement

2PC + consensus algorithm will solve the problem

but 2PC is blocing protocol,which effects system scalablity


Saga pattern
--------------
Saga patten is non blocking

orchestrator  choreography


explicit lock     implicit locking(db automatically locks  a table during update operation relase after comiton recird)

using separate code to get ad release locks 

2 ways Slect for update






















APIs

Theater API

POST /v1/theaters/
GET  /v1/theaters/{theaterId}
GET  /v1/theaters/
PUT  /v1/theaters/{theaterId}
DELETE /v1/theaters/{theaterId}



Screen API

POST /v1/theaters/{theaterId}/screens
GET  /v1/theaters/{theaterId}/screens/{screenId}
GET  /v1/theaters/{theaterId}/screens/
PUT  /v1/theaters/{theaterId}/screens/{screenId}
DELETE /v1/theaters/{theaterId}/screens/{screenId}

Seat API

POST /v1/theaters/{theaterId}/screens/{screenId}/seat
GET  /v1/theaters/{theaterId}/screens/{screenId}/seat/
DELETE /v1/theaters/{theaterId}/screens/{screenId}/seat/{seatId}

Booking API

POST /v1/book/
GET  /v1/book/{userId}?bookedDate=yyyyddmm
GET  /v1/book/{userId}
GET  /v1/book/{theaterId}-admin
GET  /v1/book

Payment API

POST /v1/payment/
GET  /v1/payment/{bookingId}
POST /v1/payment/{bookingId}/refund

Seat Management

POST  /v1/seat







Payment API


Notification API








 





















