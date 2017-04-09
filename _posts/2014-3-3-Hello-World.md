---
layout: post
title: Project 1: Finding the best locations to get emails based on NYC subway data
---

***Challenge***: Using subway data, try to find the best subway locations in NYC to spread awareness (through getting emails), and to get people to attend a gala supporting women in tech.

***Data used***: Freely available turnstile data provided by the MTA ([http://web.mta.info/developers/turnstile.html](http://web.mta.info/developers/turnstile.html)), geolocations of the various subway locations in NYC

***Tools used***: Python, Pandas, Juypter Notebook, Matplotlib, Seaborn, Plotly 

***Approach***:

First off, we wanted to see what this data looked like:

![Data head](https://github.com/adbeyer23/adbeyer23.github.io/blob/master/images/DataScreenshot_project1.png?raw=true){:class="img-responsive"}


The most important columns here are the Entries and Exits columns..and they have some gigantic numbers in them. After doing some research, we realized that those numbers were counting from the beginning of counting and therefore, we would need to subtract a row from a previous row to get the true entry and exit rates.

After looking at the data further, we found out that our most trafficked station by far was Lorimer ST. This did not make any sense  as this station is in Brooklyn, and doesn’t go along with what the MTA thinks are the most busiest station. Other stations like Fresh Pond Road were also on this list along with stations we knew had high traffic—like Grand Central station.

Upon looking further at the data, we found that sometimes it appeared that the turnstile count had reset, causing the difference between that row and the previous to be huge. We decided to remove all rows in which the count was greater than 20000—as we highly doubt any station would have had 20000 people entering or exiting it in a four hour period.

Was our data fully cleaned yet? Not quite. After finding our mean traffic were some stations being much lower than assumed, we found out that some turnstile counts were going in reverse, meaning we had negative entry or exits counts. As we did not know the cause for this, we got rid of these rows as well.

After that, we were able to see which stations were the most highly trafficked:

![top10](https://github.com/adbeyer23/adbeyer23.github.io/blob/master/images/TotalTraffic_project1.png?raw=true){:class="img-responsive"}

This goes in line with our assumptions and what the MTA believes are the busiest stations.

We also took a look at the number of entries in the stations with the most traffic by  hour interval and day of the week:

![By Hour](https://github.com/adbeyer23/adbeyer23.github.io/blob/master/images/By%20Hour.Project1.png?raw=true){:class="img-responsive"}

![By Day](https://github.com/adbeyer23/adbeyer23.github.io/blob/master/images/Byday_fixed.png?raw=true){:class="img-responsive"}


***Recommendations:***

1. We decided it would make the most sense to target passengers as they enter the station, like when they are on the platform. We felt, if passengers were waiting for the subway, they would be much more receptive to canvassers, than if they were leaving the subway, on their way to somewhere else. 
2. To maximize success, we recommend that canvassers target the most trafficked stations, most of which were in Manhattan. This does mean that a lot of tourists would be targeted (which the gala did not want). However, the stations with the most traffic, are also in areas with high densities of both women and tech companies. We predict that women and people in tech would be some of the most receptive people to wanting to further women in tech.
3. Based on our graphs, we also predict that canvassers will have the most success targeting passengers during rush hour and during the weekday. Weekday and rush hour traffic was significantly higher than traffic at other times. 

***Takeaways:***

1. **When you don’t have a lot of data and in the absence of testing a lot of assumption have to be made.** We assumed that people waiting for a subway would more likely talk to our canvassers than people just leaving the station. We also assumed that we would more success with people entering the subway in the afternoon vs. the morning. Are these assumptions true? I am not really sure. The experimenter/scientist in me wants to test this out—like by sending a group of canvassers at different times of the day and to different locations to see what happens.
2. **There is always going to be bad data, and, worse, subtly bad data. **Even if the data is machine-generated like this data was, there is always going to be issues with it. What is worse is when the data looks fine, but actually isn’t. Dataframe.describe() and domain knowledge are your friends here. Does that mean sound right? Should the minimum value be negative? You won’t be able to answer these questions unless you assiduously try to summarize the data, and know what bad data should look like.
3. **Domain-specific knowledge is important. **I am new to NYC and did not know much about the subway system. If I my fellow classmates had not helped me understand the subway system better, I would have assumed that there was nothing wrong with Lorimer ST having the highest traffic. If you don’t know what the data should look like or what it represents, it is hard to see if your outliers are bad data or not.
4. **Don’t miss the big picture. **After finding more data than expected being bad, I wanted to explore the data more to possibly fix other issues.  I also wanted to create more graphs, and bring in more data. However, we only had 5 days to complete and present on this project. Perfection must give way to good enough

Interested in the code or presentation for this project? Take a look at my [GitHub](https://github.com/adbeyer23/MTA-Analysis-Project).
