# Project 4: Data Lake with Apache Spark (etl-data-lake-spark) 

## Introduction  
This project is designed for a music streaming startup, **Sparkify**, to transition from a traditional data warehouse to a **data lake**. An **ETL pipeline** is developed to extract raw data from **Amazon S3**, transform it using **Apache Spark**, and load the processed data back into **S3** in the form of **dimensional tables**.  

With this new structure, Sparkify’s analytics team can efficiently analyze user activity and gain insights into listening behavior.  

## Dataset  
The project uses two datasets hosted in public **S3 buckets**:  
- **Song data**: Contains metadata about songs and artists.  
- **Log data**: Contains user activity records, such as song play events.  

Both datasets are stored as **JSON files**.  

## Database Schema  
A **star schema** is implemented to optimize queries related to song play analysis.  

![schema](/images/schema.png)  

### Fact Table  
- **songplays** → records of song play events (only where the page action is `NextSong`).  

### Dimension Tables  
- **users** → app users.  
- **songs** → song details.  
- **artists** → artist information.  
- **time** → timestamps of songplays broken down into units (hour, day, week, month, year, weekday).  

## Spark ETL Process  
The ETL pipeline is structured as follows:  

1. **Process Song Data**  
   - Read song files.  
   - Extract and load data into **songs** and **artists** tables.  

2. **Process Log Data**  
   - Read log files.  
   - Filter records where the event is `NextSong`.  
   - Extract user and time information.  
   - Load data into **users**, **time**, and **songplays** tables.  

All tables are stored in **Parquet format** and partitioned for optimized querying.  

## Project Structure  
- **etl.py** → ETL script that reads data from S3, processes it with Spark, and writes it back to S3.  
- **dl.cfg** → Configuration file containing AWS credentials and S3 details.  
- **test.ipynb** → Jupyter Notebook for testing the ETL pipeline.  

## How to Run the Project  

1. **Install dependencies**  
   Make sure you have:  
   - Python 3.6+  
   - Apache Spark  
   - Hadoop AWS package  

2. **Set up AWS credentials**  
   Update the `dl.cfg` file with your AWS Access Key and Secret Key:  
   ```ini
   [AWS]
   AWS_ACCESS_KEY_ID=YOUR_KEY
   AWS_SECRET_ACCESS_KEY=YOUR_SECRET
