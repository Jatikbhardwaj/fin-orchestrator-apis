# 🏦 fin-orchestrator-apis: Banking Modern Data Stack with FastAPI Backend

![Snowflake](https://img.shields.io/badge/Snowflake-29B5E8?logo=snowflake&logoColor=white)
![DBT](https://img.shields.io/badge/dbt-FF694B?logo=dbt&logoColor=white)
![Apache Airflow](https://img.shields.io/badge/Apache%20Airflow-017CEE?logo=apacheairflow&logoColor=white)
![Apache Kafka](https://img.shields.io/badge/Apache%20Kafka-231F20?logo=apachekafka&logoColor=white)
![Debezium](https://img.shields.io/badge/Debezium-EF3B2D?logo=apache&logoColor=white)
![Python](https://img.shields.io/badge/Python-3776AB?logo=python&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-2496ED?logo=docker&logoColor=white)
![Git](https://img.shields.io/badge/Git-F05032?logo=git&logoColor=white)
![CI/CD](https://img.shields.io/badge/CI%2FCD-000000?logo=githubactions&logoColor=white)

---

## 📌 Project Overview

**fin-orchestrator-apis** is a comprehensive **end-to-end modern data stack pipeline** for the **Banking domain**,
enhanced with a robust **FastAPI backend** exposing CRUD APIs for banking entities.  
It simulates banking data (customers, accounts, transactions), streams real-time changes, transforms data into
analytics-ready models, and exposes a professional API interface — following best practices in data engineering, backend
development, and CI/CD.

This project blends **data engineering** and **backend API development** into a single, production-grade solution.

---

## 🏗️ Architecture

![Architecture](assets/fin-orchestrator-apis arch.jpg)

**Pipeline and API Flow:**

1. **Data Generator** → Generates synthetic banking data (customers, accounts, transactions).
2. **Kafka + Debezium** → Streams change data capture (CDC) events into MinIO (S3-compatible storage).
3. **Airflow** → Orchestrates ingestion from MinIO to Snowflake and manages snapshots & incremental loads.
4. **Snowflake** → Cloud data warehouse storing raw, transformed, and historical data layers.
5. **DBT** → Applies transformations, builds marts, and manages Slowly Changing Dimensions (SCD Type-2).
6. **FastAPI** → Provides RESTful CRUD APIs for customers, accounts, and transactions, enabling real-time access and
   manipulation.
7. **CI/CD with GitHub Actions** → Automates testing, building, and deployment of pipelines and APIs.

---

## ⚡ Tech Stack

- **Snowflake** → Cloud Data Warehouse
- **DBT** → Transformations, testing, snapshots (SCD Type-2)
- **Apache Airflow** → Orchestration & DAG scheduling
- **Apache Kafka + Debezium** → Real-time streaming & CDC
- **MinIO** → S3-compatible object storage
- **Postgres** → Source OLTP system
- **Python (Faker)** → Data simulation
- **FastAPI** → Modern, high-performance backend API framework
- **Docker & docker-compose** → Containerized setup
- **Git & GitHub Actions** → CI/CD workflows

---

## ✅ Key Features

- **End-to-end Banking Data Pipeline:** From OLTP source to analytics-ready data warehouse.
- **Real-time CDC:** Kafka + Debezium capturing Postgres WAL changes.
- **Data Transformation:** DBT staging, marts, and snapshots for historical tracking.
- **Slowly Changing Dimensions:** Full history of dimension changes via DBT snapshots.
- **Automated Orchestration:** Airflow DAGs managing data ingestion and processing.
- **Professional REST APIs:** FastAPI exposes CRUD endpoints for customers, accounts, and transactions.
- **Containerized Deployment:** Easy setup via Docker.
- **CI/CD Pipelines:** Automated testing and deployment with GitHub Actions.

---

## 📂 Repository Structure

```text
fin-orchestrator-apis/
├── apis/                      # FastAPI routers for customers, accounts, transactions
│   ├── __init__.py
│   ├── customers.py           # Customer CRUD API
│   ├── accounts.py            # Account CRUD API
│   └── transactions.py        # Transaction CRUD API
├── core/
│   ├── __init__.py
│   └── db.py                  # Snowflake connection helper
├── banking_dbt/               # DBT project (models, snapshots, tests)
├── consumer/                  # Kafka to MinIO ingestion script
├── data-generator/            # Faker-based synthetic data generator
├── docker/                    # Airflow DAGs, plugins, and configs
├── kafka-debezium/            # Kafka connectors and CDC config
├── postgres/                  # PostgreSQL OLTP schema and seeds
├── docker-compose.yml         # Container orchestration
├── requirements.txt           # Python dependencies
├── main.py                    # FastAPI app entrypoint
├── README.md                  # This file
└── .github/workflows/         # CI/CD GitHub Actions workflows
```

---

## 🌐 REST API Endpoints

| Operation                   | HTTP Method | URL                              | Description                               |
|-----------------------------|-------------|----------------------------------|-------------------------------------------|
| **Customers**               |             |                                  |                                           |
| List all current customers  | GET         | `/customers`                     | Retrieve all current customers            |
| Get customer by ID          | GET         | `/customers/{customer_id}`       | Retrieve a single current customer by ID  |
| Create a new customer       | POST        | `/customers`                     | Add a new customer record                 |
| Update existing customer    | PUT         | `/customers/{customer_id}`       | Update details of an existing customer    |
| Delete a customer           | DELETE      | `/customers/{customer_id}`       | Delete a customer record                  |
|                             |             |                                  |                                           |
| **Accounts**                |             |                                  |                                           |
| List all current accounts   | GET         | `/accounts`                      | Retrieve all current accounts             |
| Get account by ID           | GET         | `/accounts/{account_id}`         | Retrieve a single current account by ID   |
| Create a new account        | POST        | `/accounts`                      | Add a new account record                  |
| Update existing account     | PUT         | `/accounts/{account_id}`         | Update details of an existing account     |
| Soft delete an account      | DELETE      | `/accounts/{account_id}`         | Mark an account as inactive (soft delete) |
|                             |             |                                  |                                           |
| **Transactions**            |             |                                  |                                           |
| List all transactions       | GET         | `/transactions`                  | Retrieve all transactions                 |
| Get transaction by ID       | GET         | `/transactions/{transaction_id}` | Retrieve a single transaction by ID       |
| Create a new transaction    | POST        | `/transactions`                  | Add a new transaction record              |
| Update existing transaction | PUT         | `/transactions/{transaction_id}` | Update details of an existing transaction |
| Delete a transaction        | DELETE      | `/transactions/{transaction_id}` | Delete a transaction record               |

---

## ⚙️ Step-by-Step Implementation

### 1. Data Simulation

- Generated synthetic banking data (**customers, accounts, transactions**) using **Faker**.
- Inserted data into **PostgreSQL (OLTP)** so the system behaves like a real transactional database (**ACID, constraints
  **).
- Controlled generation via `config.yaml`.

---

### 2. Kafka + Debezium CDC

- Set up **Kafka Connect & Debezium** to capture changes from **Postgres**.
- Streamed **CDC events** into **MinIO**.

---

### 3. Airflow Orchestration

- Built DAGs to:
    - Ingest **MinIO data → Snowflake (Bronze)**.
    - Schedule **snapshots & incremental loads**.

---

### 4. Snowflake Warehouse

- Organized into **Bronze → Silver → Gold layers**.
- Created **staging schemas** for ingestion.

---

### 5. DBT Transformations

- **Staging models** → cleaned source data.
- **Dimension & fact models** → built marts.
- **Snapshots** → tracked history of accounts & customers.

---

### 6. FastAPI Backend

- Modular FastAPI project exposes **CRUD REST APIs** for customers, accounts, and transactions.
- Connects directly to Snowflake to serve and manipulate data.
- Supports real-time data access beyond batch pipelines.
- Includes data validation, error handling, and timestamp management.

---

### 7. CI/CD with GitHub Actions

- **ci.yml:** Runs linting, DBT compile, and tests on pull requests.
- **cd.yml:** Deploys Airflow DAGs and DBT models on merge to main branch.
- FastAPI deployment can be integrated similarly.

---

## 🚀 Getting Started

1. Clone the repo:
   ```bash
   git clone https://github.com/<your-username>/fin-orchestrator-apis.git
   cd fin-orchestrator-apis
   ```

2. Configure environment variables for Snowflake credentials and other secrets.

3. Build and start containers:
   ```bash
   docker-compose up --build
   ```

4. Access FastAPI docs at:
   ```
   http://127.0.0.1:8000/docs
   ```

5. Run DBT models and Airflow DAGs as per instructions in respective folders.

## 📈 Usage

- Use FastAPI endpoints to **fetch, create, update, and delete** customers, accounts, and transactions.
- Monitor data lineage and history with DBT snapshots and Airflow orchestration.
- Extend or integrate with frontend apps, BI tools, or other services.

---

## 📊 Final Deliverables

- **Automated CDC pipeline** from Postgres → Snowflake, ensuring real-time data ingestion and consistency.
- **DBT models** including facts, dimensions, and snapshots implementing Slowly Changing Dimensions (SCD Type-2) for
  historical tracking.
- **Orchestrated DAGs in Apache Airflow** managing ingestion, transformation, and snapshot workflows with scheduling and
  monitoring.
- **Synthetic banking dataset** generated with Faker, simulating realistic customers, accounts, and transactions for
  testing and demos.
- **Robust FastAPI backend** exposing fully functional CRUD REST APIs for customers, accounts, and transactions,
  enabling real-time data access and manipulation beyond batch processing.
- **Comprehensive CI/CD workflows** using GitHub Actions automating linting, testing, building, and deployment of both
  data pipelines and API services, ensuring continuous reliability and delivery.

---

## 🙌 Contributions & Support

Contributions are welcome! Please open issues or pull requests for improvements, bug fixes, or new features.

---

## 📞 Contact

**Author:** Jatik Bhardwaj  
**LinkedIn:** [jatik-bhardwaj](https://www.linkedin.com/in/jatik-bhardwaj-502b30206/)  
**Email:** [jatikbhardwaj@gmail.com](mailto:jatikbhardwaj@gmail.com)

---

*Thank you for exploring fin-orchestrator-apis — a modern, professional banking data platform with API-first design!*

