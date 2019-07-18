# Data Pipelines in Airflow

## Summary
* [Problem to solve](#Problem-to-solve)
* [Apache Airflow](#Apache-Airflow)
* [Technology Stack](#Technology-Stack)
* [Data Quality Checks](#Data-Quality-Checks)
* [Description of particular scripts](#Description-of-particular-scripts)
* [How to run?](#How-to-run)
--------------------------------------------

#### Problem to solve
A music streaming company has decided that it is time to introduce more automation and monitoring to their data warehouse ETL pipelines. Due to some human mistakes and analysis based on incomplete data, additional validation checks are necessary to bring trust to both to team of analysts and higher management.  

#### Apache Airflow
Airflow was originally developed by Airbnb to manage their data based operations with a fast growing data set. Airflow is undergoing incubation at Apache Software foundation as Airbnb have decided to open source it under Apache certification. Apache airflow makes work flow much simpler and organised by allowing you to divide it into small independent (if possible) task units. Easy to organise and easy to schedule ones.

#### Technology Stack
1. Data is stored in `AWS S3` (Amazon Simple Storage Service) in JSON files:
- log data: s3://udacity-dend/log_data
- song data: s3://udacity-dend/song_data
2. Data is transfered into `Redshift` staging tables and copied to prepared for analysis in `facts` and `dimensions` tables. 
3. The whole pipeline is automated in `Apache Airflow`.
4. `Python 3` serves as a bridge to communicate between AWS services and execute SQL queries.

#### Data Quality Checks
To not let the situation with incomplete data happen again after every execution data checks are performed. If execution of the dag results in no added rows, error will be yieled with appropriate information in logs. 

#### Description of particular scripts
- `create_tables.sql` - Contains the DDL (the structure) for all tables used in this projecs
- `udac_example_dag.py` - The main DAG configuration file to execute in Airflow web UI
- `stage_redshift.py` - Operator to read files from S3 and load into Redshift staging tables
- `load_fact.py` - Operator to load the fact table in Redshift
- `load_dimension.py` - Operator to read from staging tables and load the dimension tables in Redshift
- `data_quality.py` - Operator for data quality checking

#### How to run?
After proper configuration of AWS Redshift service and installing Apache on the machine it's enough to run the pipeline in Airflow web interface under local address: http://localhost:8080 . 

