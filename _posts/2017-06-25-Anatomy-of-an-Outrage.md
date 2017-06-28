For my final project at Metis, I decided to look at how Twitter responded to a controversial story. The story I picked came from May 30th, 2017 when TMZ leaked a photo in which Kathy Griffin was holding a mask that looked like Donald Trump’s bloody, severed head. My goal of this project was to see how people responded to something controversial and to get an understanding of how something controversial goes viral. For my presentation and for this blog post, I have done the analysis in 3 acts. Because Twitter’s API let’s you grab tweets via search for only 7 days in the past, I was limited in options and glad this story came around at the beginning of June. 

**Getting the Tweets**

In order to accomplish my goal, I used Tweepy to grab 2.1 million tweets that either mentioned Kathy Griffin or used Kathy Griffin’s screen name from the time TMZ leaked the picture (2pm on May 30th) until the story died down (June 4th). I stored all of my tweets on MongoDB in an AWS instance. It took me about 3 days to get all of the tweets as I lost a day to my AWS crashing because of lack of memory and all of my tweets being lost during that process. 

For the first two acts below, I used only about 1.2 million of the 2.1 million tweets. This is because I identified many tweets as bot traffic, and I was concerned with how people reacted to this story, not computers. See Act III for my analysis of these bots.

**ACT I: Outbreak of Outrage: Looking at the First 100,000 Tweets**

For the first act, I looked at the first 100,000 tweets, equating to roughly the first 6 hours after the story broke, to get an understanding of how the story spread. The first thing I did was sentiment analysis on the tweets to see if people were reacting to this story more negatively or positively. Unsurprisingly, based on the subject matter, the tone was somewhat negative with a mean of -.19. I then decided to graph the tweets based on the time created and the polarity: 

