# BigData-Ecommerce-Analysis

## Setup

Download the Olist dataset from:
https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce

Place all CSV files into:
data/raw/

---

## Environment Requirements

Make sure you are using a Python environment with:

- Python 3.10+
- PySpark
- Java (version 17 recommended)
- MongoDB (running locally)

Install Python dependencies:

pip install -r requirements.txt

---

## Run Order

1. Run notebooks/01_data_ingestion.ipynb  
   → Creates: data/processed/orders_core.parquet  

2. Run notebooks/02_spark_processing.ipynb  
   → Creates:
   - customer_spending.parquet  
   - top_categories.parquet  
   - monthly_trends.parquet  
   - customer_segments.parquet  

3. Run notebooks/03_mongodb.ipynb  
   → Loads processed data into MongoDB  

4. Run notebooks/04_queries_visualisation.ipynb  

---

## MongoDB Setup

This project requires a local MongoDB server running on:

mongodb://localhost:27017/

Steps:

1. Install MongoDB Community Server  
2. Start MongoDB:
   - Linux:
     sudo systemctl start mongod
   - Or:
     mongod
3. Run notebooks/03_mongodb.ipynb  

---

## Notes

- Make sure your notebook kernel uses the correct environment
- Java must be available in your environment (`java -version`)
- Data folders (raw/processed) are not tracked in Git