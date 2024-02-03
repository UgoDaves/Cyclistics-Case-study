![banner](https://github.com/UgoDaves/Cyclistics-Case-study-with-SQL/assets/152723434/f2dd4369-08dc-4df4-ae61-e2a96fcc3346)

# Cyclistics Case-study with SQL
Cyclistics, a Chicago based bike-share company consisting of a fleet of over 5,800 bicycles and 600 docking stations, is seeking avenues to enhance company growth. The focus is on developing marketing strategies aimed at transitioning casual members into annual members as a means to boost overall membership and engagement.

## Ask phase
In my capacity as the data analyst within the team, I have been assigned the responsibility of comprehending the distinctive behaviors of annual members and casual riders in their utilization of Cyclistic's services. This analysis aims to provide insights into the divergent patterns of usage, ultimately contributing to answering the overarching business question of how to optimize and increase the number of annual memberships within the company.

## Prepare Phase
- Discription of all data used:
  Here is a [link](https://divvy-tripdata.s3.amazonaws.com/index.html) to the dataset. You can also access its license [here](https://divvybikes.com/data-license-agreement).
  This is an original public dataset, updated monthly consisting of therteen columns (ride_id, rideable_type, started_at, ended_at, start_station_name, start_station_id, end_station_name, end_station_id, start_lat	start_lng, end_lat, end_lng, member_casual)
![image](https://github.com/UgoDaves/Cyclistics-Case-study-with-SQL/assets/152723434/453bea36-77ae-4322-a098-cae31b18970a)

## Process Phase
- In the process of data preparation, I employed Microsoft Excel to eliminate columns containing latitude, longitude, and station information, as they were deemed irrelevant to my analysis. Additionally, the station column contained null values, prompting its exclusion from the dataset.
- I also created primary keys in all twelve dataset for the ease of joins in sql, and data modeling in power BI for visualization.

### Dataset importation into postgresql
#### - first I created tables of coresponding dataset files, in order to import into postgresql.
``` sql
CREATE DATABASE cyclistic;

CREATE TABLE january (
	jan_ride_id INT PRIMARY KEY,
	rideable_type VARCHAR(15),
	started_at TIMESTAMP,
	ended_at TIMESTAMP,
	member_casual VARCHAR(10)
);

CREATE TABLE february (
	feb_ride_id TEXT PRIMARY KEY,
	jan_ride_id INT REFERENCES january(jan_ride_id),
	rideable_type VARCHAR(15),
	started_at TIMESTAMP,
	ended_at TIMESTAMP,
	member_casual VARCHAR(20)
);

CREATE TABLE march (
	feb_ride_id TEXT REFERENCES february (feb_ride_id),
	jan_ride_id INT REFERENCES january(jan_ride_id),
	march_ride_id TEXT PRIMARY KEY,
	rideable_type VARCHAR(15),
	started_at TIMESTAMP,
	ended_at TIMESTAMP,
	member_casual VARCHAR(20)
);

CREATE TABLE april (
	feb_ride_id TEXT REFERENCES february (feb_ride_id),
	jan_ride_id INT REFERENCES january(jan_ride_id),
	march_ride_id TEXT REFERENCES march(march_ride_id),
	april_ride_id TEXT PRIMARY KEY,
	rideable_type VARCHAR(15),
	started_at TIMESTAMP,
	ended_at TIMESTAMP,
	member_casual VARCHAR(20)
);

CREATE TABLE may (
	feb_ride_id TEXT REFERENCES february (feb_ride_id),
	jan_ride_id INT REFERENCES january(jan_ride_id),
	march_ride_id TEXT REFERENCES march(march_ride_id),
	april_ride_id TEXT REFERENCES april(april_ride_id),
	may_ride_id TEXT PRIMARY KEY,
	rideable_type VARCHAR(15),
	started_at TIMESTAMP,
	ended_at TIMESTAMP,
	member_casual VARCHAR(20)
);

CREATE TABLE june (
	feb_ride_id TEXT REFERENCES february (feb_ride_id),
	jan_ride_id INT REFERENCES january(jan_ride_id),
	march_ride_id TEXT REFERENCES march(march_ride_id),
	april_ride_id TEXT REFERENCES april(april_ride_id),
	may_ride_id TEXT REFERENCES may(may_ride_id),
	june_ride_id TEXT PRIMARY KEY,
	rideable_type VARCHAR(15),
	started_at TIMESTAMP,
	ended_at TIMESTAMP,
	member_casual VARCHAR(20)
);

CREATE TABLE july (
	feb_ride_id TEXT REFERENCES february (feb_ride_id),
	jan_ride_id INT REFERENCES january(jan_ride_id),
	march_ride_id TEXT REFERENCES march(march_ride_id),
	april_ride_id TEXT REFERENCES april(april_ride_id),
	may_ride_id TEXT REFERENCES may(may_ride_id),
	june_ride_id TEXT REFERENCES june(june_ride_id),
	july_ride_id TEXT PRIMARY KEY,
	rideable_type VARCHAR(15),
	started_at TIMESTAMP,
	ended_at TIMESTAMP,
	member_casual VARCHAR(20)
);

CREATE TABLE august (
	feb_ride_id TEXT REFERENCES february (feb_ride_id),
	jan_ride_id INT REFERENCES january(jan_ride_id),
	march_ride_id TEXT REFERENCES march(march_ride_id),
	april_ride_id TEXT REFERENCES april(april_ride_id),
	may_ride_id TEXT REFERENCES may(may_ride_id),
	june_ride_id TEXT REFERENCES june(june_ride_id),
	july_ride_id TEXT REFERENCES july(july_ride_id),
	aug_ride_id TEXT PRIMARY KEY,
	rideable_type VARCHAR(15),
	started_at TIMESTAMP,
	ended_at TIMESTAMP,
	member_casual VARCHAR(20)
);

CREATE TABLE september (
	feb_ride_id TEXT REFERENCES february (feb_ride_id),
	jan_ride_id INT REFERENCES january(jan_ride_id),
	march_ride_id TEXT REFERENCES march(march_ride_id),
	april_ride_id TEXT REFERENCES april(april_ride_id),
	may_ride_id TEXT REFERENCES may(may_ride_id),
	june_ride_id TEXT REFERENCES june(june_ride_id),
	july_ride_id TEXT REFERENCES july(july_ride_id),
	aug_ride_id TEXT REFERENCES august(aug_ride_id),
	sep_ride_id TEXT PRIMARY KEY,
	rideable_type VARCHAR(15),
	started_at TIMESTAMP,
	ended_at TIMESTAMP,
	member_casual VARCHAR(20)
);

CREATE TABLE october (
	feb_ride_id TEXT REFERENCES february (feb_ride_id),
	jan_ride_id INT REFERENCES january(jan_ride_id),
	march_ride_id TEXT REFERENCES march(march_ride_id),
	april_ride_id TEXT REFERENCES april(april_ride_id),
	may_ride_id TEXT REFERENCES may(may_ride_id),
	june_ride_id TEXT REFERENCES june(june_ride_id),
	july_ride_id TEXT REFERENCES july(july_ride_id),
	aug_ride_id TEXT REFERENCES august(aug_ride_id),
	sep_ride_id TEXT REFERENCES september(sep_ride_id),
	october_ride_id TEXT PRIMARY KEY,
	rideable_type VARCHAR(15),
	started_at TIMESTAMP,
	ended_at TIMESTAMP,
	member_casual VARCHAR(20)
);

CREATE TABLE november (
	feb_ride_id TEXT REFERENCES february (feb_ride_id),
	jan_ride_id INT REFERENCES january(jan_ride_id),
	march_ride_id TEXT REFERENCES march(march_ride_id),
	april_ride_id TEXT REFERENCES april(april_ride_id),
	may_ride_id TEXT REFERENCES may(may_ride_id),
	june_ride_id TEXT REFERENCES june(june_ride_id),
	july_ride_id TEXT REFERENCES july(july_ride_id),
	aug_ride_id TEXT REFERENCES august(aug_ride_id),
	sep_ride_id TEXT REFERENCES september(sep_ride_id),
	october_ride_id TEXT REFERENCES october(oct_ride_id),
	nov_ride_id TEXT PRIMARY KEY,
	rideable_type VARCHAR(15),
	started_at TIMESTAMP,
	ended_at TIMESTAMP,
	member_casual VARCHAR(20)
);

ALTER TABLE october
RENAME COLUMN october_ride_id TO oct_ride_id

CREATE TABLE december (
	feb_ride_id TEXT REFERENCES february (feb_ride_id),
	jan_ride_id INT REFERENCES january(jan_ride_id),
	march_ride_id TEXT REFERENCES march(march_ride_id),
	april_ride_id TEXT REFERENCES april(april_ride_id),
	may_ride_id TEXT REFERENCES may(may_ride_id),
	june_ride_id TEXT REFERENCES june(june_ride_id),
	july_ride_id TEXT REFERENCES july(july_ride_id),
	aug_ride_id TEXT REFERENCES august(aug_ride_id),
	sep_ride_id TEXT REFERENCES september(sep_ride_id),
	october_ride_id TEXT REFERENCES october(oct_ride_id),
	nov_ride_id TEXT REFERENCES november(nov_ride_id),
	dec_ride_id TEXT PRIMARY KEY,
	rideable_type VARCHAR(15),
	started_at TIMESTAMP,
	ended_at TIMESTAMP,
	member_casual VARCHAR(20)
);
```
### I Combined and created new tables with all datesets called 'allmonths.'
``` sql
CREATE TABLE allmonths AS 
SELECT * FROM (
SELECT rideable_type, started_at, ended_at, member_casual FROM january
UNION ALL
SELECT rideable_type, started_at, ended_at, member_casual FROM february
UNION ALL
SELECT rideable_type, started_at, ended_at, member_casual FROM march
UNION ALL
SELECT rideable_type, started_at, ended_at, member_casual FROM april
UNION ALL
SELECT rideable_type, started_at, ended_at, member_casual FROM may
UNION ALL
SELECT rideable_type, started_at, ended_at, member_casual FROM june
UNION ALL
SELECT rideable_type, started_at, ended_at, member_casual FROM july
UNION ALL
SELECT rideable_type, started_at, ended_at, member_casual FROM august
UNION ALL
SELECT rideable_type, started_at, ended_at, member_casual FROM september
UNION ALL
SELECT rideable_type, started_at, ended_at, member_casual FROM october
UNION ALL
SELECT rideable_type, started_at, ended_at, member_casual FROM november
UNION ALL
SELECT rideable_type, started_at, ended_at, member_casual FROM december
);

SELECT * FROM allmonths
-- A total off 5719877
```
### I Created new tables with columns: day_of_week, ride_length and seasons
``` sql
CREATE TABLE allmonths1 AS
SELECT * FROM (
SELECT
member_casual,
rideable_type,
started_at,
ended_at,
ended_at - started_at AS ride_lenght,
CASE
	WHEN EXTRACT(dow from started_at) = 0 THEN 1
	WHEN EXTRACT(dow from started_at) = 1 THEN 2
	WHEN EXTRACT(dow from started_at) = 2 THEN 3
	WHEN EXTRACT(dow from started_at) = 3 THEN 4
	WHEN EXTRACT(dow from started_at) = 4 THEN 5
	WHEN EXTRACT(dow from started_at) = 5 THEN 6
	ELSE 7
END AS day_of_week,
case
	WHEN started_at BETWEEN '2023-03-19' AND '2023-06-21' THEN 'spring'
	WHEN started_at BETWEEN '2023-06-20' AND '2023-09-24' THEN 'summer'
	WHEN started_at BETWEEN '2023-09-23' AND '2023-12-22' THEN 'fall'
	ELSE 'winter'
END AS seasons
FROM allmonths
);
```
### Lastly, I imported the Cyclistic database into PowerQuery & PowerBi for analysis


## Analyze Phase
- During the analysis phase, I identified instances in the "ride_length" column where entries exceeded the 24-hour threshold, which represents the maximum duration for bike usage in a single day. To address this, I removed rows containing ride lengths exceeding the 24-hour mark. Additionally, I converted the "ride_length" values into minutes to facilitate a more straightforward analysis.
```sql
-- Removed rows above the 24hr mark
CREATE TABLE allmonths2 AS
SELECT * FROM(
SELECT *
FROM allmonths1
WHERE ride_length < '1 day'
ORDER BY ride_length Desc
);

-- Created a column for ride lenght in minutes 'time_in_min'
SELECT 
member_casual,
rideable_type,
DATE(started_at),
ride_length,
EXTRACT(hour from ride_length)*60 + extract(minute from ride_length) AS time_in_min
FROM allmonths2
ORDER BY 5 DESC;
```
- Upon analyzing the 'time_in_min' column in Power Query, I observed instances where the values were negative, indicating inconsistencies in the associated 'started' and 'ended' columns. Consequently, I opted to remove these discrepancies by deleting the corresponding rows. I also deleted rows with a zero value.

### The total number of members who use Cyclistic bikes outweight the number of casual users by over 1.5 million and ass seen from the stacked barchart, the highest number of rides can be found in the summer, follwed by spring. the least amount of rides are in the winter
<img width="255" alt="totalnumberofrides" src="https://github.com/UgoDaves/Cyclistics-Case-study-with-SQL/assets/152723434/8686f25b-e062-49b1-91ec-580fa72ff3c5">
<img width="261" alt="ridesbyseason" src="https://github.com/UgoDaves/Cyclistics-Case-study-with-SQL/assets/152723434/0a827905-82ad-4316-af23-763cc05224e6">
