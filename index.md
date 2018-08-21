# User Scenario - The Characters
### 	Who is your target user?

We believe our primary user base to be of two categories,

- The everyday commuter, who makes use of a particular route on a daily basis in order to notify the user of any events on their way, the traffic conditions and provide an alternate route if available, thereby helping them to not only save time by avoiding a certain route but also provide an alternate route to reach their destination.

- The tourist, who is not aware of any events in and around the city. Tourists usually have their whole trip planned, they have plans for each and every day of their trip and even the slightest disturbance to the plan due to traffic along their route because of a music concert or a big sports event can damper their whole day and eventually the trip altogether. If notified of the traffic and information about the event ahead, we believe our application can be a major help in making a tourist’s time in Dublin hassle free.

  A tourist can also make use of our Event feature, where all the events and related info on any particular day can be viewed by selecting the date and can redirect to Google Maps app if he/she wants to navigate to the event

That being said, the application is not limited to the mentioned type of users, but can be used generally by anyone who wishes to be notified about any events along their route



### 	Why are they important?

The target users, as mentioned 
- are the everyday men and women who are the workforce of this city. We believe in making their daily commute a bit easier and tension free so that they can concentrate solely on their work and not worrying about getting to work or coming back home.

- are the people who come to Dublin to enjoy and experience the beautiful city it is. We believe in making their time here as beautiful as possible so that they can enjoy the city as they wish and not worry about unnecessary traffic they might have avoided with prior notification.


### 	What problem are you solving for them?

Traffic is a major issue in Dublin, here are a few news articles on the effect of traffic that also served as a great motivating factor for our project.

![Traffic1]( nhriday.github.io/1.1.png )

“On average, commuters said they spent approximately 43 minutes each way on their daily commute to Dublin city. Over a year, this averages out to 14 days behind the wheel and some say the proposed changes could add 10 days to the existing total”

![Traffic2](nhriday.github.io/2.2.png)

“A new survey says Almost three quarters of companies in Dublin have seen the negative effects of congestion on their business increase over the past three months. Dublin Chamber shows that 73% of its members said traffic problems in Dublin have had an increasingly negative impact on their business since the start of December.”

![Traffic3](nhriday.github.io/3.3.png)

“Time lost due to aggravated traffic congestion in the greater Dublin area is costing the economy €350 million per year with the amount set to rise to €2 billion by 2033. The Department of Transport’s Economic and Financial Evaluation Unit has undertaken a research project to estimate the cost of aggravated congestion across Ireland’s transport system.”

![Traffic4](nhriday.github.io/4.4.png)

“A new index of world cities has revealed that Dublin is the "slowest-moving" major city in the world when it comes to traffic congestion. The report by Bank of America Merrill Lynch found that during congested periods in the capital, the average driver reaches a speed of 7.5km/h, with peak hour speeds of 5.5km/h - slower than a horse and cart.”

![Traffic5](nhriday.github.io/5.5.png)

The report says, “Traffic heading into and out of certain parts of Dublin city is an absolute nightmare and unfortunately, it's going to get a lot worse as traffic is set to increase by 50,000 journeys a day in the next nine years, according to the Department of Transport.”

The primary problem of our target users we aim to solve is that of avoiding unnecessary traffic. Usually, most daily commuters may use an application that provides them the route to their destination and also frequent commuters who are well versed with the route may not use any application at all. The problem with both these approaches are neither of them are aware of any events along their route which might have led to a high traffic scenario which eventually may result in the user stuck in traffic and getting late to work, getting home or simply put, reaching their destination. Our application helps them avoid this by notifying them about any events along their way and most importantly an alternate route if available so that they can reach their destination.



# Technical Problem: The Setting 

### 	Why does your system exist? 

When we first set out to develop this application, we had two reference points. Ticketmaster and Google Maps. Ticketmaster is a website that sells tickets for almost every event in Ireland, specifically Dublin as we are building a database that consists of events in Dublin. Google Maps is an application used by almost everyone to reach their destination and its use ranges right from taking a walk to planning a trip. We believe our system exists as an effective culmination of the best features of the two applications

