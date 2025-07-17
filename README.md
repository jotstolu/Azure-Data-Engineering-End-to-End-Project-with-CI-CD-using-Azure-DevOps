# Azure-Data-Engineering-End-to-End-Project-with-CI-CD-using-Azure-DevOps

This project demonstrates how to build a modern, scalable data pipeline in the cloud using **Azure Data Factory**, **Azure DevOps**, **Delta Lake**, and **Databricks**. The pipeline processes CSV datasets related to the **Paris Olympics 2024**, builds silver and gold layers with **PySpark and Delta Live Tables**, and implements continuous integration using DevOps.

---

## 🧭 Project Overview

Key features of the project:

- Ingests multiple CSV files from a GitHub repo using **Azure Data Factory**
- Implements dynamic **Bronze → Silver → Gold** layering in **Databricks**
- Utilizes **Delta Live Tables (DLT)** for streaming and quality enforcement
- Includes **CI/CD with Azure DevOps Pipelines**
- Stores curated data in **Azure Synapse Warehouse** for downstream analytics

---

## 🗺️ Architecture Overview

The architecture showcases an orchestrated data flow with CI/CD integration:

![Olympics Architecture](./assets/olympics_architecture.png)

---

## 🔄 Azure Data Factory Pipeline

This pipeline handles automated ingestion of CSV files from GitHub into **ADLS Gen2 Bronze zone**.

- The `LookupJson` and `ForEach` logic dynamically controls file iteration.
- Ingested data is stored in a Bronze container for transformation.

![ADF Pipeline](./assets/datafactory_pipeline.png)

---

## 🧪 Silver Layer: Dynamic Data Ingestion in Databricks

The Silver layer consists of Databricks jobs that dynamically process multiple JSON/CSV files stored in ADLS Bronze.

- Uses PySpark to parse JSON arrays
- Converts raw Bronze data to clean Silver tables
- Saves each transformed dataset to its respective Silver container

![Dynamic Data Reading](./assets/dynamic_data_reading_and_writing_workflow.png)

---

## 🥇 Gold Layer: Delta Live Tables

The Gold layer is built using **Delta Live Tables (DLT)**.

- Reads Silver tables via Spark Structured Streaming
- Applies transformations and merges into star-schema-ready tables
- DLT manages schema enforcement and handles incremental loads

![DLT Pipeline](./assets/DLT_pipeline.png)

---

## 🗂️ Notebooks in This Project

```
olympics_project/
├── json_notebook.python               # Parses and explodes JSON data
├── Silver_Nocs.python                 # Silver table for countries
├── Silver_Coaches & Events.python     # Silver table with nested JSON flattening
├── silver_Athletes.python             # Athlete-level silver table
├── Gold_Notebook.python               # DLT logic for the gold layer
```

---

## ⚙️ Technologies Used

- **Azure DevOps** – CI/CD pipeline and automation
- **Azure Data Factory** – Ingests raw CSV files from GitHub
- **Azure Data Lake Storage Gen2** – Layered data storage (Bronze, Silver, Gold)
- **Databricks** – PySpark transformations, job orchestration
- **Delta Lake** – ACID-compliant tables
- **Delta Live Tables (DLT)** – Streaming transformations and data quality enforcement
- **Azure Synapse Analytics (Warehouse)** – Final data consumption layer

