# Azure Databricks Data Engineering Project

An end-to-end Azure Data Engineering solution built using Azure Data Factory, Azure Databricks, and best-practice data-layering to ingest, transform, and prepare data for analytics and reporting.

---

## 🧠 Project Overview

This repository contains a complete Data Engineering pipeline using Microsoft Azure services. The pipeline ingests raw datasets, organizes them into Medallion Architecture layers (Bronze, Silver, Gold), and prepares them for downstream analytics or BI tools like Power BI. :contentReference[oaicite:2]{index=2}

It’s designed to simulate real-world scenarios and provide hands-on experience building scalable, maintainable, and cloud-native data pipelines.  

---

## 🗂️ Repository Structure
```
Azure_Databricks-DataEngineering_Project/
├── dataset/ # Used for query the data from Azure Data Factory to source location
├── factory/ # Azure Data Factory pipeline definitions
├── linkedService/ # Linked service configs - Bridge for ADF to talk with source & destination
├── pipeline/ # ADF pipeline JSON files
├── silver_layer/ # Transformed silver-level data scripts
├── gold/ # Gold layer transformation & output
├── templates/Notebooks_Job # Notebooks and jobs for Databricks
├── publish_config.json # ADF publish settings
└── README.md # Project overview and docs
```


---

## 📊 Architecture

This project uses a **Medallion Architecture (Bronze → Silver → Gold)** to process data:
<img width="1438" height="575" alt="image" src="https://github.com/user-attachments/assets/32704d57-2157-41af-9e52-ca3462617be7" />

1. **Bronze Layer – Raw ingestion:**  
   * Raw data is loaded from the `Github/buy_anything_sales.csv` file into Azure SQL Database using Azure Data Factory then ingested into Azure Data Lake Storage Gen2.

2. **Silver Layer – Cleansing & Transformations:**  
   * Azure Databricks handles cleaning, normalizing, and transforming raw records into analytical tables.

3. **Gold Layer – Analytics-ready data:**  
   * Transformed data is aggregated/organized into gold-level tables with star schema for reporting, dashboards, or Machine Learning workflows.

**Diagram:**  
<img width="1165" height="570" alt="image" src="https://github.com/user-attachments/assets/b239d00d-fa67-4595-be70-cafc1ef0e236" />
<img width="2000" height="909" alt="image" src="https://github.com/user-attachments/assets/d0a86611-31dc-442d-928c-2b437ee215fe" />

---

## 🛠️ Key Technologies Used

| Layer / Tool | Purpose |
|--------------|---------|
| **![Azure Data Factory](https://img.shields.io/badge/Azure%20Data%20Factory-0072C6?logo=microsoftazure&logoColor=white)** | Orchestration of data ingestion pipelines |
| **![Azure Data Lake Storage Gen2](https://img.shields.io/badge/Azure%20Data%20Lake%20Storage%20Gen2-0072C6?logo=microsoftazure&logoColor=white)** | Scalable storage for raw and processed data |
| **![Azure Databricks](https://img.shields.io/badge/Azure%20Databricks-FF3621?logo=databricks&logoColor=white)** | Distributed processing & transformation using PySpark |
| **![Medallion Architecture](https://img.shields.io/badge/Medallion%20Architecture-FFD700?logo=azuredevops&logoColor=black)** | Logical layering for quality, performance & governance |
| **![GitHub](https://img.shields.io/badge/GitHub-181717?style=for-the-badge&logo=github&logoColor=white)** | CI/CD |
---

## 🚀 Setup & Deployment

### Prerequisites

Before you begin, make sure you have:

- An active **Azure subscription**
- Azure Data Lake Gen2 with access credentials
- Azure Data Factory workspace
- Azure Databricks workspace
- (Optional) Power BI Desktop for reporting

---

### 💾 Data Ingestion (Bronze Layer)

1. **📌 Github_to_SQLDatabaseTable Pipeline**
  * This pipeline copies a CSV file named buy_anything_sales.csv from a GitHub hosted dataset.
  * It reads the file using a delimited text (CSV) format.
  * The pipeline writes the data into an Azure SQL Database Table.
  * It uses a direct insert operation without staging intermediate storage.
  * Data type conversions are managed automatically during the copy process.

2. **📌 incremental_pipeline Pipeline**
  * This pipeline implements incremental data loading using watermarking.
  * It first looks up the last processed date from a SQL dateholder table.
  * Then it finds the latest date from the SalesOrders table for new data.
  * Only records with OrderDate greater than the last processed date are copied to Data Lake in Parquet format.
  * Finally, the pipeline updates the dateholder table with the newest date processed.

_Please replace connection strings and service credentials in linkedService configs before deploying._

---

### 🔄 Transformation (Silver & Gold)
  * The pipeline triggers an Azure Databricks Notebook job using a Databricks-linked service in Azure Data Factory.
  * It runs one or more Databricks notebooks that contain your data transformation logic in Spark.
  * The activity specifies the notebook path and can pass parameters into the notebook if configured.
  * ADF orchestrates execution by submitting the notebook task to Databricks, where the code is executed on a Spark cluster.
  * The notebook output (success/failure and logs) is returned to the pipeline run for monitoring.

* **How to Use:**
1. Import `templates/Notebooks_Job/*` into Azure Databricks.
2. Configure your cluster and secrets (for secure ADLS access).
3. Run notebooks in sequence: Bronze → Silver → Gold.
4. Save transformed data back to ADLS.

<img width="1966" height="1125" alt="image" src="https://github.com/user-attachments/assets/be063a61-2d45-4e17-b6cd-ff1a2058cd80" />
<img width="1526" height="1125" alt="image" src="https://github.com/user-attachments/assets/b13267ba-3e3c-4f49-a29b-6ae1d1ac0958" />

---

## 💡 Project Highlights

- Implements a scalable ELT pipeline following best practices. 
- Bronze → Silver → Gold layering for data quality & analytics readiness.
- Dynamic Incremental ingestion using Azure Data Factory.
- PySpark transformations in Azure Databricks for performance & flexibility.

---

## 🧑‍💻 Contribution

Contributions, issues, and feature requests are welcome!

1. Fork the repository  
2. Create a new branch (`git checkout -b feature/your-feature`)
3. Commit your changes (`git commit -m "feat: description"`)
4. Push to your fork (`git push origin feature/your-feature`)
5. Open a Pull Request

---

## 📬 Contact

Created by **Shreeram** — for feedback or questions, open an issue or reach out via GitHub.

Happy Data Engineering! 🚀
