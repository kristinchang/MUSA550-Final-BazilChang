---
title: "Methodology"
date: 2021-12-15
categories:
  - blog
tags:
  - Github Page
  - update
---

The following describes the methods used to produce each Green New Deal analysis tool.

**Air Pollution over Time(2001-2014) Visualization**

* Data

We downloaded a csv of ozone and pm2.5 contaminants data from the [Louisiana Department of Health portal](https://healthdata.ldh.la.gov/). We also downloaded parish geo data from the Louisiana Department of Transportation. Then, we cleaned the data by simplifying columns and renaming and converting the datatype of primary and foreign key columns to match to be joined. We converted both dataframes from wide to long form. We also converted the year column to a datetime object and extracted just the year for a clean year column.
* Spatial Joins

We then merged both the to the parish dataframe separately. Finally, we trimmed to the most recent 6 years so the file would be the appropriate size for github pages and projected both dataframes in crs 4326. 

* Visualizations

We generated interactive maps using hvplot, grouping by year such that change over time can be observed. Finally, we saved both plots as html files to be embedded in github pages.

**Fossil Fuel Production Dashboard**
* Data

We again use parish-level geographies, and the air quality data leveraged in part 1 of our toolkit. We then read in point data on the location and capacity of petroleum refineries in 2020 in the United States from the [Energy Information Administration](https://www.eia.gov/maps/layer_info-m.php). We filter the refinery data to Louisiana, and use atmospheric distillation thousands of barrels per day (AD_Mbpd) as a proxy for general facility capacity. We also leverage point data representing offshore drilling platform locations in the Gulf of Mexico. This data was collected as a part of the second iteration of the Designing a Green New Deal studio and was retrieved from the studio Box folder.

* Spatial Joins

We merge the air pollution data with the parish data to create a choropleth map of Louisiana with the colors representing the number of days each parish recorded ozone contaminants above the recommended level in 2014. We then spatially join the refinery point data to the air pollution by parish polygons. 
Because multiple parishes contain more than one refinery, we use the dissolve function to aggregate refinery capacity numbers by parish. The result is one refinery capacity number per parish that is a sum of capacity across the parish. 
* Data Link

We use data link to combine the choropleth map of ozone contamination by parish with a table of aggregated refinery capacity by parish. Clicking on a parish on the map will highlight the corresponding row in the table.
* Visualizations

  - The first visualization displays the fossil fuel infrastructure in Louisiana over the choropleth map of ozone contamination. The refinery locations are represented by circles on the map with their sizes corresponding to refinery capacity. Hovering over a refinery location will display it’s lat lon and capacity. The white dots represent offshore drilling locations in the Gulf between Texas and Mississippi. On hover, the choropleth map displays the parish name and corresponding ozone contamination indicator which is encoded as the color of the polygons. The goal of this visualization is to display the higher levels of pollution that correspond with higher concentration and capacity of O&G production in Louisiana.
  - The second visualization links the choropleth map of ozone contamination with a table displaying the refinery capacity numbers by parish. This allows the user to click on a parish and then have the corresponding row containing aggregated capacity information to be highlighted. The goal of this dashboard is to easily see the aggregate refinery capacity by parish and how it relates to ozone contamination. For example, East Baton Rouge has a level of ozone contamination (bright orange on the map). Once clicked on, the user can see that the refinery capacity for this parish is high as well – 539 Ad_MDP.
  - We save and both visualizations as HTML.

**Senitment Analysis: #GreenNewDeal**

For the Twitter analysis, we applied for the Academic Use API and were successful in upgrading our developer account. We initialized the API with our credentials and conducted numerous queries, only a few of which made it into our final analysis. Each query filtered for the hashtag “green new deal” and removed retweets from the search.

For the non-geo located tweets, we filtered by start time and end time to control the date range of the information returned. We then created a data frame and made a datetime column. We outline the process for three separate analyses below:

Daily Count of Tweets following the Debate
The query we used is all tweets that used the Green New Deal Hashtag in the two weeks following the 2020 Presidential debate on September 29th, 2020. We then create a datetime index from the ‘created_at’ field and use this to group by date to get a daily count of tweets. We convert to a string and plot with Altair. The result is an interactive chart that shows a huge spike in tweets about the Green New Deal the day after the debate—confirming our theory that we would get more data about the GND during this time frame. We export to html. 

Location of GND Tweets in Louisiana in 2020
This query adds in ‘place:LA’ to filter for tweets that are geo coded in Louisiana. Because there are so few tweets that are geocoded, we expand the timeframe to be the entire year of 2020. We follow the same steps to create a dataframe and extract out the place ID as a column of its own. We then convert this place dict to a dataframe. Finally, we merge the place data frame back to the query results. We have 76 geo tweets in total. This allows us to group by the name of the location and get a count of tweets per location in Louisiana. As you can see from the results, there are some inconsistent geo locations included despite the geo filter. However, the majority of located tweets are in Larose and New Orleans. We again plot the count of tweets using Altair and export to HTML. 

Location of GND Tweets in the US in the 2 weeks post Debate
This query adds in ‘place_country:US’ to filter for tweets that are geo coded in the United States during the 2 weeks following the climate change debate. We have 269 tweets with locations in this data set after following the same methodology as above. Of these 269 tweets, 14 come from LA and 12 from Brooklyn. This indicates that the discussion of the GND is occurring in larger, progressive cities and not in areas like Louisiana that have a greater need for climate change policies. We again plot the count of tweets and export to HTML. 

Text Analysis of GND Tweets in the 2 weeks post Debate

We return to the first query of all GND tweets in the 2 weeks following the debate to have a large sample size for our text analysis. This yields 12,094 tweets. 

Word Counts
We then use tweet.text to extract the text and perform many cleaning operations such as removing URLs, extracting only lower case words, removing stop words and punctuation, and removing the search term. After only removing ‘#greennewdeal’ initially, we add #greennewdeal.',, 'green', 'new', '#GreenNewDeal' as well. This yields a final word count for frequently used words—the top word is ‘@joebiden’ with almost 1,600 tweets using it. Second is ‘#medicareforall’, and ‘support’. This would indicate a generally positive overall opinion of the GND. We plot the count of tweets and export to HTML.

Sentiment Analysis
We use TextBlob to perform a sentiment analysis of this same set of tweets. We remove the URL, and create a number of fields and a dataframe. We create date, text, polarity, and subjectivity—the final two being derived from textblob. We then remove the tweets that are unbiased (have a polarity of 0) which comes to 4819 tweets removed. 

The median post-debate polarity is 0.125 (on a scale of negative one to one) indicating a slightly positive skew to the discussion surrounding the GND. The median subjectivity is .497 (on a scale of zero to one) indicating that the subjectivity skews lower. 

We plot a histogram of both the polarity and subjectivity and export as pngs. We then plot subjectivity and polarity against each other, and observe the trend that as subjectivity increases, so does polarity in both directions. That is, as the tweets get more and more subjective, they are also either most positive or more negative. This trend makes sense given the charged nature of the Green New Deal. 

Finally, we extract the hour of the day from the date field using the datetime function. We use this to group the biased tweets by the hour of the day and generate a box and whiskers plot of polarity for each hour. Polarity skews negative around 1am and 3am. We export to png. 

