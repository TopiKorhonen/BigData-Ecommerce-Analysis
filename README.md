# BigData-Ecommerce-Analysis

## Setup
Download the Olist dataset from https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce and place all CSV files in data/raw/

## Run Order
1. Run notebooks/01_data_ingestion.ipynb first. Creates data/processed/orders_core.parquet
2. Run notebooks/02_spark_processing.ipynb. Creates customer_spending, top_categories, monthly_trends and customer_segments parquet files
3. Run notebooks/03_mongodb.ipynb
4. Run notebooks/04_queries_visualisation.ipynb
