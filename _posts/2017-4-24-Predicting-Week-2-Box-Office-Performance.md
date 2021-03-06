---
layout: post
title: Predicting Week 2 Box Office Performance
---


For my second project, I looked at trying to predict the decline between week 1 and week 2 at the box office. When I was looking at movies on Box Office Mojo, I found most movies dropped pretty significantly from week 1 to week 2, but some movies increased, and I wanted to look at the factors behind the change. 

**Data**:

I started off by scraping 5500 of the top grossing domestic movies from Box Office Mojo using BeautifulSoup. The 5500th movies corresponded to about $5 million total gross at the box office. I did not scrape more than this because I wanted to avoid movies that were not wide release as I didn’t want theater count to be a significant variable. From there, I used Scrapy to scrape basic movie information from each movie’s page (budget, runtime, rating, box office info, etc.). I also pulled critic and user reviews from Metacritic, Rotten Tomatoes, and IMDB with the help of the OMDB API.

**Cleaning Data:**

I hope to eventually refine my cleaning process here. I had a lot of missing and misleading information, and instead of maybe inputting a mean or median or finding another way to get that data, I just deleted those rows. The cleaning process took the most amount of time. I had to fix  a lot of columns like Runtime to turn them into numerical values so my algorithm could make sense of them.

I  initially thought that a good amount of movies in my dataset, around 10-15%, actually had an increase in revenue at the box office from week 1 to week 2. I eventually analyzed those outliers and found out that the great majority of those were released on a Wednesday or a Thursday. I didn’t realize that Box Office Mojo started their weeks on a Friday, meaning the opening night (and maybe the second night)  of those movies was week 1, and the next Friday to the following Thursday was week two. This made it look like some of the movies in my dataset were doing much better than they actually were. I ended up removing all movies released on Wednesday or Thursday. After all of my cleaning, I was left with about 1900 movies. 

 I also engineered two columns: season and whether the movie was released around a holiday. I wanted to see if seasonality matters because the amount of movies released and the overall quality of them varies a lot (there are more movies released and of higher acclaim in the winter). Movies released around a holiday could also have high fluctuations at the box office and I wanted my model to account for that as well.

**The model:**

The variable I was trying to predict was gross change, as a percent, between week one and week two.

![By Hour](https://github.com/adbeyer23/adbeyer23.github.io/blob/master/images/GrossChange%20copy.png?raw=true){:class="img-responsive"}

Most movies have about a 50 percent decrease in box office revenue from week 1 to week 2. I ended up taking the logarithm of gross change because neither this variable or the residuals produced from the model were normal.

I used sklearn’s Elastic Net CV (cross-validated) to optimize and to try to narrow down the amount of features in my model (because of my categorical features, I had about 90 total features). The Elastic Net CV brought my features down to about 35 and gave me an R-squared score of .29 and a mean squared error of .047. 

The strongest coefficients (by absolute value) explain a lot about how my model made predictions:

![By Hour](https://github.com/adbeyer23/adbeyer23.github.io/blob/master/images/Screen%20Shot%202017-04-24%20at%209.42.25%20PM.png?raw=true){:class="img-responsive"}


Positive coefficients mean the model predicted that they would decrease the amount of gross decline and negative coefficients increase the amount. Rotten Tomato and IMDB Rating scores being positive make sense  in that I would expect better rated movies to overall do better at the box office.The studio Weinstein makes a lot of highly acclaimed movies and release movies around the holidays, which I think explains why Weinstein has a strong coefficient.  My guess to why concert movies don’t do well the second week is because many of those movies are seen by kids/tweens (two of the concertt movies were about Justin Bieber and One Direction), who only see the movie the first week, and then nobody sees it after that. I believe week 1 gross is a negative coefficient as it is hard for a movie to continually have a high gross every week.

**Further Steps:**

1. Get more data/better deal with missing data. I ended up having to cut my dataset from 5500 movies to about 1900 because of missing data. In the future, I hope to get more data, and or find a good way to replace missing data (like with using the mean or median for the missing data).
2. Explore more non-linear relationships. Many of the  best and worst performing week 1 to week 2 movies were holiday movies. However, they differed based on review and type of movies. The worst performing movies had a lot of romance and horror movies while the best had a lot of action and drama. I want to explore these holiday movies more as there appears to be some non-linear relationships here. I want to definitely run a random forest and the like on my data to see if that does better than linear regression.
3. Bring in more features. I want to definitely look at social media mentions or other media mentions before a movie is released compared to the weekend after, to see if the relationship between those can help aid in predicting gross decline

**Project Takeaways:**

- Explore the outliers to determine if they are errors. If I did not look at my outliers more, I would have missed the fact that Box Office Mojo started their week on Friday vs. Sunday. 
- Don’t worry about finding the best or even a unique project idea. With limited time, it’s much better to have a mediocre idea and a complete project, compared to a great idea, but an incomplete project.

Interested in the code or presentation for this project? Take a look at my [GitHub](https://github.com/adbeyer23/).

