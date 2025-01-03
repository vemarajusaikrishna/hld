Inventory management


Funtinal requirements
--------------------
Able to add/delete/update/get products/inventory items in catalog
sync with all ecommerce platformsn in rela time.
Notify customer about inventory status
provide options to support reorder points

Non functional requiements
-------------------------
Highly available
Durable
consistency
scalablilty
As the business grows , the new proucts added,system should give ame performance 

-----------

ead TPS and write TPS

Amazon has 300M active accounts 
200M are prime accounts

There are 3B visits which involves 10 pages per visit in  month.

QPS
----

30 B - 1 month

1B/day
10000 QPS


TPS
300M items ordered in 2 days on prime days.
150M/day
1500 TPS

-----



Notifications will be sent in 4 scenarios
1)Low stock :- If stock falls below threshold point.
2)Out of stock:if stock is reached to zero.
3)Restocking:periodic notifications for replenishment:


Solutiion:

periodc monitoring:
real time monitoring


APIs
---------
Product APIs


POST /api/v1/products

GET  /api/v1/products/{productId}
GET  /api/v1/products/
PATCH  /api/v1/products/
DELETE /api/v1/products/{productId}


Inventory APIs

POST /api/v1/products/{productId}/inventory/
GET  /api/v1/products/{productId}/inventory/{inventoryId}
PATCH  /api/v1/products/{productId}/inventory/{inventoryId}
DELETE /api/v1/products/{productId}/{productId}/inventory/{inventoryId}




Supplier API:-


Warehouse API:-


order API:-


ER Diagram
-----------















