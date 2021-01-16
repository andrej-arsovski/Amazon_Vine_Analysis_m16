# Paid Reviews and 5-Star Ratings: An Amazon Analysis

## Overview
The purpose of this work was to analyze Amazon reviews written by members of the paid Amazon Vine program. The Amazon Vine program is a service that allows manufacturers and publishers to receive reviews for their products. Companies like SellBy pay a small fee to Amazon and provide products to Amazon Vine members, who are then required to publish a review. This analysis was performed on a subset database of Amazon products (watches). 

PySpark was used to perform the ETL process to extract the dataset, transform the data, connect to an AWS RDS instance, and load the transformed data into pgAdmin. Next, PySpark was used to determine if there is any bias toward favorable reviews from Vine members in the dataset.

## Results

The raw data was extracted from Amazon's S3 database and contained various columns of data and contained 960,720 entries.

![dataframe.png](https://github.com/andrej-arsovski/Amazon_Vine_Analysis_m16/blob/main/screenshots/dataframe.png)

The dataframe was transformed first to select only reviews that had more than 20 votes, then only to include those which had at least half as many "helpful_votes" as "total_votes" 

helpful_df = votes_filter_df.filter("helpful_votes/total_votes>=0.5")
helpful_df.show()

Finally, the reviews were separated into two groups: a group that was part of the paid "Vine" program, and an unpaid group.

![paid.png](https://github.com/andrej-arsovski/Amazon_Vine_Analysis_m16/blob/main/screenshots/paid.png)


![unppaid.png](https://github.com/andrej-arsovski/Amazon_Vine_Analysis_m16/blob/main/screenshots/unpaid.png)

There were a total of 43 paid reviews compared to 7750 unpaid ones. 

14 of the 43 paid reviews were 5-Star reviews, compared to 4027 of the unpaid ones.

Therefore, 32.6% of the paid reviews were 5-star compared to 52.0% of the unpaid ones. 

## Summary

Together this data suggests that paid reviews were not more likely to yield 5-star reviews therefore not indicating a positivity bias for reviews in the Vine program. However, additional analyses could help strengthen this finding. 

One additional analysis could simply look at the average score (number of stars) of a paid review versus an unpaid one. 
