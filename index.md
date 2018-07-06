# User Scenario - The Characters
### 	Who is your target user?

We believe our primary user base to be of two categories,

- The everyday commuter, who makes use of a particular route on a daily basis in order to notify the user of any events on their way, the traffic conditions and provide an alternate route if available, thereby helping them to not only save time by avoiding a certain route but also provide an alternate route to reach their destination.

- The tourist, who is not aware of any events in and around the city. Tourists usually have their whole trip planned, they have plans for each and every day of their trip and even the slightest disturbance to the plan due to traffic along their route because of a music concert or a big sports event can damper their whole day and eventually the trip altogether. If notified of the traffic and information about the event ahead, we believe our application can be a major help in making a tourist’s time in Dublin hassle free.

That being said, the application is not limited to the mentioned type of users, but can be used generally by anyone who wishes to be notified about any events along their route

### 	Why are they important?

The target users, as mentioned 
- are the everyday men and women who are the workforce of this city. We believe in making their daily commute a bit easier and tension free so that they can concentrate solely on their work and not worrying about getting to work or coming back home.

- are the people who come to Dublin to enjoy and experience the beautiful city it is. We believe in making their time here as beautiful as possible so that they can enjoy the city as they wish and not worry about unnecessary traffic they might have avoided with prior notification.


### 	What problem are you solving for them?

Traffic is a major issue in Dublin, here are a few news articles on the effect of traffic that also served as a great motivating factor for our project.

![Traffic1]( nhriday.github.io/1.png )

“On average, commuters said they spent approximately 43 minutes each way on their daily commute to Dublin city. Over a year, this averages out to 14 days behind the wheel and some say the proposed changes could add 10 days to the existing total”

![Traffic2](nhriday.github.io/2.png)

“A new survey says Almost three quarters of companies in Dublin have seen the negative effects of congestion on their business increase over the past three months. Dublin Chamber shows that 73% of its members said traffic problems in Dublin have had an increasingly negative impact on their business since the start of December.”

![Traffic3](nhriday.github.io/3.png)

“Time lost due to aggravated traffic congestion in the greater Dublin area is costing the economy €350 million per year with the amount set to rise to €2 billion by 2033. The Department of Transport’s Economic and Financial Evaluation Unit has undertaken a research project to estimate the cost of aggravated congestion across Ireland’s transport system.”

![Traffic4](nhriday.github.io/4.png)

“A new index of world cities has revealed that Dublin is the "slowest-moving" major city in the world when it comes to traffic congestion. The report by Bank of America Merrill Lynch found that during congested periods in the capital, the average driver reaches a speed of 7.5km/h, with peak hour speeds of 5.5km/h - slower than a horse and cart.”

![Traffic5](nhriday.github.io/5.png)

The report says, “Traffic heading into and out of certain parts of Dublin city is an absolute nightmare and unfortunately, it's going to get a lot worse as traffic is set to increase by 50,000 journeys a day in the next nine years, according to the Department of Transport.”
The primary problem of our target users we aim to solve is that of avoiding unnecessary traffic. Usually, most daily commuters may use an application that provides them the route to their destination and also frequent commuters who are well versed with the route may not use any application at all. The problem with both these approaches are neither of them are aware of any events along their route which might have led to a high traffic scenario which eventually may result in the user stuck in traffic and getting late to work, getting home or simply put, reaching their destination. Our application helps them avoid this by notifying them about any events along their way, details about the event such as capacity and an estimation of the number of vehicles, start time and probable end time of the event, and most importantly an alternate if available so that they can reach their destination.



# Technical Problem: The Setting 

### 	Why does your system exist? 

When we first set out to develop this application, we had two reference points. Ticketmaster and Google Maps. Ticketmaster is a website that sells tickets for almost every event in Ireland, specifically Dublin as we are building a database that consists of events in Dublin. Google Maps is an application used by almost everyone to reach their destination and its use ranges right from taking a walk to planning a trip. We believe our system exists as an effective culmination of the best features of the two applications

### 	What is the core technical problem? 
We have developed a web API using flask which runs on the localhost of the server (provided by UCD). The problem with this is, it is not available on the public domain and we cannot access it in the application. We are facing a few minor issues with hosting it on the public domain and should be able to overcome it for the Mid-Term presentation


### 	Can you review other existing systems or products that address this problem? 
As our application is basically a route providing service or a map application, the best reference point for us was Google Maps. It is available to the public domain and can be utilized effectively. We plan to emulate the service provided by Google Maps in our own unique perspective

