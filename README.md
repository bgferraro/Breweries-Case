 Breweries Case Inbev 
==================================

This repository contains the DAG code used in the [Case Inbev - breweries using Databricks notebooks with medallion architecture in pipelined to data]

## How the model was built

Pipelined was built by ingesting the website (<https://www.openbrewerydb.org/>) that provides data from the breweries.
The medallion model was used, which uses layers (bronze, silver and gold). Developed in notebooks on Databricks (.iypnb) 
The start is carried out by Airflow and all of this was containerized in docker to provide all files via gitHub.
The language considered was pyspark with delta tables to provide logs

This application runs this repository with Airflow.
Containerization of the Databricks with Airflow application to provide synchronization and activation of notebooks.
You need to add in `.env` and add your own credentials. 
The code used in the Databricks notebooks is available in the `databricks_notebook_code` folder.

## Using this Application

Run this Airflow project without installing anything locally.

1. Fork this repository.
2. Create a new GitHub codespaces project on your fork. Make sure it uses at least 2 colors!
3. Once the Airflow project has started, access the Airflow UI by clicking on the **Ports** tab and opening the forward URL for port 8080.
4. The Dag Scripts will trigger the medallion architecture notebooks and jobs will be created.
5. Monitoring will be possible to check directly in Databricks

## Resources / Monitoring / Alerts 

1. The Cluster used has the configuration below
   ![image](https://github.com/user-attachments/assets/cab0aa73-f0a5-42bb-8e15-a97e38390651)

2. All failure monitoring and alerting is carried out internally in Databricks where we can see from the execution history which job error occurred and check the details, lines and causes directly in Databricks.
   ![image](https://github.com/user-attachments/assets/3a74e88e-3bcf-4095-9b26-01a0a6b48930)

3. It is also possible to look at the execution of each job through the Spark UI to identify partitioning, parallel processes execution time problems in the Spark Dags and Catalyst Optimizer in more detail.
![image](https://github.com/user-attachments/assets/adca78e7-ebdd-46df-a1d8-9e69269c0015)


2. In case of errors, the execution can be repeated according to the existing configuration and if there is an error again, a deeper validation will need to be carried out to overcome whether it is related to the code or not for a manual execution.
In case of failures, the document can also help with recovery https://docs.databricks.com/pt/jobs/repair-job-failures.html

