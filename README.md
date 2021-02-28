# Dataware House project

## Introduction
A music streaming startup, Sparkify, has grown their user base and song database and want to move their processes and data onto the cloud. Their data resides in S3, in a directory of JSON logs on user activity on the app, as well as a directory with JSON metadata on the songs in their app.

## Data & Files 

### DATA
The data that will be loaded from S3 resides here:
Song data: `s3://udacity-dend/song_data`
Log data: `s3://udacity-dend/log_data`
Log data json path: `s3://udacity-dend/log_data`

The first dataset is a subset of real data from the Million Song Dataset. Each file is in JSON format and contains metadata about a song and the artist of that song. The files are partitioned by the first three letters of each song's track ID. For example, here are filepaths to two files in this dataset.

Typical example of the data:
```{"num_songs": 1, "artist_id": "ARJIE2Y1187B994AB7", "artist_latitude": null, "artist_longitude": null, "artist_location": "", "artist_name": "Line Renaud", "song_id": "SOUPIRU12A6D4FA1E1", "title": "Der Kleine Dompfaff", "duration": 152.92036, "year": 0}```

The second dataset consists of log files in JSON format generated by this event simulator based on the songs in the dataset above. These simulate app activity logs from an imaginary music streaming app based on configuration settings.

### Python Files
- create_tables.py: this python file creates the tables that are required to load and ingest the data into the redshift database
- etl.py: this python file performs the ETL. Firstly the data is being inserted into staging tables. After this is done the data is inserted into the fact and dimension tables created as part of create_tables.py

## Schema for Song Play Analysis
In this section the schema's for the database are explained. 

### Fact Table
1. songplays - records in log data associated with song plays i.e. records with page `NextSong`
   - `songplay_id`, `start_time`, `user_id`, `level`, `song_id`, `artist_id`, `session_id`, `location`, `user_agent`

### Dimension Tables
2. users - users in the app
   - `user_id`, `first_name`, `last_name`, `gender`, `level`
3. songs - songs in music database
   - `song_id`, `title`, `artist_id`, `year`, `duration`
4. artists - artists in music database
   - `artist_id`, `name`, `location`, `latitude`, `longitude`
5. time - timestamps of records in songplays broken down into specific units
   - `start_time`, `hour`, `day`, `week`, `month`, `year`, `weekday`
