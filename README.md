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

1. **Bronze Layer – Raw ingestion:**  
   * Raw data is loaded from the `dataset/` folder into Azure Data Lake using Azure Data Factory. :contentReference[oaicite:3]{index=3}

2. **Silver Layer – Cleansing & Transformations:**  
   * Azure Databricks handles cleaning, normalizing, and transforming raw records into analytical tables. :contentReference[oaicite:4]{index=4}

3. **Gold Layer – Analytics-ready data:**  
   * Transformed data is aggregated/organized into gold-level tables for reporting, dashboards, or Machine Learning workflows. :contentReference[oaicite:5]{index=5}

**Diagram (optional):**  

---

## 🛠️ Key Technologies Used

| Layer / Tool | Purpose |
|--------------|---------|
| **Azure Data Factory** | Orchestration of data ingestion pipelines |
| **Azure Data Lake Storage (Gen2)** | Scalable storage for raw and processed data |
| **Azure Databricks** | Distributed processing & transformation using PySpark |
| **Medallion Architecture** | Logical layering for quality, performance & governance |
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

1. Upload your raw `.csv` files into the `dataset/` folder.
2. Use Azure Data Factory to connect to this data source.
3. Create a Copy Pipeline:
   - Lookup all dataset paths.
   - For each data file, copy into your Bronze container.

_Please replace connection strings and service credentials in linkedService configs before deploying._

---

### 🔄 Transformation (Silver & Gold)

1. Import `templates/Notebooks_Job/*` into Azure Databricks.
2. Configure your cluster and secrets (for secure ADLS access).
3. Run notebooks in sequence: Bronze → Silver → Gold.
4. Save transformed data back to ADLS.

---

## 💡 Project Highlights

- Implements a scalable ELT pipeline following best practices. :contentReference[oaicite:6]{index=6}
- Bronze → Silver → Gold layering for data quality & analytics readiness. :contentReference[oaicite:7]{index=7}
- Modular metadata-driven ingestion using Azure Data Factory. :contentReference[oaicite:8]{index=8}
- PySpark transformations in Azure Databricks for performance & flexibility. :contentReference[oaicite:9]{index=9}

---

## 🧑‍💻 Contribution

Contributions, issues, and feature requests are welcome!

1. Fork the repository  
2. Create a new branch (`git checkout -b feature/your-feature`)
3. Commit your changes (`git commit -m "feat: description"`)
4. Push to your fork (`git push origin feature/your-feature`)
5. Open a Pull Request

---

## 📄 License

This project is open-source and free to use under the [MIT License](LICENSE) — *if you choose to include one.*

---

## 📬 Contact

Created by **Shreeram** — for feedback or questions, open an issue or reach out via GitHub.

Happy Data Engineering! 🚀
::contentReference[oaicite:10]{index=10}
