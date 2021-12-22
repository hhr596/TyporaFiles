I'll do a brief introduction to the mechanism of the DIAMOND system.

It is simple, we use cameras to collect information about vehicles and the drivers inside. And we use prefounded databases to identify the driver to see if he/she is qualified for driving and to send the penalty messages to the person if he/she had violated the speed limit.

So what if we don't have any information about the driver in a prefounded database. Well, that's when the ANPR facilities come in handy. The ANPR refers to Automatic Number Plate Recognition, they are basically cameras as well, but with special algorithms programmed. The ANPR facilities can be installed at gas stations, on a police car, or at a fixed spot on the road. These cameras scan car plates at every single second, and bundle its scanning results with GPS locations when sending them to the server. So literally this generates an auxiliary database that helps us to locate a car so we can send policemen on scene to check the unindenfied driver.

Well, that's how it works!

So we can now take a look at the structure of the system. It could be really comprehensive.

So we have a Local Server to manage the speed&photo cameras, and an ANPR server to manage the ANPR network. The Proxy Server here is as an essential security agency. Every online data transmission needs to go through this server, It hides both the IP addresses from the server that sends the request and the server that receives the data. So to make the online communications much more reliable. 

On top of that, we have the central processing server, every dicision will be made through this server. Such as: Is the car out of speed? What information can we find in the databases about this driver? Or, Who shall we send the messages to afterwards? It's like a CPU to a computer.

At last, we have the destination server, which is set at the office who sends the penaly notice to the driver. And this happens when we successfully identified the driver with our databases.

If the driver is unidentifiable, then the message goes to the Local Office Server, to tell them that there may be an invalid driver on the road!





Since we understand that the system is mostly running automatically 24/7,  we need triggers that motivate the system to operate, in this case, by triggers I mean the key events that initiates a series of actions.

In the diamond system, we have two triggers, which are the two Parallelograms here at the top left corner.

We start from collecting data on the road, and we send them to the Central Processing Server to determine if the vehicle is out of speed. If we find it violates the speed law, then we're going to identify the driver with the detected face photos in our databases. 

We have two periods in the search process.

First, to see if the driver is in an official database, which is one of the DVLA (Driver and Vehicle licensing Agency), IPS (Idendity and Passport Service), and HomeOffice databases. Second, if he/she is not in the official database, then we will try to use the ANPR database we built to find the vehicle's current location so we can send policemen to check the driver.

Once the driver is identifed, the alert will go directly to the destination Office, if not, it goes to the Local Office.

And every records generated or results received are kept and updated in our ANPR database.