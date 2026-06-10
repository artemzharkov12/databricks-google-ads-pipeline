# Google Ads Data Engineering Pipeline (PySpark & Databricks)

This repository contains a complete data engineering assessment designed to clean, transform, and analyze digital marketing data from Google Ads using **PySpark** and **Databricks**.

---

## 🛠️ Tech Stack & Concepts
* **Language:** Python (PySpark SQL & DataFrames)
* **Platform:** Databricks Community Edition / Cloud Workspace
* **Storage Format:** Delta Lake (Delta Tables)
* **Query Language:** ANSI SQL

---

## 📂 Repository Structure
* `Databricks_Task.dbc` — The complete Databricks notebook archive containing all running code, markdown explanations, and pre-rendered outputs.
* `README.md` — Project documentation and overview.

---

## 🚀 Pipeline Architecture & Key Steps

### 1. Data Load & Smart Profiling
* Loaded the uncleaned Google Ads CSV dataset into a Spark DataFrame with automatic schema inference.
* Implemented a dynamic script to inspect data quality, which isolates and counts missing (`null`) values across columns, displaying only the fields that require attention.

### 2. Data Cleansing & Transformation
* **Data Normalization:** Cleaned financial strings (removed currency symbols like `$`) using regular expressions and cast fields to `double`. Handled inconsistent date formats (spread across 3 different patterns) using conditional `when().rlike()` statements. Standardized text fields using `initcap()`.
* **Hybrid Missing Data Strategy:** Filled missing values in behavioral metrics (`Clicks`, `Impressions`, `Cost`) with `0.0` to preserve upper-funnel volume. Completely removed rows with missing `Sale_Amount` (revenue) to maintain strict financial reporting integrity and avoid fabricating income data.
* **Feature Engineering:** Calculated `ROAS` (Return on Ad Spend) with conditional logic to completely eliminate potential `ZeroDivisionError` anomalies.
* **Filtering:** Narrowed the dataset down to a commercially meaningful subset of profitable ads (`ROAS > 1.0`).

### 3. Advanced SQL Analysis
* Registered the polished DataFrame as a temporary view (`df`).
* Executed an optimized SQL aggregation query utilizing `GROUP BY` and multiple window/aggregate functions (`COUNT`, `SUM`, `AVG`) to analyze daily performance trends by **Date** and **Device Type**.

---

## 💻 How to View This Project
Since `.dbc` is a binary Databricks archive format, it cannot be previewed directly on GitHub. To explore the workspace:
1. Download the `Databricks_Task.dbc` file from this repository.
2. Open your Databricks workspace.
3. Go to **Workspace** -> **Users** -> **[Your Email]**.
4. Right-click, select **Import**, and upload the `.dbc` file.
5. All code, markdown cells, and visual outputs will be fully preserved and ready to review.