![First 100k](https://github.com/adbeyer23/adbeyer23.github.io/blob/master/images/first100kgraph.png?raw=true){:class="img-responsive"}


Furthermore, I looked at trying to identifying news sites and conservative and liberal tweeters with heavy influences to see if they affected how a story spread. To identify news sites, I looked for certain organization mentions (Fox News, CNN, TIME, etc.) in the user description or screen name, and also for general terms like “news”. I removed any tweeters from this list that had less than 100,000 followers to remove any obvious non-news sites. This strategy worked out pretty well. To identify liberal and conservative tweets with a lot of influence I looked for tweeters with over 100,000 followers and  words like “conservative” or “democrat” in the user description. Liberal influencers were much harder to identify than conservative ones, or there may be just not as many tweeting(see the takeaway section for more information about this).

I also identified tweeters who referenced either the original TMZ article or the most retweeted article which was from the Daily Wire (which is a conservative news site).

As we can see from the graph, for the first hour to hour in a half, there isn’t a lot of tweets, but the volume starts to increase as more news sites and heavy conservative influencers start to tweet. Tweet volume also starts to increase when the Daily Wire posts there story about 1.5 hours in and people start to retweet it. 

I also did some topic modeling on these first 100,000 tweets and found good separation at 3 topics using non-negative matrix factorization and a TFIDF vectorizer.

__Topic 1: Fire Kathy Griffin__

![Act 1 Fire](https://github.com/adbeyer23/adbeyer23.github.io/blob/master/images/act1fire1.png?raw=true){:class="img-responsive"}

The first topic revolves around a push to get Kathy Griffin fired from hosting CNN’s New Years Eve special. A lot of people were wondering why CNN, who did not condone this photo, did not immediately fire her. A lot people were setting up campaigns to call CNN’s advertisers to complain.

__Topic 2: General Reporting (with a conservative slant)__

![Act 1 General](https://github.com/adbeyer23/adbeyer23.github.io/blob/master/images/act1general1.png?raw=true){:class="img-responsive"}

The second topic revolves around words used to describe the picture. However, many of these words seem to be words one would expect a conservative or someone on the alt-right would use like “liberal meltdown” or using words with strong connotations like “decapitation” .

__Topic 3: Comparisons to Obama__

![Act 1 Obama](https://github.com/adbeyer23/adbeyer23.github.io/blob/master/images/act1obama1.png?raw=true){:class="img-responsive"}

The final topic involves comparisons to Obama and his presidency. For example, there was a lot of talk about how certain people were getting fired for mocking Obama—like a rodeo clown who wore an Obama mask.

Overall, based on the topics, the prevalence of the Daily Wire article, and the amount of conservative heavy influencers,  it appears  conservative elements were an important reason for this story to go as viral as it did.

**ACT II: TAKE SIDES!: The Rest of the Tweets**

In the second act, I looked at the rest of the tweets to get an understanding of how the story progressed. The first thing I found is that the links being tweeted were different. The Daily Wire link was no longer the most retweeted, and was beaten out by a pro-Griffin anti-Trump article in Teen Vogue and an article in the liberal-leaning Vulture. There were still a lot of conservative-leaning links being posted, but overall  appeared there was somewhat of a pushback in liberal-leaning viewpoints.

We can see this in the topics as well. Because there were a  lot more tweets spanning a greater amount of time, I find the best number of topics to be 6, again with non-negative matrix factorization and a TFIDF vectorizer working the best.

__Topic 1: Kathy Griffin getting fired from CNN__

![Act 2 Fire](https://github.com/adbeyer23/adbeyer23.github.io/blob/master/images/act2fire%20kathy%20griffin.png?raw=true){:class="img-responsive"}


In the first topic, there is general talk about Kathy Griffin eventually getting fired from CNN.

__Topic 2: Comparisons to Obama__

![Act 2 Obama](https://github.com/adbeyer23/adbeyer23.github.io/blob/master/images/act2comparisons%20to%20obama.png?raw=true){:class="img-responsive"}

Unlike comparisons between Trump and Obama in the first 100,000 tweets, these comparisons are definitely coming from more liberal viewpoints. Tweeters were bringing up how Ted Nugget had threatened Obama, and many people were hanging mannequins that looked like Obama. Back then, a lot of conservatives were defending that as free speech, and many are asking if that was free speech, how is what Kathy Griffin doing now not free speech?

__Topic 3: Kathy Griffin’s Apology and claims of being bullied__

![Act 2 Apology](https://github.com/adbeyer23/adbeyer23.github.io/blob/master/images/act2apology.png?raw=true){:class="img-responsive"}

This topic seems to center around Kathy Griffin’s eventual apology for the photo and then claims that Trump and some members of his family (like Donald Jr.) were bullying Kathy Griffin through their tweets and talks to the media.

Topics 4 through 6 center around some of the most retweeted tweets.

__Topic 4: Trump’s tweet about Kathy Griffin__

  ![Act 2 Trump](https://github.com/adbeyer23/adbeyer23.github.io/blob/master/images/act2trumptweet.png?raw=true){:class="img-responsive"}

This topic focuses a lot on Donald Trump saying Kathy Griffin should be ashamed, and whether or not his children, especially Barron, are legitimately disturbed by this photo.

__Topic 5: Mentions of Trump’s “sensitive children”__

  ![Act 2 Stetten](https://github.com/adbeyer23/adbeyer23.github.io/blob/master/images/act2stettentweet1.png?raw=true){:class="img-responsive"}

Two people: Melissa Stetten above, and Rickey Gervais were the most and third most retweeted respectively. Both tweeted in a kind of mocking and funny tone, pointing out who Trump’s children are, and if they would actually be disturbed with a picture like this.

__Topic 6:  Defending Kathy Griffin/Calling out Trump__

  ![Act 2 Apatow](https://github.com/adbeyer23/adbeyer23.github.io/blob/master/images/act2apatowtweet.png?raw=true){:class="img-responsive"}

This topic revolves around Judd Apatow’s tweets and others like him in which there is either a defense of Kathy Griffin, or assertions that what Kathy Griffin did was not in good taste, but what Trump does, like denying climate change, is much, much worse.  To me, these assertions are somewhat bizarre and have a somewhat us vs them mentality to them. Kind of like with the comparisons to Obama, there is not a lot of general talk about the limits of free speech, whether something is “free speech” or not is determined by what group you affiliate with. 

**Act III: Rise of the Bots: Analyzing the Bot Traffic**

When examining all of my tweets, I wanted to get an understanding of who was tweeting most about the event. What I ended up seeing is that there were quite a lot of tweeters tweeting 100+ times just about Kathy Griffin, with some tweeting 600+ times. When I looked at some of those tweeters in more depth, I saw that the vast majority of their tweets were retweets and many were retweets of the same thing over and over again or the tweets did not make a lot of sense (using weird phrasings or combinations of hashtags).  Based on this, and a lot of articles I read, I realized that Twitter had a lot of bots and a big chunk of my tweets were most likely bot traffic. I decided to separate suspected bot tweets from probable human tweets.

After a lot of trial and error, I decided on labeling a tweet as from a bot if the tweeter tweeted 15 or more times about this event and 95%+ were retweets. This isn’t perfect, and I believe some of the people in this category were not bots, and that many of the bots now are more sophisticated so that they can create original tweets too. However, based on eyeballing many of this suspected bots, I believe these metrics do pretty good to help get an understanding of who bots are and what they are tweeting about. I ended up labeling around 900,000 of my 2.1 million tweets as probably from bots.

What is scary,  was not just that there was so much bot traffic, but that the bot traffic may have even eclipsed the human traffic at the beginning of the story:

  ![Bot by day](https://github.com/adbeyer23/adbeyer23.github.io/blob/master/images/botbyday.png?raw=true){:class="img-responsive"}

Bots maybe made this story more viral than it would have been in the absence of bots. 

Next I looked at the partisanship of these bots:

  ![Bot Partisan](https://github.com/adbeyer23/adbeyer23.github.io/blob/master/images/botpartisan1.png?raw=true){:class="img-responsive"}

I determined partisanship by looking at the hashtags being used (I would rarely expect a liberal to use #MAGA) and what words were being used in user descriptions (similar to how I determined liberal and conservative influencers in act I). For many of these bots, many of their descriptions were just a bunch of hashtags (like #MAGA #TrumpTrain, #LockHerUp, etc.). Almost all of the bots I could recognize leaned conservative and were overwhelmingly using conservative hashtags:

I am not sure how much of an effect bot traffic, especially bot traffic leaning in a certain direction, affects a story and how people respond to it. I hope to look at that more in the future.

**Epilogue: Takeaways**

- Stories become viral when they are multi-faceted, when people can grab on to many different parts. This story was pretty popular for 3-4 days, and I believe this is because of all the different things that happened (CNN firing Griffin, Griffin’s apology, Trump getting involved, etc). Also, this story did not fully fall down partisan lines and there were some nuance in reactions. Anderson Cooper, left-leaning and Griffin’s colleague at CNN, denounced Kathy Griffin, and many people, while not agreeing with what Kathy Griffin did, defended her right to free speech.
- Bots take up a huge chunk of traffic, and maybe be effecting how far a story is reaching. Are bots, like the ones tweeting about the Kathy Griffin story, making stories more viral? I would assume so because they can cause these stories to start trending, but more research needs to be done in this area. 
- It is much easier to identify conservative tweeters than liberal ones. Many conservative tweeters see their political leaning as a “badge of honor” and proudly label that they are, for example, conservative or part of the alt-right (I am assuming the imbalance between labeled conservatives and liberals is not because there are much more conservatives on Twitter). Liberals don’t mention that they are liberal or democrat that much. In fact, when I was looking for liberal bots and influencers, I had the word “liberal” in the user description as signifying a liberal tweeter. However, most of the people who mention liberal in their user description were saying something like “fighting liberal thought,” so I had to remove that as an identifier. 
