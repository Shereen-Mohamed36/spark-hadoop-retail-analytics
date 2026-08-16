# Retail Analytics Pipeline (PySpark + Hadoop HDFS)

This repository demonstrates the integration between **Apache Spark** and **Hadoop HDFS** for large-scale retail analytics. Raw datasets are stored and managed in HDFS, while PySpark interacts directly with the HDFS storage layer to execute distributed transformations, window functions, and Spark SQL queries.

---

## Storage & Execution Architecture

```text
+------------------------------------+
|         Hadoop HDFS Storage        |
|  (/user/student/retail/raw/*.csv)  |
+------------------------------------+
                  │
                  │ (Distributed File Read)
                  ▼
+------------------------------------+
|        Apache Spark Engine         |
|  - PySpark DataFrame Transformations|
|  - Spark SQL Queries & CTEs        |
+------------------------------------+
```


## Data Pipeline & HDFS Setup

To replicate the execution environment on a multi-node Hadoop cluster:

1. **Create the HDFS target directory:**
   ```bash
   hdfs dfs -mkdir -p /user/student/retail/raw
   
2. **Ingest raw relational CSV datasets into HDFS:** 
   

```Bash
hdfs dfs -put datasets/*.csv /user/student/retail/raw/
```

3. **Verify file placement in HDFS:**

```Bash
hdfs dfs -ls /user/student/retail/raw 
```


### Analytical Scope & Key Queries

The project processes 16 complex business analytics queries across two core technical paradigms:

**Part I — PySpark DataFrame API**

Q1. Category Performance: Total revenue, net profit, and profit margin (profit_margin_pct) per product category.

Q2. State Top Customers: Top 5 spending customers per state using dense_rank() over state partitions.

Q3. Store Operational Metrics: Store-level revenue, profit, completed order counts, and distinct active customers.

Q4. High-Performing Staff: Identifying employees with sales exceeding their specific store average.

Q5. Inventory Risk: High-revenue products with critical stock levels (stock_quantity < 20).

Q6. Regional Peak Months: Highest revenue month per region using windowed row numbering.

Q7. Category Diversity: Customers purchasing across ≥3 distinct product categories.

Q8. Supplier Performance: Supplier ranking by volume, total revenue, and cumulative profit.

**Part II — Spark SQL Engine**

Q9. Regional Category Profitability: Dense-ranked top 3 product categories by profit per region.

Q10. Loyalty Tier Benchmarking: Customers spending above the average of their assigned loyalty tier.

Q11. Unordered Stock: Detecting products with zero sales activity via LEFT JOIN operations.

Q12. Employee Reach: Staff serving customers across more than 3 distinct cities.

Q13. Store Revenue Peaks: Identification of peak sales months per individual store location.

Q14. Revenue Share Contribution: Percentage contribution of each store to global enterprise revenue.

Q15. Multi-Order Detection: Identifying customers placing multiple orders within a single day.

Q16. Month-over-Month Revenue Drop: Detecting store monthly revenue decline against preceding months using LAG().
