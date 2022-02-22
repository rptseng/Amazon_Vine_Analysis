# Amazon_Vine_Analysis
## Background
The purpose of this project is to retrieve and analyze data from an Amazon Review dataset to determine whether there is a difference in star score between reviews written by members of the paid Amazon Vine program compared to unpaid reviews. We will be using PySpark to create a script that extracts and transforms the data, then loads this data into a pgAdmin database using an AWS RDS instance.

## ETL Process
The Amazon Review dataset chosen for this analysis was "https://s3.amazonaws.com/amazon-reviews-pds/tsv/amazon_reviews_us_Video_Games_v1_00.tsv.gz". The transformations to this dataset were made to create the following four DataFrames:
- customers_table
- products_table
- review_id_table
- vine_table

The columns of these tables were selected to fit the parameters specified in the "challenge_schema.sql" file.

After cleaning the data and connecting pgAdmin to the AWS RDS instance, the below output was retrieved when querying for the tables.

![review_id_sql.png](https://github.com/rptseng/Amazon_Vine_Analysis/blob/main/images/review_id_sql.png)

![products_table_sql.png](https://github.com/rptseng/Amazon_Vine_Analysis/blob/main/images/products_table_sql.png)

This demonstrates we were successfully able to load the Amazon Reviews into our database.

## Determining Bias of Vine Reviews
For this analysis, we will be filtering only for reviews that meet the criteria of at least 20 total votes with at least 50% of those votes being considered helpful votes. These are the assumptions we will carry for a meaningful review. The below screenshot demonstrates the slice of the data being considered for rating analysis.

![helpful_vote_df.png](https://github.com/rptseng/Amazon_Vine_Analysis/blob/main/images/helpful_vote_df.png)

From this subset of reviews, we will be comparing whether there is a difference in rate of five-star ratings from Vine members versus non-Vine members. There is a column in the dataframe called "vine" with the value "Y" for yes and "N" for no.

## Summary
![reviews_summary.png](https://github.com/rptseng/Amazon_Vine_Analysis/blob/main/images/reviews_summary.png)

- The total count of Vine reviews is 94. The total count of non-Vine reviews is 40,471.
- The total count of Vine 5-star reviews is 48. The total count of non-Vine 5-star reviews is 15,663.
- The percentage of 5-star Vine reviews is 51.1%. The percentage of 5-star non-Vine reviews is 38.7%

Based on these results, we can see that a greater percentage of reviews from Vine members are five stars compared to non-Vine reviews. This would indicate there is a bias for more positive reviews from Vine members.

A possible future analysis that can be done is to take the average star rating rather than the percentage of five-star ratings to see if a similar bias persists. An additional consideration would be to run this analysis again on reviews for a different set of products because the sample size across the Vine and non-Vine groups in Video Games is very large, where the non-Vine group is 400 times bigger than the Vine group.