### 	Challenges
  - **Estimate end time** – The Ticketmaster API does not give us the end time of the events, only the starting times. We estimated the end time of the events based on the type of event and historical data for the large venues

  - **Predict traffic with radius** – The primary logic behind notifying the user about the event and the traffic around it, is the route of the user being in a specific vicinity or area around the venue. We decided to define an estimated area around the event by calculating the radius for a specific distance. This was done with help of a website ‘www.freemaptools.com’. The website allows us to enter the geographical coordinates of the venue and also the required radius and then draws an area around the location. We plan to use this to estimate the radius and notify the user about the event and the traffic around it.

Along with the radius, we also came up with something known as Pre-start time – in the case of larger events, which is our primary target to predict traffic, the traffic will be higher or start to increase maybe an hour or two before the start of the event; and Post-end time – similarly, the traffic is high after an hour or two after the event has ended. 


  - **Accessing Flask through our client** – The web API written in flask to process requests from the server, is to be accessed by public ports which were not made available by UCD. In order to access it using the public internet we need access to the ports on the server. We communicated with IT services in solving this problem.
 
  - **Data Refresh** – The data from Ticketmaster API is unstructured and inconsistent. We encountered a lot of missing values including the capacity of the venue, end time and location of the venue. We carefully filled in the missing values by referring to other entries and historical data. 

 - **Locating venue along the route** – Locating the venue along the route is one of the primary objectives of the application. We accomplished this by calculating the distance between the geographical points of the venue and the points on the route to make sure it is as accurate as possible. The geolocations are obtained using Google Places API and subsequently used to calculate the distance. If the distance we calculated is inside the radius defined, we can infer that the venue is along the route the user is commuting on.

  - **Displaying Routes** – The routes on the application are displayed by accessing the Google Maps API. Initially, the API gave us a number of geo-points on the route we wanted. We connected those points using a straight line and displayed the route on the map. The glaring error here was that the routes were not following the corresponding road on the map. They were just a few straight lines combined together and displayed.

      As a solution to this challenge, we made use of a field in the API known as ‘Polyline’, which enabled us to display the precise route lines on the map. The field was encoded, we decoded it with the help of a library called ‘Interactive Polyline Encoder Utility’. Once we could access the polyline field, we extracted a greater number of route points on the map and used it to display the routes that follow the road accurately. 



### 	Can you review other existing systems or products that address this problem? 
  - **Google Maps** - Google Maps is a very effective navigation tool which notifies users about real time changes along the route. It also notifies the user of traffic ahead while commuting by displaying the intensity of traffic by different colors, red being the indication that traffic is high and also provides an alternate route(s). This does not give the user a clear idea of the traffic. We want to provide the user with an additional feature by notifying them about the traffic with information about why the traffic is high and an alternate route(s) if available. If the user is aware of a large-scale event ahead, say a music concert with about 10000 people. This helps the user get a clear idea of the situation and plan the commute accordingly. We plan to emulate the service provided by Google Maps in our own unique perspective
  
 - **AA Roadwatch** – A part of the Automotive Association (AA Ireland), this is another application that provides information on road blockages, constructions all over Ireland. This application is developed for Ireland and the information is detailed and in real-time all over the country. It provides traffic updates as well. Again, it does not consider the traffic due to any event along the route of the commuter. It provides real-time updates of disruptions in the city, but does not provide event (music concerts or sports events in general) details and alternate routes based on the traffic around an event.
 
  - **Citymapper** – Citymapper is a crowd sourced city transit navigation app which offers a range of options to use while commuting in a city. It includes a journey planner as well. For a source and destination entered, the app also provides information on any disruptions in the route in real-time. Disruptions can be anything from road blockages to traffic congestion. The app provides routes and suggestions on how to use public transport to the destination. It does not provide directions for a commuter using a car or a motorbike.  The application does have a lot of features that would be a wonderful addition with our app, but it does not provide a solution to the specific problem we aim to solve. Moreover, this application does not operate in Ireland.

  - **INRIX Traffic** – A crowd sourced application, which provides a comprehensive view of the traffic around the commuter in real-time and any events or incidents along the way. It also provides navigation to the destination. The user can also choose to view the events on the route. Compared to the AA Roadwatch app, the disruptions such as road blockages shown in the city were very few. No events were displayed in the city after choosing the event display function in the app, whereas there were events all over the city according to our app. The app is designed for major US cities and not consistent with information in Dublin. It also does not consider the traffic due to a disruption with the alternate routes it suggests.

    The biggest drawback with crowd sourced applications is that the incident reported can be faked by anyone to divert traffic. Reports of people reporting fake incidents to reroute traffic around their homes has been recorded. Two students faked a traffic jam and tricked the application to reroute traffic affecting thousands of commuters.

  