# Technical Solution: The Plot 
![ProcessFlow]( nhriday.github.io/process.JPG )

![Open](https://github.com/nhriday/nhriday.github.io/blob/master/Open.gif)



**Client - Server**
The very first step is the user entering the source and destination of the commute planned. This is done on our Android client to set the two parameters. This request is sent to our back-end server, where the server interacts with the Google direction API to obtain the geo-locations of the locations requested from the client. Using these geo-locations, a route to the preferred destination is displayed on the screen. The server communicates with a back-end database to collect information on events relevant to the route on which the user plans to commute and sends it back to the serve as a response. The server sends all this information, routes and event information back to the client

**Database**

We have a database which consists of the following information of the events: - 
*	Event title & Venue
*	Start time, End time (estimated)
*	Capacity of the venue

 
### Technology

**Front-end:**
  * Android - Our front-end client is written in Android, which is an interface to help the user navigate through the application. 
 
 * Maps SDK - SDK used to manage access to Google Maps server and display the map layout in our client (application)
 
 * Google Places API - API used to get automated suggestions from Google Maps when a user types in the name of a location. It also helps in obtaining the geo-locations of the searched location
 
 * AwesomeSplash - used to create a custom splash screen, the screen that pops up when the app icon is clicked on. A library developed by Viktor Arsovski and is available at https://github.com/ViksaaSkool/AwesomeSplash 

**Back-end:** 
  * Flask Server
   – handle the requests from the client and call the Google Maps API for relevant information regarding routes and return the event details by accessing the database depending on the request, which is the date and time entered by the user or system time by default and the route information returned from the Google Maps API

  * mySQL database
   – stores all structured event data including venue, start time, title, capacity primarily

  *	Data: What data resources are you going to use and how will you access, collect, and store them?
Ticketmaster API using python and store relevant data in the database

# Evaluation: The Reviews

**What does success look like for your system?**

A user enters a preferred source and destination using our application, in 
return the following is available on the display -:
-	A route to the destination
-	Event markers along the route
-	Notifications to the user about the traffic conditions
-	Event info including title, time details, capacity of the venue
-	Traffic conditions close to the start/end time of the event
-	Alternate route(s) if available
This would be a successful system

**How will you evaluate the system that you built?**

We plan on evaluating our system during a live large-scale event at which we believe our system can be evaluated thoroughly. The event we have planned to evaluate our system at is a cricket match between India and Ireland at the Malahide Cricket Club Ground in Dublin

# Conclusion: The Plan

**Project management strategy**

We are following the Agile project management strategy. We are following a system where we have two-week sprints. Each of us have a specific task assigned and the scrum master (Mehul Singh) is the buffer for any type of information exchange. The following illustration represents the process flow

![Sprint]( nhriday.github.io/sprints.JPG )

In addition to the above sprints, we discuss the progress and issues at least every two days over text messaging or Skype. At the end of each week, all of us make sure we meet face to face at UCD mostly to discuss the progress and get ready for the next sprint. Initially we divided ourselves into two teams of 2 and 3 to work on front-end and back-end development respectively. After the second sprint, the whole team took on the responsibility of writing the report and readying the presentation. All 5 of us met at the end of the second sprint and gave inputs on what each of them worked on and came up with the report and the presentation.

**Biggest challenges**

The challenge we believe is obtaining the accurate routes in order for the commuter to be able to use it effectively. Google Maps Direction API for Android does not provide routes and navigation information. We cannot get the routes by calling the Google Maps on the phone, only the Maps JavaScript API provides the routes.

We plan to overcome it by sending the geolocation data from the Google Places API to the server to make API calls instead of making HttpConnections to call the API by the client. This helps us to send back the exact route data back to the client by drawing polylines on the map. Obtaining the geo-locations also helps us to provide alternate routes.

**Roadmap**

![Roadmap]( nhriday.github.io/roadmap.JPG )

# Resources
•	List of resources (software, papers, tutorials, books, stats, business indicators)
-	Github
-	https://github.com/ViksaaSkool/AwesomeSplash
-	https://pages.github.com
-	http://flask.pocoo.org/docs/1.0
-	https://www.tutorialspoint.com/flask
-	https://blog.miguelgrinberg.com/post/designing-a-restful-api-with-python-and-flask
-	https://developer.ticketmaster.com/
-	https://developers.google.com/maps/documentation/
-	Android Studio
-	Jupyter Notebook
-	Youtube
-	Google
-	Stack Overflow
