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
   hdfs dfs -mkdir -p /user/student/retail/raw ```
