# 🏦 Banking Modern Data Stack

![Snowflake](https://img.shields.io/badge/Snowflake-29B5E8?style=for-the-badge&logo=snowflake&logoColor=white)
![dbt](https://img.shields.io/badge/dbt-FF694B?style=for-the-badge&logo=dbt&logoColor=white)
![Apache Airflow](https://img.shields.io/badge/Apache_Airflow-017CEE?style=for-the-badge&logo=apacheairflow&logoColor=white)
![Apache Kafka](https://img.shields.io/badge/Apache_Kafka-231F20?style=for-the-badge&logo=apachekafka&logoColor=white)
![Debezium](https://img.shields.io/badge/Debezium-FF0000?style=for-the-badge&logo=debezium&logoColor=white)
![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-2496ED?style=for-the-badge&logo=docker&logoColor=white)
![Git](https://img.shields.io/badge/Git-F05032?style=for-the-badge&logo=git&logoColor=white)
![CI/CD](https://img.shields.io/badge/CI%2FCD-2088FF?style=for-the-badge&logo=githubactions&logoColor=white)

## 📌 Project Overview

This project demonstrates an **end-to-end modern data stack pipeline**
for a **Banking domain**.
We simulate customer, account, and transaction data, stream changes in real time, transform them into analytics-ready models, and visualize insights — following best practices of CI/CD and data warehousing.

👉 Think of it as a **real-world banking data ecosystem** built on modern data tools.

## 🏗️ Architecture

<p align="center">
  <img src="./real_time_banking_pipeline.png" alt="Architecture Diagram" width="900"/>
</p>


### Pipeline Flow:
1.**Data Generator** → Simulates banking transactions, accounts & customers (via Faker).
2.**Kafka + Debezium** → Streams change data (CDC) into MinIO (S3-compatible storage).
3.**Airflow** → Orchestrates data ingestion & snapshots into Snowflake.
4.**Snowflake** → Cloud Data Warehouse (Bronze → Silver → Gold).
5.**DBT** → Applies transformations, builds marts & snapshots (SCD Type-2).
6**CI/CD with GitHub Actions** → Automated tests, build & deployment.

## 🛠️ Tech Stack

- ❄️ **Snowflake** → Cloud Data Warehouse
- 🔁 **DBT** → Transformations, testing, snapshots (SCD Type-2)
- 🌀 **Apache Airflow** → Orchestration & DAG scheduling
- 📨 **Apache Kafka + Debezium** → Real-time streaming & CDC
- 🪣 **MinIO** → S3-compatible object storage
- 🐘 **Postgres** → Source OLTP system
- 🐍 **Python (Faker)** → Data simulation
- 🐳 **Docker & docker-compose** → Containerized setup
- 🔧 **Git & GitHub Actions** → CI/CD workflows

## Key Features

- **PostgreSQL OLTP:** Source relational database with ACID guarantees (customers, accounts, transactions)
- **Simulated banking system:** customers, accounts, and transactions
- **Change Data Capture (CDC)** via Kafka + Debezium (capturing Postgres WAL)
- **Raw → Staging → Fact/Dimension** models in DBT
- **Snapshots for history tracking** (slowly changing dimensions)
- **Automated pipeline orchestration** using Airflow
- **CI/CD pipeline** with dbt tests + GitHub Action

## 📁 Repository Structure

```plaintext
banking-modern-datastack/
├── .github/workflows/          # CI/CD pipelines (ci.yml, cd.yml)
├── banking_dbt/                # DBT project
│   ├── models/
│   │   ├── staging/            # Staging models
│   │   ├── marts/              # Facts & dimensions
│   │   └── sources.yml
│   ├── snapshots/              # SCD2 snapshots
│   └── dbt_project.yml
│
├── consumer/
│   └── kafka_to_minio.py
│
├── data-generator/             # Faker-based data simulator
│   └── faker_generator.py
│
├── docker/
│   └── dags/                   # Airflow DAGs, plugins, etc.
│       ├── minio_to_snowflake.py
│       └── scd_snapshots.py
│
├── kafka_debezium/             # Kafka connectors & CDC logic
│   └── generate_and_post_connector.py
│
├── postgres/                   # Postgres schema (OLTP DDL & seeds)
│   └── schema.sql
│
├── .gitignore
├── docker-compose.yml          # Containerized infra
├── dockerfile-airflow.dockerfile
├── requirements.txt
└── README.md
```

## Step-by-step Implimentation

### 1.Data Simulation

- Generated synthetic banking data (customers, accounts, transactions) using **Faker**.
- Inserted data into **PostgreSQL (OLTP)** so the system behaves like a real transactional database (ACID, constraints).
- Controlled generation via config.yaml.

### 2.Kafka / Debezium CDC

- Set up **Kafka Connect & Debezium** to capture changes from **Postgres**.
- Streamed CDC events into **MinIO**.

### 3.Airflow Orchestration

- Built DAGs to:
    - Ingest **MinIO data → Snowflake (Bronze)**.
    - Schedule **snapshots & incremental loads**.
 
### 4.Snowflake Warehouse

- Organized into **Bronze → Silver → Gold layers**.
- Created **staging schemas** for ingestion.

### 5.DBT Transformations

- **Staging models** → cleaned source data.
- **Dimension & fact models** → built marts.
- **Snapshots** → tracked history of accounts & customers.

### 6. CI/CD with GitHub Actions

- **ci.yml** → Lint, dbt compile, run tests.
- **cd.yml** → Deploy DAGs & dbt models on merge.

## 📊 Final Deliverables

- **Automated CDC pipeline** from Postgres → Snowflake
- **DBT models** (facts, dimensions, snapshots)
- **Orchestrated DAGs in Airflow**
- **Synthetic banking dataset** for demos
- **CI/CD workflows** ensuring reliability

