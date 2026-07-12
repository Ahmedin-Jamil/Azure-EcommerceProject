# Azure End-to-End Ecommerce Data Engineering Project

## Project Overview
An end-to-end cloud data pipeline built on Microsoft Azure using the 
Brazilian Olist Ecommerce dataset. Raw transactional data is ingested, 
enriched, transformed, and served to analytics tools using the 
Medallion Architecture (Bronze → Silver → Gold).

## Architecture Diagram
[paste your architecture diagram image here]

## Tech Stack
| Layer | Tool |
|---|---|
| Data Sources | MySQL (filess.io), MongoDB (filess.io) |
| Ingestion | Azure Data Factory (ADF) |
| Storage | Azure Data Lake Storage Gen2 (ADLS Gen2) |
| Transformation | Azure Databricks (PySpark) |
| Serving | Azure Synapse Analytics |
| Visualization | Power BI / Tableau / Microsoft Fabric |

## Pipeline Stages

### 🥉 Bronze Layer — Raw Ingestion
- Connected Azure Data Factory to a hosted MySQL database
- Ingested 7 CSV files (orders, customers, products, payments, 
  sellers, reviews, geolocation) into ADLS Gen2 bronze folder
- Used both scheduled and parameterized ADF pipelines for 
  flexible ingestion

### 🥈 Silver Layer — Enrichment & Transformation
- Connected Azure Databricks to ADLS Gen2 using service principal
- Pulled product category translation data from MongoDB (NoSQL) 
  for data enrichment — MongoDB was chosen here because category 
  names are subject to frequent updates, making a flexible NoSQL 
  store more appropriate than a rigid SQL table
- Performed PySpark transformations: joins, null handling, 
  data type casting, and business rule validation
- Stored cleaned output back to ADLS Gen2 silver folder

### 🥇 Gold Layer — Analytics-Ready Serving
- Connected Azure Synapse Analytics to the silver layer in ADLS Gen2
- Created external tables and views using CETAS 
  (Create External Table As Select)
- Gold layer serves as the final source for Power BI, 
  Tableau, and Microsoft Fabric dashboards

## Dataset
[Brazilian E-Commerce Public Dataset by Olist](https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce)
- 100,000+ orders from 2016 to 2018
- Multiple sellers across Brazil
- Includes order status, price, payment, freight, customer location,
  product attributes, and customer reviews

## Key Learnings
- Designed a cloud-native data pipeline from scratch using Azure services
- Applied the Medallion Architecture to separate raw, clean, 
  and business-ready data
- Understood the difference between SQL (MySQL) and NoSQL (MongoDB) 
  and when to use each
- Used PySpark in Databricks for large-scale distributed data processing
