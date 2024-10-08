### README.md

```markdown
# Airflow ETL for Amazon Data Engineering Books

## Table of Contents
- [Project Overview](#project-overview)
- [Technologies Used](#technologies-used)
- [Installation](#installation)
- [Setup](#setup)
- [Creating Files](#creating-files)
- [Connecting to PostgreSQL](#connecting-to-postgresql)
- [Hosting Airflow and PostgreSQL Locally](#hosting-airflow-and-postgresql-locally)
- [Usage](#usage)
- [Airflow DAG](#airflow-dag)
- [Data Storage](#data-storage)
- [Contributing](#contributing)
- [License](#license)

## Project Overview
This project aims to extract data engineering books from Amazon, transform the data as needed, and load it into a PostgreSQL database using Apache Airflow.

## Technologies Used
- Python 3.12.7
- Apache Airflow
- PostgreSQL
- Requests (for web scraping)
- Beautiful Soup (for HTML parsing)

## Installation
1. Clone the repository:
   ```bash
   git clone https://github.com/yourusername/Airflow_Build-Amazon_books_ETL_job.git
   ```
2. Navigate to the project directory:
   ```bash
   cd Airflow_Build-Amazon_books_ETL_job
   ```
3. Create a virtual environment:
   ```bash
   python -m venv .venv
   ```
4. Activate the virtual environment:
   - For macOS/Linux:
     ```bash
     source .venv/bin/activate
     ```
   - For Windows:
     ```bash
     .venv\Scripts\activate
     ```
5. Install the required packages:
   ```bash
   pip install apache-airflow[postgres] requests beautifulsoup4
   ```

## Setup
### Using Docker
1. **Install Docker and Docker Compose**:
   - Follow the installation instructions on the [Docker website](https://docs.docker.com/get-docker/).

2. **Start Airflow and PostgreSQL**:
   - Navigate to the project directory where `docker-compose.yml` is located.
   - Start the services:
     ```bash
     docker-compose up
     ```
   - This command will set up and run Airflow along with a PostgreSQL database.

3. **Access the Airflow Web Interface**:
   - Open your web browser and go to `http://localhost:8080`.
   - The default username and password are both `airflow`.

### Without Docker (optional)
1. **Install PostgreSQL**:
   - Download and install PostgreSQL from the [official website](https://www.postgresql.org/download/).
   - Create a new database for Airflow:
     ```bash
     psql -U postgres
     CREATE DATABASE airflow_db;
     ```

2. **Initialize the Airflow Database**:
   - After creating the database, initialize Airflow:
     ```bash
     airflow db init
     ```

3. **Start Airflow**:
   - Start the Airflow web server:
     ```bash
     airflow webserver --port 8080
     ```
   - In another terminal, start the scheduler:
     ```bash
     airflow scheduler
     ```

## Creating Files
1. **Create a DAG File**:
   - Inside the project directory, create a folder named `dags` if it doesn’t exist.
   - Create a new Python file for your DAG, e.g., `amazon_books_dag.py`.

2. **Sample DAG Code**:
   - Here’s a basic structure for your DAG:
   ```python
   from airflow import DAG
   from airflow.operators.python import PythonOperator
   from datetime import datetime

   def extract():
       # Logic to extract data from Amazon
       pass

   def transform():
       # Logic to transform the data
       pass

   def load():
       # Logic to load data into PostgreSQL
       pass

   default_args = {
       'owner': 'airflow',
       'start_date': datetime(2023, 1, 1),
   }

   dag = DAG(
       'amazon_books_dag',
       default_args=default_args,
       schedule_interval='@daily',
   )

   with dag:
       extract_task = PythonOperator(task_id='extract', python_callable=extract)
       transform_task = PythonOperator(task_id='transform', python_callable=transform)
       load_task = PythonOperator(task_id='load', python_callable=load)

       extract_task >> transform_task >> load_task
   ```

## Connecting to PostgreSQL
1. **Update Connection Settings in Airflow**:
   - Go to the Airflow web interface, and under **Admin > Connections**, add a new connection.
   - Fill in the details:
     - **Connection ID**: `postgres_default`
     - **Connection Type**: `PostgreSQL`
     - **Host**: `postgres` (or `localhost` if not using Docker)
     - **Schema**: `airflow_db`
     - **Login**: `your_postgres_user`
     - **Password**: `your_postgres_password`
     - **Port**: `5432`
    


## Hosting Airflow and PostgreSQL Locally
- If you're using Docker, both Airflow and PostgreSQL will be hosted in containers, and you can access them through `http://localhost:8080` for Airflow and the configured PostgreSQL connection.
- If you're running them without Docker, ensure that both services are running and accessible on the specified ports.

## Usage
1. **Access the Airflow web interface** at `http://localhost:8080`.
2. **Trigger the DAG** from the dashboard and monitor the task execution.

## Airflow DAG
- This DAG extracts data from Amazon, transforms it, and loads it into a PostgreSQL database.
- Each task is represented as a `PythonOperator` in the DAG.

## Data Storage
- The data is stored in the PostgreSQL database `airflow_db`.
- You can define the schema for storing the book data as per your requirements.

## Screenshots

## Airflow Dashboard
![Airflow Dashboard](https://github.com/ShivaniNatani/Airflow_Build-Amazon_books_ETL_job/blob/main/image-1.png)

### PostgreSQL Schema
![PostgreSQL Schema](https://github.com/ShivaniNatani/Airflow_Build-Amazon_books_ETL_job/blob/main/image-2.png)

### Data Pipeline
![Data Pipeline](https://github.com/ShivaniNatani/Airflow_Build-Amazon_books_ETL_job/blob/main/image.png)

## Contributing
If you wish to contribute to this project, please fork the repository and create a pull request.

## License
This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
```

### Key Additions
- Detailed steps for connecting to PostgreSQL, both with and without Docker.
- Instructions for creating a simple DAG.
- Clear organization of the setup process and usage.