# Technical Solution: The Plot 

## **Technology Involved**

**What does the system do?**

![System](nhriday.github.io/system.png)


### **Front-end:**

   Our front-end client is written in Android. The functions developed in this client include Launch Screen, Authentication System, Map and Event Display, Communication with Flask server, and User instructions.
  
  **Launch screen** - The launch screen provides an elegant transition during the waiting time. Besides, all the system permissions needed are checked and requested in this phase. The screen will then navigate to the login page if permissions are granted. A library called AwesomeSplash on Github was used in this app. It provides a customizable animated launch screen. The app logo and name are displayed in the screen. 
   
   
  **Authentication system** - As building a custom authentication system is complex, Google Firebase is chosen as the authentication system. Firebase is a powerful platform for mobile application development. Its authentication system is not hard for deployment and fits well with the Android system. Our application supports login with Google account and just about any email address and password. With the email and password account entered, A verification email will be sent to the address. When user logins into their account, a request is sent to the Firebase platform for authentication. After a successful login, the basic user information including icon, user name, and account will be sent back to the client. Glide, a fast image loading framework for Android, is used to retrieve the user icon to avoid lags. All these user details are displayed on the top of the menu. There is a sign out button in the menu. The client will check for account status. If user has already signed out, the text on the button will change into sign in and navigate to the login page.
    
    
  **Map and Event display** - There are a map page and an event page in this client (app). The map page allows user to enter source and destination to check if there is any event happening along the route. The two search boxes have auto-complete function. As a location is typed in, the Google API Client will check with Google Places API which then returns five most appropriate places and displayed in the search box. Because Google Places API use the same database with Google Maps, there will be no confliction between these places. When one location is selected, the name will be displayed in the text box. Meanwhile, the geo-location is also retrieved from API and stored for communicating with the server. The current location of the device is obtained and used as the default source in the search box. A map is displayed beneath the search box. The map and some map tools use Google Maps API for Android. Besides, the marker for locating events, radius, polyline for showing route path are also provided by the API. A custom information window adapter is implemented for displaying details of the events. The information window will pop out after clicking the marker. By clicking the polyline, the estimated travel time will be shown using snackbar on the bottom of the screen.

   The event page is similar to the map page. A floating button is set on the bottom right corner of the page. After clicking this button, a date picker will come out to let the user select the day he or she wants to check. The events information is then returned from the server and displayed by the marker on the map. The radius of the event is also shown by adding a light blue circle around the event. 
    
  **Communication with Flask server** - When the post action in map or event page happens, a new thread is created for communicating with the server. This can avoid the main UI thread from getting stuck. When the communication is finished, this thread will join to the main thread again. For the communication, two utility classes are created for the route and event connection. During the communication, a HTTP connection is built to the web API URL. Data such as date, geo-location that needs to be passed to the server are sent as tokens in the URL. Data returns from the Flask server in Json format. The Json library in Java is used to decode the data and use in the map and event page. Moreover, the polyline returned from server is encoded. A library called 'Interactive Polyline Encoder Utility' in the google maps API is used to decode the polyline into a list of LatLng type geo-points to draw path on the map.
    
   **User instructions** - A brief instruction is implemented to help the user get a better understanding of the application. The instruction consists of three pages, an overview of the application, an introduction to the map page, and an introduction to the event page. A library called FancyWalkthrough on GitHub was used to build these pages.
    
   **UI design** - The overall user interface design of this client follows the Android material design guidelines. The interface uses navigation drawer layout as the overall layout. The drawer menu designs to be similar with original Android application like Google Play Store. The color and icon used in the client is also chosen from material design examples. 
    
    
