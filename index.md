# User Scenario - The Characters
### •	Who is your target user?

We believe our primary user base to be the everyday commuter who makes use of a particular route on a daily basis in order to notify the user of any events on their way, the traffic conditions and provide an alternate route if available, thereby helping them to not only save time by avoiding a certain route but also provide an alternate route to reach their destination. The application is not limited to the mentioned type of users, but can be used generally by anyone who wishes to be notified about any events along their route

### •	Why are they important?

The target users, as mentioned are the everyday men and women who are the workforce of this city. We believe in making their daily commute a bit easier and tension free so that they can concentrate solely on their work and not worrying about getting to work or coming back home

### •	What problem are you solving for them?

The primary problem of our target users we aim to solve is that of avoiding unnecessary traffic. Usually, most daily commuters may use an application that provides them the route to their destination and also frequent commuters who are well versed with the route may not use any application at all. The problem with both these approaches are neither of them are aware of any events along their route which might have led to a high traffic scenario which eventually may result in the user stuck in traffic and getting late to work, getting home or simply put, reaching their destination. Our application helps them avoid this by notifying them about any events along their way, details about the event such as capacity and an estimation of the number of vehicles, start time and probable end time of the event, and most importantly an alternate if available so that they can reach their destination

# Technical Problem: The Setting 

### •	Why does your system exist? 

When we first set out to develop this application, we had two reference points. Ticketmaster and Google Maps. Ticketmaster is a website that sells tickets for almost every event in Ireland, specifically Dublin as we are building a database that consists of events in Dublin. Google Maps is an application used by almost everyone to reach their destination and its use ranges right from taking a walk to planning a trip. We believe our system exists as an effective culmination of the best features of the two applications

### •	What is the core technical problem? 
We have developed a web API using flask which runs on the localhost of the server (provided by UCD). The problem with this is, it is not available on the public domain and we cannot access it in the application. We are facing a few minor issues with hosting it on the public domain and should be able to overcome it for the Mid-Term presentation


### •	Can you review other existing systems or products that address this problem? 
As our application is basically a route providing service or a map application, the best reference point for us was Google Maps. It is available to the public domain and can be utilized effectively. We plan to emulate the service provided by Google Maps in our own unique perspective

# Technical Solution: The Plot 
![AppLogo]( nhriday.github.io/process.JPG )


**Client - Server**
The very first step is the user entering the source and destination of the commute planned. This is done on our Android client to set the two parameters. This request is sent to our back-end server, where the server interacts with the Google direction API to obtain the geo-locations of the locations requested from the client. Using these geo-locations, a route to the preferred destination is displayed on the screen. The server communicates with a back-end database to collect information on events relevant to the route on which the user plans to commute and sends it back to the serve as a response. The server sends all this information, routes and event information back to the client

**Database**

We have a database which consists of the following information of the events: - 
*	Event title & Venue
*	Start time, End time (estimated)
*	Capacity of the venue

 
**Technology**

*	Front-end:
  *Android
   - Our front-end client is written in Android, which is an interface to help the user navigate through the application. 
  *Maps SDK
   - SDK used to manage access to Google Maps server and display the map layout in our client (application)
  *Google Places API
   - API used to get automated suggestions from Google Maps when a user types in the name of a location. It also helps in                       obtaining the geo-locations of the searched location
  *AwesomeSplash
   - used to create a custom splash screen, the screen that pops up when the app icon is clicked on. A library developed by Viktor Arsovski and is available at https://github.com/ViksaaSkool/AwesomeSplash 

*	Back-end: 
  *Flask Server
   – handle the requests from the client and call the Google Maps API for relevant information regarding routes and return the event details by accessing the database depending on the request, which is the date and time entered by the user or system time by default and the route information returned from the Google Maps API

  *mySQL database
   – stores all structured event data including venue, start time, title, capacity primarily

*	Data: What data resources are you going to use and how will you access, collect, and store them?
Ticketmaster API using python and store relevant data in the database


### Markdown

Markdown is a lightweight and easy-to-use syntax for styling your writing. It includes conventions for

```markdown
Syntax highlighted code block

# Header 1
## Header 2
### Header 3

- Bulleted
- List

1. Numbered
2. List

**Bold** and _Italic_ and `Code` text

[Link](url) and 
![AppLogo]( nhriday.github.io/1.jpeg )
```

For more details see [GitHub Flavored Markdown](https://guides.github.com/features/mastering-markdown/).

### Jekyll Themes

Your Pages site will use the layout and styles from the Jekyll theme you have selected in your [repository settings](https://github.com/nhriday/nhriday.github.io/settings). The name of this theme is saved in the Jekyll `_config.yml` configuration file.

### Support or Contact

Having trouble with Pages? Check out our [documentation](https://help.github.com/categories/github-pages-basics/) or [contact support](https://github.com/contact) and we’ll help you sort it out.
