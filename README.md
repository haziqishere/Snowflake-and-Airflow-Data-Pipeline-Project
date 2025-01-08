# Snowflake Data Pipeline Project

A modern data pipeline leveraging dbt, Airflow, and Snowflake to transform TPC-H sample data into analytics-ready models.

![Pipeline Flow](./readme%20photos/DAG.png)

## Tech Stack

![Snowflake](https://img.shields.io/badge/Snowflake-29B5E8?style=for-the-badge&logo=snowflake&logoColor=white)
![Apache Airflow](https://img.shields.io/badge/Apache%20Airflow-017CEE?style=for-the-badge&logo=Apache%20Airflow&logoColor=white)
![dbt](https://img.shields.io/badge/dbt-FF694B?style=for-the-badge&logo=dbt&logoColor=white)
![Docker](https://img.shields.io/badge/docker-%230db7ed.svg?style=for-the-badge&logo=docker&logoColor=white)
![Python](https://img.shields.io/badge/python-3670A0?style=for-the-badge&logo=python&logoColor=ffdd54)

## Project Overview

This project demonstrates a production-grade data transformation pipeline that:
- Sources TPC-H sample data from Snowflake
- Transforms raw data through staging and intermediate models
- Creates final fact tables for analytics
- Implements data quality tests
- Orchestrates the entire workflow using Airflow and Cosmos

## Data Models

The project follows a layered transformation approach:

### Staging Layer
- `stg_tpch_orders`: Standardizes orders data
- `stg_tpch_line_items`: Processes line item details

### Intermediate Layer
- `int_order_items`: Combines orders with line items
- `int_order_items_summary`: Aggregates order metrics

### Mart Layer
- `fct_orders`: Final fact table with order details and metrics
## Project Structure

The project repository is organized as follows:

```
/Snowflake-Airflow-Date-Pipeline-Project
│
├── dags/                   # Airflow DAGs
│   └── tpch_dag.py         # Main DAG definition
│
├── dbt/                    # dbt project directory
│   ├── models/             # dbt models
│   │   ├── staging/        # Staging models
│   │   ├── intermediate/   # Intermediate models
│   │   └── marts/          # Mart models
│   └── dbt_project.yml     # dbt project configuration
│
├── docker/                 # Docker setup files
│   └── Dockerfile          # Dockerfile for the project
│
├── readme_photos/          # Images for README
│   └── DAG.png             # Pipeline flow image
│
└── README.md               # Project README file
```

This structure ensures a clear separation of concerns, making it easier to manage and scale the project.

## Setup

To set up the project, follow these steps:

1. **Clone the repository**:
    ```sh
    git clone https://github.com/yourusername/Snowflake-Airflow-Date-Pipeline-Project.git
    cd Snowflake-Airflow-Date-Pipeline-Project
    ```

2. **Initialize the Astro project**:
    ```sh
    astro dev init
    ```

3. **Start the Airflow environment**:
    ```sh
    astro dev start
    ```

4. **Set up dbt profiles**:
    - Create a `profiles.yml` file in the `~/.dbt/` directory with your Snowflake credentials.

5. **Install dbt dependencies**:
    ```sh
    astro dev run dbt deps
    ```

6. **Run dbt seed to load seed data**:
    ```sh
    astro dev run dbt seed
    ```

7. **Run dbt models**:
    ```sh
    astro dev run dbt run
    ```
    ```

## Usage

Access Airflow UI at [http://localhost:8080](http://localhost:8080)

### Running the Pipeline

- Enable DAG `dbt_dag`
- Trigger DAG manually or wait for schedule

### Local Development

- Test dbt models:
    ```sh
    dbt test --profiles-dir /usr/local/airflow/include/dbt/
    ```

