# Retail Transaction Data Warehouse & Analytics

An end-to-end **Data Warehouse and Business Intelligence project** for analyzing e-commerce retail transactions. The project covers the full analytical workflow, from raw data processing and ETL to multidimensional analysis and business reporting.

The solution uses **SSIS** to clean and integrate transaction data into **SQL Server**, models the warehouse using a **Snowflake Schema**, builds an **OLAP cube with SSAS**, performs multidimensional analysis using **MDX**, and creates interactive business reports in **Power BI**.

## Project Overview

The dataset contains retail transactions from **March 2023 to February 2024** across five countries:

* United States
* Germany
* Canada
* United Kingdom
* Australia

The raw dataset contains approximately **302,000 transaction records and 30 attributes**, covering customer information, products, locations, transactions, shipping methods, payment methods, ratings, and order status.

After data cleaning and preprocessing, approximately **298,000 records and 21 attributes** were retained for analytical processing.

**Dataset:** [Retail Analysis Large Dataset - Kaggle](https://www.kaggle.com/datasets/sahilprajapati143/retail-analysis-large-dataset/data)

---

## Tech Stack

| Category                | Technologies                                     |
| ----------------------- | ------------------------------------------------ |
| Database                | Microsoft SQL Server                             |
| ETL                     | SQL Server Integration Services (SSIS)           |
| Data Modeling           | Snowflake Schema                                 |
| OLAP                    | SQL Server Analysis Services (SSAS)              |
| Query Language          | SQL, MDX                                         |
| Visualization           | Power BI                                         |
| Additional Analysis     | Excel PivotTable, Looker Studio                  |
| Development Environment | Visual Studio 2022, SQL Server Management Studio |

---

## Data Pipeline

```text
Retail Transaction Dataset (CSV)
              │
              ▼
       Data Cleaning & ETL
              │
             SSIS
              │
              ▼
       SQL Server Data Warehouse
              │
              ▼
      Snowflake Data Model
              │
              ▼
          SSAS OLAP Cube
              │
       ┌──────┴──────┐
       ▼             ▼
      MDX         Power BI
   Analysis        Reports
```

The pipeline transforms raw transactional data into a structured analytical model that supports multidimensional querying and business reporting.

---

## Data Warehouse Design

A **Snowflake Schema** was designed around the central `FACT_SALES` table.

![Snowflake Schema](docs/images/snowflake-schema.png)

### Fact Table

**FACT_SALES**

Stores transaction-level measures and references to analytical dimensions.

Main measures and attributes include:

* Amount
* Total Amount
* Total Purchases
* Ratings
* Feedback
* Order Status

### Dimension Tables

The warehouse contains dimensions for:

* **Customer** — customer demographics and customer segment
* **Location** — country, state, and city
* **Date** — year, quarter, and month
* **Product** — product information
* **Brand** — product brand
* **Category** — product category
* **Type** — product type
* **Shipping** — shipping method
* **Payment** — payment method

Product information is further normalized into **Product, Brand, Category, and Type dimensions**, forming the snowflake structure.

---

## ETL Process with SSIS

SSIS pipelines were developed to transform the source CSV dataset and load data into SQL Server.

Major ETL operations included:

* Reading raw transaction data from CSV files.
* Converting and standardizing data types.
* Filtering invalid and blank records.
* Removing duplicate dimension records.
* Deriving **Year, Month, and Quarter** attributes from transaction dates.
* Loading dimension tables before the fact table.
* Performing lookup transformations to map dimension keys into `FACT_SALES`.
* Loading the final processed transaction data into the warehouse.
* Validating data loads through SSIS execution results and SQL Server queries, including row-count reconciliation between pipeline output and target tables.

### Example ETL Workflow

![SSIS ETL Pipeline](docs/images/ssis-etl-pipeline.png)

The ETL process produces approximately **298,000 valid transaction records** for downstream analytical processing.

---

## OLAP Cube & Multidimensional Analysis

An **SSAS Multidimensional Cube** was built on top of the SQL Server Data Warehouse.

The cube enables analysis across multiple business dimensions such as:

```text
Sales
 ├── Time
 │    └── Year → Quarter → Month
 │
 ├── Location
 │    └── Country → State → City
 │
 ├── Product
 │    └── Category → Brand → Product
 │
 └── Customer
```

![SSAS Cube](docs/images/ssas-cube.png)

The project uses **MDX (Multidimensional Expressions)** to perform analytical queries against the cube.

Examples of analytical questions include:

* How did revenue change by quarter and year?
* Which products generated the highest revenue?
* What were the top-selling products for different customer age groups?
* Which brands performed best within each product category?
* Which cities generated the highest revenue in each country?
* How did sales quantity and revenue vary across countries over time?
* Which shipping methods were used most frequently?
* How did average product ratings vary across brands?

A total of **15 multidimensional business queries** were analyzed using the SSAS cube and MDX.

---

## Power BI Reporting

Power BI was connected to the **SSAS analytical model** to create business reports for sales and product performance analysis.

### 1. Product Sales by City

Analyzes the product types with the highest sales quantity across cities in Germany during 2023.

![Product Sales Report](docs/images/powerbi-product-sales.png)

This report helps identify which product types perform strongly in different local markets.

---

### 2. Geographic Sales Performance

Analyzes:

* Sales quantity
* Revenue
* City-level performance
* State-level performance
* Country-level performance

![Geographic Performance Report](docs/images/powerbi-geographic-performance.png)

The geographic hierarchy allows sales performance to be examined across different levels of location.

---

### 3. Monthly Brand Revenue

Analyzes monthly revenue trends for different product brands during 2023.

![Monthly Brand Revenue](docs/images/powerbi-brand-revenue.png)

The report provides a time-based view of brand performance and makes it easier to compare monthly revenue patterns.

---

## Additional Analysis

The analytical model was also explored using:

**Excel PivotTable**

The SSAS cube was connected to Excel to perform multidimensional analysis and validate analytical results using interactive PivotTables.

**Looker Studio**

Additional visualizations were created to analyze:

* Monthly revenue by country
* Geographic revenue distribution
* Sales performance by product category and time period

---

## Key Project Outcomes

Through this project, an end-to-end analytical workflow was implemented covering:

**Data Integration**

Raw retail transaction data was cleaned, transformed, validated, and loaded into a structured SQL Server Data Warehouse using SSIS.

**Data Modeling**

A Snowflake Schema was designed to organize transactional data into reusable fact and dimension tables.

**Multidimensional Analytics**

SSAS cubes, hierarchies, measures, and MDX queries were used to analyze sales across product, customer, geographic, and time dimensions.

**Business Intelligence**

Power BI reports were developed to support analysis of revenue, sales quantity, product performance, geographic performance, and monthly brand trends.

---

## Project Workflow

```text
Raw Retail Data
       │
       ▼
Data Cleaning & Transformation
       │
       ▼
SSIS ETL Pipelines
       │
       ▼
SQL Server Data Warehouse
       │
       ▼
Snowflake Schema
       │
       ▼
SSAS Multidimensional Cube
       │
       ├──────────► MDX Analysis
       │
       ├──────────► Excel Pivot Analysis
       │
       ▼
Power BI / Looker Studio
       │
       ▼
Business Reports & Insights
```

---

## Documentation

For detailed implementation steps, ETL transformations, OLAP configuration, MDX queries, and reporting processes, see the full project report:

[View Full Project Report](./Document/22520372_22520443_ProjectReport.pdf)

---

**Project period:** November 2024 – January 2025
