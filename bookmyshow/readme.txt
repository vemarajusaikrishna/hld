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



API
---

Theater API:

GET /api/v1/theaters/{theaterId}
POST /api/v1/theaters/
DELETE /api/v1/theaters/{theaterId}
PATCH /api/v1/theaters/{theaterId}

Screen API

GET /api/v1/theaters/{theaterId}/screens/{screenId}
POST /api/v1/theaters/{theaterId}/screens
DELETE /api/v1/theaters/{theaterId}screens/{screenId}
PATCH /api/v1/theaters/{theaterId}screens/{screenId}

Seat API

GET /api/v1/theaters/{theaterId}/screens/{screenId}/seat/{seatId}
POST /api/v1/theaters/{theaterId}/screens/{screenId}/seat
DELETE /api/v1/theaters/{theaterId}screens/{screenId}/seat/{seatId}


Movie

GET     /api/v1/movies/{movieId}
POST    /api/v1/movies
DELETE  /api/v1/movies/{movieId}
PATCH   /api/v1/movies/{movieId}

Booking API

POST /api/v1/reserve
GET /api/v1/reserve/{bookinId}
GET /api/v1/reserve/{userId}
GET /api/v1/reserve/{theaterId}
DELETE /api/v1/reserve/{bookinId}
PATCH  /api/v1/eserve/{bookingId}

Payment API

POST /api/v1/payment
GET  /api/v1/payment/{paymentId}
POST /api/v1/payment/{paymentId}/refund/
DELETE /api/v1/payment/{paymentId}/refund/{refundId}


Search API

GET /api/search/v1/movies?region=AHD   -get list of movies in a city
GET /api/search/v1/movies?region = AHD&language=english&genres=crime&format=3D&latitude=12.1313131&longitude=12.2121313 - apply filters

Notification API

POST /api/notify/v1/


ER

Theater - screen one -many
screen - shows one -many
movie - show one - many
screen - show one - many

user - booking one - many
booking-seat - many - many same seat can be booked in different bookings from different shows
booking-payment - one-one


Theater

id
name
description
openingTime
closingTime
address

Screen
id
theaterId
size
name

Seat
id
screenId
number
row
class

Show
id
screenId
movieId
startTime
endTime

Movie
id
name
title
genere
language
duration
releaseDate
cast
crew

Booking

bookingId
bookedBy
bookedOn
lastUpdatedOn
lastupdatedBy
status
showId
paymentId




bookedSeats

showId
seatId
bookingId
status




 





















