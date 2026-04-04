# Data Structure & Schema

This document defines the expected schema between notebooks to ensure smooth data flow.

## orders_core.parquet (Input to Spark Processing)

**Created by:** `01_data_ingestion.ipynb` (Topi)

**Location:** `data/processed/orders_core.parquet`

**Schema:**
```
- order_id: string (primary key from orders)
- customer_id: string (foreign key)
- customer_city: string
- customer_state: string
- order_status: string (delivered, shipped, canceled, etc.)
- order_purchase_timestamp: timestamp
- payment_value: double
- order_value: double (total order value including items + freight - discount)
- product_id: string
- product_category_name: string
- product_price: double
- review_score: int (1-5, nullable)
```

**Notes:**
- All rows should be at order-item level (one row per item per order)
- Missing values should be NULL, not 0 or "N/A"
- Timestamps in ISO format
- Currency in BRL (Brazilian Real)

---

## Spark Processing Outputs

**Created by:** `02_spark_processing.ipynb` (Nadja)

**Location:** `data/processed/`

### 1. customer_spending.parquet
```
- customer_id: string
- customer_city: string
- customer_state: string
- order_count: int
- total_spending: double
- avg_order_value: double
- min_order_value: double
- max_order_value: double
- zero_payment_orders: int
- customer_segment: string (VIP, Premium, Regular, Occasional)
```

### 2. top_categories.parquet
```
- product_category_name: string
- total_orders: int
- total_items_sold: int
- total_revenue: double
- avg_order_value: double
- avg_product_price: double
- reviewed_orders: int
- avg_review_score: double
- review_rate: double (%)
```

### 3. monthly_trends.parquet
```
- year_month: string (yyyy-MM format)
- year: int
- month: int
- order_count: int
- unique_customers: int
- total_revenue: double
- avg_order_value: double
- items_sold: int
- delivered_orders: int
- canceled_orders: int
- delivery_rate: double (%)
```

### 4. customer_segments.parquet
```
- customer_id: string
- recency: int (days since last order)
- frequency: int (number of orders)
- monetary_value: double (total revenue from customer)
- r_score: int (1-4 quartile)
- f_score: int (1-4 quartile)
- m_score: int (1-4 quartile)
- segment: string (Champions, Loyal Customers, At Risk, Potential, Need Attention)
```

---

## MongoDB Collections

**Created by:** `03_mongodb.ipynb` (John)

**Names:** Same as parquet files (customer_spending, top_categories, etc.)

**Indexes to create:**
- customer_spending: index on customer_id, customer_segment
- top_categories: index on product_category_name, total_revenue
- monthly_trends: index on year_month
- customer_segments: index on customer_id, segment

---

## Queries & Visualizations

**Created by:** `04_queries_visualisation.ipynb` (Kelechi)

- Customer lifetime value distribution
- Category performance trends
- Monthly revenue patterns
- Segment distribution pie chart
- Top 10 categories by revenue
- Customer spending by state/region
