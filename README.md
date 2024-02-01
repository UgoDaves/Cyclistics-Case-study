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
#### - first you have to create tables.
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
### Combine and create new table with all datesets called 'allmonths.'
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
