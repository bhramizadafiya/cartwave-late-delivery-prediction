# Processed Data Notes

The preprocessing pipeline generated the following processed files:

- merged_orders.csv
- train.csv
- test.csv
- model_results.csv

These files were generated from the raw Olist data after:
- filtering delivered orders
- creating the late_delivery_flag target variable
- aggregating item-level and payment-level tables to the order level
- merging orders, items, payments, and customer tables
- engineering time-based features
- handling missing values
- encoding categorical variables
- splitting the data into training and testing sets

The processed files were stored in Amazon S3 for reproducibility and reuse across notebook sessions.
