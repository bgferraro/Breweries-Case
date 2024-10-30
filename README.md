Breweries Case Inbev 
==================================

This repository contains the DAG code used in the [Case Inbev - breweries using Databricks notebooks with medallion architecture in pipelined to data]

# How the model was built

Pipelined was built by ingesting the website (<https://www.openbrewerydb.org/>) that provides data from the breweries.
The medallion model was used, which uses layers (bronze, silver and gold). Developed in notebooks on Databricks (.iypnb) 
The start is carried out by Airflow and all of this was containerized in docker to provide all files via gitHub
The language considered was pyspark with delta tables to provide logs

This application runs this repository with Airflow.
Containerization of the Databricks with Airflow application to provide synchronization and activation of notebooks 
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

1. All failure monitoring and alerting is carried out internally in Databricks where we can see from the execution history which job error occurred and check the details, lines and causes directly in Databricks.
2. It is also possible to look at the execution of each job through the Spark UI to identify partitioning, slowness and execution time problems in the Spark Dags and Catalyst Optimizer in more detail.
3. In case of errors, the execution can be repeated according to the existing configuration and if there is an error again, a deeper validation will need to be carried out to overcome whether it is related to the code or not for a manual execution.
In case of failures, the document can also help with recovery https://docs.databricks.com/pt/jobs/repair-job-failures.html

