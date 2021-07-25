# Twitter-Follower-Followee-Graph

Our aim is to study the digital spread of #BlackLivesMatter in the USA. After collecting some data about the on-ground protests, I decided to use Twitter to study its online presence.
I had to draw multiple network graphs to study how the support for the movement spread.

I divided the people involved with the protest into 4 groups: 
1. the key protesters.
2. key politicians in power.
3. the key politicians in opposition.
4. celebrities and journalists.
  
I used the Twitter API using Tweepy in order to make a network graph to see what are the connections between these people. So I chose to look at the follower-followee relations between them. 

Their twitter handles are saved in different list. This is done by passing an input string from the database, then split this string at each occurrence of @
An empty list is initialised then run two for loops, for say protesters and politicians. And for each pair of a protester and a politician, the code checks whether the first is following the next using the “show_friendship” tweepy function where I pass the source and target screen names.
This returns a true or false and I append a row into the list with their handles and true/false result.

One of the issues that I faced is that since these were just Twitter handles, sometimes people either deactivate their account or they change their twitter handles so I used the try except feature so that the code keeps running even if it faces a user that doesn't exist. Since twitter has rate limits, which essentially means that there is a request window of 15 minutes and an upper cap limit on calls or requests you can make within this window. For example, for show_friendship it’s 180 requests per 15 minutes. Therefore, the code needs to run for a long duration thus I used the except tweepy.error.TweepError in case of non-existent handles. This happened with @DonaldTrump since his account was banned on Twitter.

After running the loops a list of lists is obtained. Using Pandas I create a dataframe with three columns: "Source", "Target" and “Follows”. And I convert this dataframe into a csv file and save it.

Now, in order to display these relations diagramatically in a graph network I use Gephi.
Import this csv file into Gephi under 'Edges' tab. Then based on this file edges are set between nodes if the follows column is true. Thus we get a directioned graph which represents how these key groups involved in the Black Lives Matter protests interacted on Twitter.

Gephi also allows other visual features like making the nodes different sized based on eigenvector centrality and displaying different colours and labels and their layouts.
![rq22](https://user-images.githubusercontent.com/62093616/126904045-01341a80-bea1-4111-bf4b-72d6fa04e37f.png)
Twitter Follower-Followee relations between Democrats, Republicans and the Black Lives Matter Protesters


![rq3](https://user-images.githubusercontent.com/62093616/126904074-50f7ee6d-b680-4e16-9300-97d97dc504a0.png)
Twitter Follower-Followee relations between the Black Lives Matter Protesters, left and right leaning Journalists

