# Azure Data Engineering Pipeline using Azure Data Factory

## Project Overview

This project demonstrates an **end-to-end ETL pipeline using Azure Data Factory**.
Data is extracted from **Azure SQL Database**, processed using **incremental loading**, and stored in **Azure Data Lake Storage**.

The pipeline is designed to load **only new records using a watermark column**, improving performance and efficiency.

---

## Architecture

Azure SQL Database → Azure Data Factory → Azure Data Lake Storage

Workflow:

1. Data is stored in Azure SQL Database.
2. Azure Data Factory pipelines orchestrate the ETL process.
3. Incremental logic extracts only new records.
4. Processed data is stored in Azure Data Lake Storage.

---

## Technologies Used

* Azure Data Factory
* Azure SQL Database
* Azure Data Lake Storage Gen2
* SQL
* GitHub

---

## Pipelines

### RetailDW_Pipeline

Copies data from Azure SQL Database to Azure Data Lake Storage.

### PL_INCREMENTAL_LOAD

Loads only new records using incremental loading logic.

### PL_MASTER_INCREMENTAL_LOAD

Master pipeline that orchestrates the incremental load pipeline.

---

## Incremental Load Logic

Incremental loading is implemented using a **watermark column**.

Steps:

1. Read last processed value from watermark table
2. Extract records greater than that value
3. Load new records to Data Lake
4. Update watermark table

Example query:

```sql
SELECT *
FROM FactShipment
WHERE ShipmentKey > @LastLoadValue
```

---

## Project Structure

```
azure-data-engineering-project
│
├── dataset
├── factory
├── integrationRuntime
├── linkedService
├── pipeline
│   ├── PL_INCREMENTAL_LOAD.json
│   ├── PL_MASTER_INCREMENTAL_LOAD.json
│   └── RetailDW_Pipeline.json
│
├── Pipelinedesign.png
├── Pipelinesuccess.png
└── README.md
```

---

## Pipeline Design

![Pipeline Design](Pipelinedesign.png)

---

## Pipeline Execution

![Pipeline Execution](Pipelinesuccess.png)

---

## Author

Sneha Thomas
Software Engineer – Gamma Analytics
