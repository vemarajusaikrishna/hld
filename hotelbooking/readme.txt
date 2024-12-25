BookMyshow


1)User should be able to get Cities to which the bookMyshow affiliated.
2)After user selects,system should fetch list of movies relased in that city
3)Now,user should be able to filter the results based on genere, language etc 
4)User should be able to sort the results based on release date etc
5)After user clicks on the movie,system should display all the details of the movie
6)After user clicks on proceed,system should retrieve all the theaters,screens ,and schedules of movie.
7)After user selects a show,it should fetch seating arrangemts
8)User  selects list of seats , system should direct the user to payment page
9)After payment success,user get payment,booking notifcations.

Admin 

Create /update/delete/get theaters
Create /update/delete/get screen info
Create/update/delete/get seat pricing
show schedule change
Create/delete bookings based on bookingId
fetch booking by userId,bookingId,theaterId
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

5000 screens all over the world
1 screen - 4 shows daily
1 screen - 200 seats

20000 shows - 4000000 seats

weekdays - 60% seats occupied
weekends - 90% seats occupied

average 80% seats filled per day = 3200000 seats

1 booking - atleast 2 seats
3200000/(2*86400) = 16 TPS

QPS = 100*TPS = 1600 QPS

storage estimation



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








 





















