 
> Problem Statement : 
```
Design a HLD class diagram of a Comedy Cafe , that hosts Events and brings in Stand up Comedian .
Send Mails to Users to notify about the Event and Jokes . 
Keep tack of the popularity of the Stand up Comedian based on the clicks by the Users.
```



<!-- ROADMAP -->

## Roadmap

- [x] Cafe gets top 20 and 5 Random Comedians based on their popularity .
- [X] Cafe gets the Event information about these Comedians. 
- [x] Send info to the message Queue . Message Queue sends the mail to the users with the help of mailBox . 
- [X] User get the mail . He/She clicks on the Comedians . A response is sent to the MailBox . MailBox then sends the resonse to the Cafe.
- [X] Cafe updates the popularity of respective Comedians.
- [X] Comedian sends the joke to the Cafe. Cafe Extracts the joke and sends it to the USers who clicked on the resp. profile of comedian .
- [X] Cafe handles the branches information and Events information. 



>APIs Needed 
```
getListOfUsers()
get_top_comedians(count = 20) --> top20comedians:list
get_random_comedians(count = 5) --> 5RandomComedians:list
sendMail_To_ListOfUsers(user_list, top25comedians + 5RandomComedians )

extract_JokefromEmail(contect) --> joke : str 
get_liked_
sendJoke_to_users

GetListOfBranches()
GetListOfEvents()
GetListOfEventsByCity(CityId)
GetEventsByLocationandCity(CityId, LocationId)
GetShowTiming(eventid, locationid)
GetAvailableSeats(eventid, locationid, showtimeid)

```
>Server : Comedy_Cafe

```
This Comedy_Cafe will do many things like
[X] Sending mails to users
[X] Track of Branches , Comedians , Events
[X] All events inforamtion
[X] Sending mails to users
[X] Sending mails to users

> load balancing.
There will be multiple app servers for load balancing . A Consistent hashing will be used for load balancing. 
Load balancing.  is used to keep the system highly concurrent when we are scaling the app server horizontally. 
We also need to scale these app servers horizontally to take the heavy load and to handle a lot of requests in parallel.  

Tech : Django (Used for large scale apps , Handles multiple request concurrently , Django has a user authentication system , Admin page to handle data)
Front End : ReactJS or BootStrapJS 
```

> Caching
```
Tech : Redis Cache
To save the information related to the events, ticket price, etc, we need to use caching.
We can use Memcache or Redis for caching to save all the information about Events , Comedians information .
Redis is open-source and it can be also used for the locking mechanism to block the tickets temporarily for a user.
It means when a user is trying to book the ticket Redis will block the tickets with a specific TTL. 
```

> Elastic Search
```
Elastic search is used to support the search APIs on Comedy Cafe website (to search cafe branch and standup Comedians and Events). 
Elastic search is distributed and it has RESTful search APIs available in the system.
It can be also used as an analytics engine that works as an App-level search engine to answer all the search queries from the front-end. 
```
### NoSQL Tables
```
Tech = MongoDB (contains Data as a dictionary ) 
It offers high speed/performance
There will be no relationship between these tables. 
1. Events ( fetch using a event_id ) 
  Contains information about Events .  
  Event_id
  Ticket price ,
  schedule(date , time) . 
  Total tickets available . 
  Duration
  Location 
  Branch
 
2. Address (fetch using address_id = (branch_id)
  Contains address of different Cafe Branche's .  
  address_id
  full_address
  Pincode
  City 
  Nearby
  Capacity : total capacity of branch
 
3. User_information(fetch using user_id or comedian_id)
  user_id
  First_name
  Last_name
  Ph_no
  Address
  Gender
  Preference : List
  DOB
```
### SQL Tables
```
Tech = MySQL (Relational DBMS)
Stores data in a structured format using rows and columns
Pk = Primary Key
FK = Foreign Kay

1. Comedy Cafe (As per probem statement there is only one Cafe having multiple branches)
  Cafe_id : PK
  Name
  Star_rating
  total_users
  
2. Branch
  branch_id : PK
  Cafe_id : FK
  address_id : (This will be used to connect to Mongo DB for more info)
  manager_id
  branch_email
  
 3. Comedians 
  comedian_id : PK  (fetch details from User_information of MongoDb )
  name
  email
  ph_no
  popularity
  
 4.Users (Customers)
  user_id : PK
  name
  email
  ph_no
  
 5. user_likes ( As there is a many to many relation b/w user and comedian )
  user_id : PK (fetch details from User_information of MongoDb )
  comedian_id : FK
  date_of_like : (To keep track of past 1 month)
 
 6. Comedian_branch ( As there is a many to many relation b/w user and Branch )
   branch_id
   comedian_id
   data_and_time : Timestampz (Comedian will be here on that date and time)
 
many to many relation b/w user and comedian
many to many relation b/w Branch and comedian
one to one relation b/w Branch and Cafe

> Note: The server 1st fetches the key from the SQL dB then interacts with Mongo DB , for faster fetch . And returns the information . This way faster read and write can be done.


```

>Async Workers
```
The main task of the Async worker is to execute the tasks such as generating the pdf or png of the images for booked tickets and sending the notification to the users. 
For push notifications, SMS notifications, or emails we need to call third-party APIs. These are network IO and it adds a lot of latency. 
Also, these time-consuming tasks can not be executed synchronously. 
To solve this problem, as soon as the app server confirms the sending of mails, it will send the message to the message queue, a free worker will pick up the task, 
execute it asynchronously and provide the SMS notification, other notifications, or email to the users.
RabbitMQ or Kafka can be used for Message Queueing System and Python celery can be used for workers.

 RabbitMQ or Kafka can be used for Message Queueing System and Python celery can be used for workers.
  1. Python celery can be used for workers : These workers will fetch respective information parallely about the 20 top comedians and 5 random comedians from the database .
  
  2. Message Queueing System : To keep track of all the Emails being sent from the Cafe to users . And then also sending jokes about comedians.
  RabbitMQ will run your tasks asynchronously . WIthout waiting for acknowlwdgement go for next message.
  This will use gmail or any mainlimg sysstem, to send mails .
```

<!-- ROADMAP -->



