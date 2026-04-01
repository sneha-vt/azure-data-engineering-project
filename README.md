# Azure Data Factory Incremental ETL Pipeline

## Overview

This project demonstrates a **metadata-driven incremental ETL pipeline** built using **Azure Data Factory**.
The pipeline extracts data from **Azure SQL Database**, loads it into **Azure Data Lake Storage Gen2 (ADLS)** in **Parquet format**, and processes only new records using a **watermark table**.

---

## Technologies Used

* Azure Data Factory
* Azure SQL Database
* Azure Data Lake Storage Gen2
* GitHub

---

## Pipeline Architecture

The solution uses a **Master–Child pipeline architecture**.

### Master Pipeline Architecture

The master pipeline orchestrates the incremental data loading process by dynamically iterating through tables defined in the metadata table.

![Master Pipeline](Pipelinedesign.png)

Steps:

* Lookup metadata from watermark table
* ForEach loop to iterate tables
* Execute child pipeline for each table

---

## Incremental Load Logic

### Child Pipeline – Incremental Load Process

The child pipeline performs incremental data extraction using watermark logic and loads new records to ADLS in Parquet format.

![Child Pipeline](Pipelinesuccess.png)

Steps:

1. Lookup the maximum watermark value
2. Compare with the LastLoadValue in the watermark table
3. Copy new records from SQL to ADLS
4. Update watermark using stored procedure


---

## Key Features

* Metadata-driven pipeline
* Incremental data loading using watermark logic
* Dynamic SQL query generation
* Automated watermark updates
* Data stored in Parquet format in ADLS

---

## Author

Sneha Thomas