### **Back-end:**
 
   **Data Sources - Ticketmaster API**

  Initially, we started with three data sources Ticketmaster, Eventbrite and Ticketleap. We progressed with Ticketmaster as the other two had a few issues detailed below: - 

  - Eventbrite - The Eventbrite API returned several fields like location.address, location.latitude, location.longitude which could be used to access the details of the events depending on the location but these fields did not return the appropriate data. 

 - Ticketleap - Ticketleap API was providing the historical data of the events. Some of the other sources did not provide API for the data extraction. Web scraping was inappropriate for these sources as the web pages had inconsistent and incomplete data.

 - Ticketmaster - Ticketmaster was the best available option out of the sources we shortlisted as it is the largest ticket selling platform for events and the API provided most of the details regarding the event details
 
 Some of the other sources did not provide API for the data extraction. Web scraping was inappropriate for these sources as the web pages had inconsistent and incomplete data.

 **Data Collection**
 
  TicketMaster API was chosen as the data source. Data was collected from the chosen API using Python. This process was implemented as a Python Notebook

  Each call to the API returned 20 events (page-wise). The API allowed maximum of 1000 event band-width; 50 calls (50 pages) to the API were allowed. The collected data was stored as a CSV file.
  
  •	There were some missing fields in each page like the geo-location of a particular venue, they had to be entered manually using google maps. The data was inconsistent 

  •	Geo-locations of venues were missing

  •	Information about some events are available on a partner site; the user is redirected to buy the tickets and event information is available on the partner site.  

  •	Basic information including event name, time, date was missing. This is mostly for the smaller events

  •	API does not give us the capacity and end-time of the event

  •	Event details of only 1000 events can be obtained

  •	Each page contains only 20 events

  •	Almost every page has one or the other information missing

  To make the application more efficient, we added the following fields to the data: -
  - **End-time** (depending on the category of the event. Ex: Music concerts would end around 10 in the night)
  
  - **Pre-start time and Post-end time** (pre and post times were calculated based on the capacity, geolocation of the venue, start time and end time)
  
  - **Capacity, Radius** - calculated using the following algorithm: 
  
  Capacity <= 1000 -> 100mts
  
  Capacity > 1000 and Capacity <= 2000 -> 200mts
  
  Capacity > 2000 and Capacity <= 5000 -> 300mts
  
  Capacity > 5000 and Capacity < 20000 -> 500mts
  
  Capacity > 20000 and Capacity <= 40000 -> 600mts 
  
  Capacity > 40000 and Capacity <= 50000 -> 700mts
  
  Capacity > 50000 -> 800mts
  
  Made use of [FreeMapTools](https://www.freemaptools.com/) to visualize the calculated radius around the venue. This was essential because in some cases we found out that the radius we defined were not able to cover the major roads. Due to the inconsistency in the data when the API is called, it is not possible to update the data on a daily basis and provide the user with the most recent update of events.  
  
 
 **Web Server and Database** – The server was provided by UCD IT services. We installed MySQL database on the server. The reason for choosing MySQL was its compatibility with Flask server and we had just finished an Intro to MySQL module in the previous semester and were well versed with it. 

  The flask server was hosted on a virtual environment created in the server and Python3 was used to run the code because the default Python2 did not support some of the packages used in the file.

We created and populated the database with the following 4 tables namely: 

- event (EventID, EventName, Date, PreStartTime, StartTime, EndTime, PostEndTime), 
- eventvenue (EventID, VenueID), 
- radius (VenueID, Radius), 
- venue (VenueID, VenueName, City, Country, Address, Geolocation, Capacity). 

We created a couple of views to simply complex queries.
   
 
 **Flask Server (Web API)** - handle the requests from the client and call the Google Maps API for relevant information regarding routes and return the event details by accessing the database depending on the request, which is the date and time entered by the user or system time by default and the route information returned from the Google Maps API. We built the web API using flask, using 3 different URL’s to get 3 distinct results that are relevant to the user. Two URL’s to display the routes and the event info on the map page and one to retrieve the event details on a particular day on the event page.

```**"https://maps.googleapis.com/maps/api/directions/json?origin= + source + "&destination=" + dest + "&alternatives=true&key=" + key**```

   The source and destination are passed from the android application. The google maps API is accessed and returns the polylines that were used to draw the primary and alternate routes on the map

```**/EventGPS-api/sql/result/<date>/<time>**```
  
   The date and time are passed from the android application. This url is used to access the database which returns the events on the given day and time. The distance between the venue and the route is calculated. If the distance is within the radius we defined, then the url returns the details of the event. (as the event is along the route).

```**/EventGPS-api/events/all/<date>**```

   The date (chosen by the user) is passed from the android application. This URL returns all the events on the particular day.
   
 
 **Integration (Hosting the web API on the web server):**

   We were not able to access the web API over the public internet as a few of the ports needed were blocked. We contacted UCD IT Services to access the public ports. After access to the ports were granted, we used port 443 (HTTPS port) to make web API available over the internet.



**The Process**

There are two things the user can do in the beginning, the first is the user entering the source and destination of the commute planned; the second is the user checking for all the events on the particular day. 

![P1](nhriday.github.io/Process1.JPG)

This request is sent to our back-end server, the client interacts with the server to get back the specific routes and event info to the user.

![P2](nhriday.github.io/Process2.JPG)

There is a process followed to get the routes, the server interacts with the Flask web API to do the same.

-	The flask web API interacts with two entities and returns back two web pages.

-	The first webpage is the routes specific to the user, by interacting with the Google direction API to obtain the polylines. Using these polylines and the routes to the preferred destination is displayed on the screen. Primary and alternate routes are displayed together on the screen.

-	The second webpage is the information about every event on the day, which is stored in the MySQL database. The web API interacts with the database to extract relevant data and sends it back to the client through the server.

![P3](nhriday.github.io/Process3.JPG)

The MySQL database stores data obtained by the Ticketmaster API to get the information about events including

•	Event title & Venue

•	Start time, End time (estimated)

•	The Capacity of the venue

![P4](nhriday.github.io/Process4.JPG)

### **App Walkthrough** ###

  -	**Start-up** – Click on the EventGPS app icon, the following screen is shown on the screen containing the app logo

![A1](nhriday.github.io/App1.JPG)

  -	**Login** – Can login using an existing account or add a new account
  
![Login](nhriday.github.io/login1.png)

  -	**Map Function** – this is the first page displayed when the app is opened, and can also be chosen from the sidebar
 
![A2](nhriday.github.io/App2.JPG)

  
 
Enter Source and Destination, the route is and the event along the route is displayed. The event is shown as a marker( ), the marker can be clicked upon to view the event details. The user will be notified whether there is an event along the route or not on the bottom of the page

**Example 1** 

1. *Source* – UCD 

2. *Destination* – Dublin Spire

3. *Result* – 1 Event(s) found along the route, Aviva Stadium

![A3](nhriday.github.io/App3.JPG)

**Example 2**

1. *Source* – My Location

2. *Destination* – UCD

3. *Result* – Currently no event

![A4](nhriday.github.io/App4.JPG)	

  - **Event Function** – Choose the ‘Event’ option from the sidebar and click on the event calendar button on the bottom right-hand side of the screen. The events of the day in real time are shown with markers and can be clicked upon to view the event details.
  
![A5](nhriday.github.io/App5.JPG)

 - **Help Page** - •	Help Page – Click on the ‘Help’ option from the sidebar. This page contains information that can help the user better understand how to use the application.
 
 ![Help](nhriday.github.io/help1.PNG)
 
 ![Help2](nhriday.github.io/help2.PNG)

# Evaluation

  The most efficient and proper way of evaluating an application such as ours, is to physically commute the routes suggested by the app and evaluate whether they are efficient as advertised. This would require a considerable amount of time and resources which we could not afford. If we could not physically evaluate the system, the next best thing would be to do it virtually. We felt we could use Google Maps app to evaluate the system. Using the Google Maps, we recorded the time delays, primary routes, alternate routes, travel distance. The same is elaborated below. 

**System components evaluated**

We started the evaluation phase with two components of the system in mind

-	**Efficiency of the radius defined** 

The radius defined around each venue is based on the capacity of the venue, larger the capacity, larger the radius. Larger the radius, larger the traffic around that particular venue during the event. We chose the radius as an important part of evaluating the system as a whole because notifying the user of the event along the preferred path entirely depends on the route being inside the radius defined for an event. The evaluating factor here is to check whether the radius defined is logical. Logical, in the sense that the high degree of traffic around the event is approximately, if not accurately is in fact inside the radius we have defined.

-	**Efficiency of the alternate routes suggested**
 	
The second integral part of our application is suggesting alternate routes to the user to avoid getting stuck in traffic. We chose to evaluate this as to make sure the alternate routes suggested are in fact useful to the commuters. The evaluating factor here is to check whether the alternate routes suggested are outside the defined radius as the routes being inside the radius of a venue defeats the purpose of this evaluation and the whole system as well. For a source and destination entered by the user, one primary and at least two alternate routes are given. The purpose of the alternate routes is to divert from the primary route thereby avoiding traffic on the primary route.

**How was the system evaluated?**

As mentioned above, we used Google Maps to evaluate the two components. The process involved just the 5 group members, each covering a single event at a time. Every evaluation was done in real-time. The first week of the evaluation phase, we covered several small events (capacity less than 10000) we had on our database. The next week we had a couple of large events (Capacity more than 30000) on our calendar at the same venue which gave us concrete results on the time delays and alternate routes.

- **Setup and Data**

 The evaluation was conducted at our residences, which also served as the source for many of the events evaluated. The equipment used were one Laptop for each group member with a working internet connection. The browser used was Google Chrome. The website URL used was https://www.google.com/maps. The results were recorded in an Excel spreadsheet. We started the evaluation at the Pre-start time that was set for every event and ended the evaluation at the Post-end time. For each event, we used routes from 5 different directions. Each route had a primary route that passed through the venue and one or more alternate routes that were outside the radius or sometimes inside depending on the available routes. Each one of us opened 5 different tabs on the browser with routes from 5 different directions and started recording results corresponding to the Pre-start time defined for the event. Once the routes were set, we refreshed the Google Maps page every 10 mins and recorded the results. The results recorded in the Excel spreadsheet were as follows: - 
-	Venue
-	Event time
-	Source and Destination
-	Distance (kms)
-	Recorded time (current system time)
-	Travel time (Inside Radius)
-	Time delay 
-	Screenshots of alternate routes (Outside the radius)

**Evaluation Example**

- **Example 1**

	• Source – Kenilworth Park
	
	• Destination – National Gallery of Ireland
	
	• Distance – 4.2 kms
	
	• Venue – Gaiety theatre, 17th July
	
	• Start time – 3.30
	
	•Capacity – 2000 (Small Event)

  
  ![EvEx](nhriday.github.io/data.JPG)
  
  
- **Example 2**

	• Source – Moeran road, Walkinstown
	
	• Destination – 131 E Wall Rd, Dublin
	
	• Distance – 8.9 kms
	
	• Venue – 3 Arena, 28th July
	
	• Start time – 18.30
	
	•Capacity – 13000 (Large Event)

  
  ![EvEx2](nhriday.github.io/data2.JPG)
  
  
- **Example 3**
  
	• Source – Temple Bar
	
	• Destination – Ringsend Park
  
  Our system displayed 3 routes for the above source and destination. There were two events on each of the routes and the third route was suggested outside the radius, which meant that the user could avoid the traffic due to both the events 
  
  
  ![EvEx3](nhriday.github.io/data3.png)
  

  
**Evaluation Outcome**

From the evaluation phase, the following outcome was observed

- **Suitable for large events** – From the data collected, we observed that the system was successful when used during larger events. The delay times during the small events was unclear. The traffic did not seem to be affected only by the event, it may have been the usual rush hour traffic or the real-time traffic during that time. Whereas, the time delays observed during the larger events were significant inside the radius which means the traffic inside the radius during the event was high enough for delays to be recorded. Therefore, we can conclude that the system works as intended for larger events

- **Pre and post times accurate for larger events** – We observed that the pre and post times defined for larger events were accurate for the ones we evaluated compared to the smaller events. The delay times we recorded from the pre-start time to the post-end time were due to the traffic caused by the event. Again, the pre and post times did not seem to affect the time delays and the traffic was also not affected due to the event and was usual traffic at that particular time.

- **Delay times inside radius (Average of 15 minutes)** – From the data we collected for the larger events (Capacity greater than 10000), we observed that delay times due to traffic inside the defined radius around the venue was an average of 15 mins. 

- **Alternate routes were outside the radius (Approx 70%)** – From the data we collected, the alternate routes suggested by the application were outside the radius with a success rate of 70%. The alternate routes were almost faultless for smaller events with the routes outside the radius. For larger events, the alternate routes did cross over with the primary route inside the radius a few times, but the routes were outside the radius for most of the events and hence the mentioned success rate.



# Conclusion

**Project Management**  

We followed an Agile project management strategy where we went through six sprints of two weeks for each sprint. We named a Scrum master and he divided specific tasks between the teams. Weekly progress was tracked by the scrum master and the problems were discussed with everyone contributing to solve issues if any. We met every weekend to discuss the weekly progress and more importantly the plan for the week ahead corresponding to the sprints defined. The report and the presentation work were done with everyone during the weekly meetings.

 Initially all of us worked together on the data collection phase and the data cleaning phase as there were a lot of manual data to be filled in the database. It needed the contribution of all the team members to enter the estimated end-time, Pre-start and Post-end times, access Google Maps API to retrieve missing location co-ordinates of venues, visualize the radius according to the defined area using [FreeMapTools](https://www.freemaptools.com/). After the database was setup, the team was divided into two, a front-end and a back-end team. The front-end team was responsible for developing the client application (Android app) and establishing connection with the flask server to retrieve the route (Primary and Alternate) information from google maps. The back-end team was responsible for creating the flask web API, configuring the web server and the database as well and integrating the web API and the server to retrieve event information. After the database was configured, the data collected initially was pushed to the database. The following illustration represents the process flow and the sprints we defined.

![Sprint]( nhriday.github.io/sprints.JPG )

In addition to the above sprints, we discuss the progress and issues at least every two days over text messaging or Skype. At the end of each week, all of us make sure we meet face to face at UCD mostly to discuss the progress and get ready for the next sprint. Initially we divided ourselves into two teams of 2 and 3 to work on front-end and back-end development respectively. After the second sprint, the whole team took on the responsibility of writing the report and readying the presentation. All 5 of us met at the end of the second sprint and gave inputs on what each of them worked on and came up with the report and the presentation.

**Challenges and Lessons learned**

-	Project Management – Initially we did not follow any kind of project management methodology, we did not meet regularly and communicated over the phone. We soon realized it did not work at all as we missed the deadlines we had set for the second week regarding the data collection and cleaning phase. We came up with a concrete plan moving ahead, an agile methodology with six sprints. We started communicating more regularly and meeting face to face to make sure we met all the deadlines we set. The front-end and the back-end teams met at least 3 times in a week excluding the team meeting in the weekend and worked on the project. Even though we did not follow a formal method to track the progress of the project and the contributions, strict deadlines were set by the scrum master and we learned the importance of meeting deadlines, achieving shorter goals and in turn completing the intended work on time, the benefits of face to face meetings.

-	Technical Knowledge – When we started out, we were well versed with python and the reason why we chose python as our main programming language. During the course of this project, we came across a host of technologies which improved our technical skills such as Flask, MySQL, Android, and Google Maps.


**Future Implementation**

-	Notify user of time delays – We believe this would be a useful implementation as notifying the user of the time delays on the primary route to the destination can help in planning the trip better. We could not implement it as we did not have enough data to accurately gauge the traffic intensity around the venue, which would have helped in estimating a delay time on the route.
-	Save user preferences – The option for the user to save a preferred source and destination instead of typing it in every time they use the app would be a very useful improvement and would improve the efficiency of the system as a whole as well. We implemented the login functionality with the sole purpose of implementing the above-mentioned function. We could not implement it because we are using a third-party authentication system and the server cannot be accessed with it thereby restricting access to our database. The solution would be developing a custom authentication system which can be tweaked to interact with our server better. Given the time, a custom system can be implemented in the future.





# Demo

- **User Story 1** – John is using our app for the first time. He logs in or creates a new account as prompted by the app. By selecting the **‘Help’** option from the sidebar, he can view quick instructions on how to use the app

- **User Story 2** – Bruce wants to check if there are any events along his route before he leaves his house. He would like to go to Rathmines. He selects our **‘Map’** function. The source is his location, which is the default for any location. He observes that there are no events along his way and traffic will not affected by any events. He continues on his commute

- **User Story 3** – Pamela wants to commute from UCD to Dublin Spire, she uses our app to check for any events along the way. She enters the source and destination and is notified that there is indeed an event along her route and it is a rather large event. She clicks on the marker to find out what the event is. It turns out to be a Football match at the Aviva Stadium and traffic is very high around the venue. She checks the travel times of the primary route and alternate routes and takes a decision on her commuting route.
 
 *Note* - Currently, we display the real-travel time,notifying the delay time to the user would be a useful addition as a future implementation

 - **User Story 4** – Linda is new to Dublin. She is here for the holidays and wants to check if there are any interesting events in the city in the evening. She uses our **‘Event’** feature by selecting the date on the date picker and is shown the events in the city in real-time and information about the events as well. 


<video src="nhriday.github.io/Demo.mp4" width="400" height="400" controls preload></video>

# Resources

•	Github

•	Microsoft Word

•	Microsoft Powerpoint

•	https://github.com/ViksaaSkool/AwesomeSplash

•	https://pages.github.com

•	http://flask.pocoo.org/docs/1.0

•	https://www.tutorialspoint.com/flask

•	https://blog.miguelgrinberg.com/post/designing-a-restful-api-with-python-and-flask

•	https://developer.ticketmaster.com/

•	https://developers.google.com/maps/documentation/

•	AwesomeSplash https://github.com/ViksaaSkool/AwesomeSplash

•	Firebase https://firebase.google.com/

•	Places API https://developers.google.com/places/web-service/intro

•	Maps SDK for Android https://developers.google.com/maps/documentation/android-sdk/intro

•	Interactive Polyline Encoder Utility  https://developers.google.com/maps/documentation/utilities/polylineutility

•	FancyWalkthrough - Android https://github.com/Shashank02051997/FancyWalkthrough-Android 

•	Android Material Design Guidelines https://material.io/design/introduction/#principles 

•	Android Studio

•	Jupyter Notebook

•	Youtube

•	Google

•	Stack Overflow

•	News articles - https://www.rte.ie/news/business/2018/0316/948010-dublin-chamber-traffic/

https://www.irishtimes.com/news/ireland/irish-news/time-lost-in-dublin-traffic-costs-economy-350m-per-year-1.3066581

http://www.thejournal.ie/worlds-most-congested-cities-3377455-May2017/

https://www.joe.ie/news/bad-news-if-you-work-or-live-in-dublin-and-you-hate-traffic-472880

http://www.engineersjournal.ie/2017/06/20/dublin-congestion-e2bn-in-2033-without-corrective-action/



