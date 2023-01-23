LLD solution of 
Problem Statement : 
Design a Comedy Cafe , that hosts Events and brings in Stand up Comedian .
Send Mails to Users to notify about the Event and Jokes . 
<!-- ROADMAP -->

Soution : 

## Classes of Comedy Cafe System:

>Comedy_cafe :
```
It manages all operations of Cafe and its branches . 
It is central part of organization for which software is being designed.
It handles sending all mails to users.
Comedians send there jokes to Cafe.
```
>Branch:
```
A cafe can have multiple branches.
A branch hosts events.
Comedians perform here.
```

>Address:
```
Address of a Cafe branch.
Capacity of the cafe .
```

>Comedians
```
Comedians class , contains information about the comedians like Name , Email , Popularity 
You can get all the events and there schedules from here . 
```

>EVENTS
```
Events information . Its Ticket price , its schedule(date , time) . Total tickets available . 
```


>MessageQueue
```
Called from Cafe , Comedians .
This holds all the email to be sent from the cafe . 
It will send the Email asynchronously.

```
>Message
```
Contains information about the email like send to , sent from , Content 
Connects with mailBox to send mail.

```

>Attachment
```
Attachement could be of type text , video , Image .
```

>User
```
Contains user name and email . And can login using mailBox 
It manages all operations of user like Clicking on Comedian .


```

>MailBox
```
This is a server used to send mail to others.
Can get all the emails of a User.
Delete emails , 
Send emails

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


