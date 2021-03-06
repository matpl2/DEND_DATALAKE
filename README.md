# DEND Data Lake Project
This file is a documentation file for the exercise performed as a part of Data Engineer NanoDegree Project - Data Lake. 

Purpose of this project is to build an ETL pipeline for a data lake hosted on S3. 


## Files
This project includes following files:
 - dl.cfg 
 - etl.py 

 
Dl.cfg is a configuration file that stores AWS Credential.
Etl.py is python execution files that process data from S3 and after ETL process write them to parquet files on S3.


## Data sets
There are two datasets used in this project that reside in S3. Here are the S3 links for each:

Song data: s3://udacity-dend/song_data
Log data: s3://udacity-dend/log_data

Song Dataset
The first dataset is a subset of real data from the Million Song Dataset. Each file is in JSON format and contains metadata about a song and the artist of that song. 

Log Dataset
The second dataset consists of log files in JSON format generated by this event simulator based on the songs in the dataset above. These simulate app activity logs from an imaginary music streaming app based on configuration settings.

## EMR instance
For the purpose of this project it is necessary to create EMR instance. For my work I have created EMR cluster with 3 m3.xlarge nodes i the defalut VPC. In such config it was necessary to configure VPC components to get access to EMR (editing Security group for public access, attaching subnets to IGW). 

EMR instance used in this excercise:
![alt text](https://github.com/matpl2/DEND_DATALAKE/blob/main/pict/emr.png)

## Tables
Using the song and event datasets, I have created a star schema optimized for queries on song play analysis. This includes the following tables.

Fact Table
1. songplays - records in event data associated with song plays i.e. records with page NextSong
   * songplay_id, start_time, user_id, level, song_id, artist_id, session_id, location, user_agent
   
Dimension Tables
1. users - users in the app
   * user_id, first_name, last_name, gender, level
   
2. songs - songs in music database
   * song_id, title, artist_id, year, duration
   
3. artists - artists in music database
    * artist_id, name, location, lattitude, longitude
    
4. time - timestamps of records in songplays broken down into specific units
    * start_time, hour, day, week, month, year, weekday
    

This star schema would be the most optimal for the analytics team. Also, because orginal dataset is in S3 the most efficient way for ETL process was to use Spark on EMR to transofrm data.
