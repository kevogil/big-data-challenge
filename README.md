# Big Data Homework - "Alexa, can you handle big data?"

## Background

Many of Amazon's shoppers depend on product reviews to make a purchase. Amazon makes these datasets publicly available. The datasets are quite large and can exceed the capacity of local machines to handle. One dataset alone contains over 1.5 million rows; with over 40 datasets, this can be quite taxing on the average local computer. By leveraging AWS, we can perform an ETL (extract, transform, load) process entirely in the cloud.

A list of the various product review datasets can be found at the following link: <br>
https://s3.amazonaws.com/amazon-reviews-pds/tsv/index.txt


### Extract
For this project, we will be creating a dataframe of Amazon customer reviews from various <b>office</b> and <b>health/personal care</b> products with PySpark in Google Colaboratory.

`Number of records in office_products_df: 2,642,434` <br>
`Number of records in health_personal_care_df: 5,331,449`

<hr>

### Transform
For each dataset, we create 4 separate tables to be loaded into our Amazon RDS (relational databases).

#### review_id_table
This table consists of each individual `review_id`, their corresponding `customer_ID`, the `product_id` and `product_parent` of the product reviewed, as well as the `review_date` of when the review was made.
The `review_date` was set to a "yyyy-mm-dd" format for ease of use.

#### products
The product table will be used as a reference table, consisting of the `product_id` and the `product_title`.
This table will only contain one instance of the same product, meaning all duplicates were removed.

#### customers
The customer table shows the `customer_count`, or the number of reviews made by each individual, or `customer_id`.
This table will only contain one instance of the same customer as well, and so all duplicates were removed.

#### vine_table
The vine table consists of the `star_ratings` left by each individual customer.
This data is stored as an integer from 1 to 5.

<hr>

### Load
The completed dataframes are finally loaded to their corresponding tables into an Amazon RDS instance.