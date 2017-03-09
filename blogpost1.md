# Blog #1


### The Current State
Since the pre-proposal, we have pulled the relevant data from [New York City Taxi Trip Data](http://www.nyc.gov/html/tlc/html/about/trip_record_data.shtml) and [Wunderground](https://www.wunderground.com/weather/api/) into .csv files.  As discussed with our TA, we borrowed scripts from a public Github [repository](https://github.com/toddwschneider/nyc-taxi-data) to extract raw data from nyc.gov and into our database. After extracting these two datasets, we wrote scripts to clean the data so that we could more easily integrate the two sets together. As the New York City taxi dataset is huge and involves multiple years, we realized the need for a way to randomly sample a portion of the dataset for faster queries. Therefore, we also wrote a script to take the .csv files and shrink them to a more manageable size.

Thus, we now have a database of tables from both datasets small enough but also representative enough for efficient queries. In the next section, we demonstrate an example query.

### Preliminary Findings
Here is an example query we wrote to calculate the payments and number of rides in a given pick up hour. Note: at the time we wrote this query, we did not yet have a sampling script so this took quite a few minutes.

Using this query, we were able to plot the following three graphs.

![Image of SQL Query](https://github.com/nchoi/NewYorkTaxis/blob/master/imgs/screenshot1.png?raw=true)
Here is the average payments (fare and tip combined) for rides at a given time frame. Interestingly, there is a huge peak at 5am for average payment.
![Average payment](https://github.com/nchoi/NewYorkTaxis/blob/master/imgs/average_payment.png?raw=true)
Here is the total number of payments per hour at a given time frame. Although there is a peak at average payment at 5am, there is also a extreme min of total payments per hour! This suggests, perhaps, that there are fewer taxis or fewer passengers around, making those customers who need taxis more willing to pay large amounts.
![Payments per hour](https://github.com/nchoi/NewYorkTaxis/blob/master/imgs/payments_per_hour.png?raw=true)
Here is the number of rides per hour. From 12am to 5am, the number of taxi rides plummets and then quickly rises to a peak at 6pm, around the time we'd expect most people to be going home from work.
![Rides per hour](https://github.com/nchoi/NewYorkTaxis/blob/master/imgs/rides_per_hour.png?raw=true)
The following charts related to tipping were created through a different query (not pictured. This chart shows the percent tip per hour. The hours in which customers are more likely to tip high amounts are around 8pm!
![Percent tip per hour](https://github.com/nchoi/NewYorkTaxis/blob/master/imgs/pct_tip_per_hour.png?raw=true)
This chart shows how frequently people tip a certain % of the fare. It seems that a little over 20% accounts for the majority of tips. It is interesting to note that tipping below 20% is rude, so we see a massive drop between 20 and 19%!
![Percent tip](https://github.com/nchoi/NewYorkTaxis/blob/master/imgs/percent_tip_720.png?raw=true)
This is the percentage of tip related to fare for January 2015.
![Tips percent of fare1](https://github.com/nchoi/NewYorkTaxis/blob/master/imgs/tips_percent_of_fare.png?raw=true)
Here is the same chart with a log scale.
![Tips percent of fare2](https://github.com/nchoi/NewYorkTaxis/blob/master/imgs/tip_percentage_related_to_fare.png?raw=true)

### The Future
Having demonstrated that we can make interesting queries at a decent speed, we will have to shift our focus on making more meaningful and novel conclusions from our data. As detailed in our pre-proposal, we intend to write an algorithm to find an optimal path for a taxi driver to maximize revenue while minimizing gasoline costs. We also plan to integrate weather data such that we find an optimal path that takes into account not just day of the week, time, and location, but also temperature and precipitation.


