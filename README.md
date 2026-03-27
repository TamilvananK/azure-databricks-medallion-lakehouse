# Databricks Medallion Data Lakehouse: Flight Data Analytics

## Project Overview

This project implements a complete Medallion Lakehouse Architecture on Azure Databricks to process large-scale flight performance datasets.

Adopting a design-first approach optimized for cloud data migration, the pipeline processes data from raw file ingestion to refined, business-ready aggregates suitable for BI reporting. This project demonstrates proficiency in modern ETL/ELT patterns, streaming ingestion, transactional storage management using Delta Lake, and enterprise-grade data governance via Unity Catalog.

## Architecture Diagram

The pipeline utilizes Databricks for unified compute, leveraging Unity Catalog for governance and metadata management across the three layers of the medallion architecture.

```mermaid
graph LR
    A[Raw CSV Landing Zone] -->|Auto Loader - Structured Streaming| B[Bronze Layer: Raw Tables]
    B -->|Schema Enforcement and Cleansing| C[Silver Layer: Cleansed Tables]
    C -->|Aggregations and MERGE Upserts| D[Gold Layer: Business Tables]
    D -->|Analytics Ready| E[PowerBI or SQL Query]

    subgraph "Databricks Compute"
        B
        C
        D
    end

    subgraph "Unity Catalog Governance"
        F[(deltalaketamil.flight_project)]
    end

    B -.-> F
    C -.-> F
    D -.-> F
