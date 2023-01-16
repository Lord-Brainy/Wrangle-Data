# Wrangle Report

## Gathering data for this project

This project involved gathering of data from three different sources as listed below. For each of the data source a different method of data gathering applied:

Importing data, already given via pandas' read_csv function
Using requests to download data off internet
Scrape data from an API
This was challenging and fun at the same time.

### Three data sources

#### Enhanced Twitter Archive

The WeRateDogs Twitter archive provided by Udacity. This contains basic tweet data for all 5000+ of their tweets, but not everything.I manually downloaded this file manually by clicking the following link: twitter_archive_enhanced.csv

#### Image Predictions File

The tweet image predictions, i.e., what breed of dog (or other object, animal, etc.) is present in each tweet according to a neural network. This file (image_predictions.tsv) is hosted on Udacity's servers and should be downloaded programmatically using the Requests library and the following URL: image_predictions.tsv

#### Data via the Twitter API

Each tweet's retweet count and favorite ("like") count. Using the tweet IDs in the WeRateDogs Twitter archive,I queried the Twitter API for each tweet's JSON data using Python's Tweepy library and store each tweet's entire set of JSON data in a file called tweet_json.txt file. Each tweet's JSON data was written to its own line.I read this .txt file line by line into a pandas DataFrame with (at minimum) tweet ID, retweet count, and favorite count.

## Assessing data

The data we got wasn't in standard formats, the way we want it. After gathering the required data, I came up with the following issues with it, after accessing it both visually and programmatically:

### Quality issues

1. In **tweet_api dataframe**, the `id` column was the wrong datatype

2. In **twitter_enhanced dataframe**, irrelevant columns were present (in_reply_to_status_id, retweeted_status_id)

3. The **three dataframes**, tweet id has the wrong datatype (should be object type)

4.  **df_image_predictions** should only have jpg_url and tweet_id and the correct prediction, no other information is required

In **twitter_enhanced dataframe**,

5. the `timeframe` was in the wrong datatype (should be datetime) 

6. the `source` column has irrelevant information instead of just containing the device the tweet is from e.g Iphone instead of _"\<a href="https://twitter.com/download/iphon..."_.

7. wrong definitions of null values ( None instead of nan) 

8. `name` column has names such as 'a', 'actually' which  is definitely an error(wrong entries are all small letters)

9. `rating` both the denominator ane numerator have really ominous values

### Tidiness issues

1. The  **three dataframes** should all be one big table

2.  The **image prediction dataframe** has 3 predictions(why not just keep the one that is true, instead of having 3 predictions), each variable should be just a column

## Cleaning Data

I used my knowledge of python and searching over the internet i.e. google, stackoverflow for references and possible guidance to resolve the above mentioned issues to the best of my knowledge. There was lot trial and error for difficult cases where regular expressions had to be used but at the same time some things for instance dropping the not so useful columns was pretty straight forward.

Overall, I learned a lot about how to use python effectively and efficiently to clean data and store it.

## Storing data

After cleaning the data, I stored the newly cleaned data into a csv file named 'twitter_archive_master.csv'