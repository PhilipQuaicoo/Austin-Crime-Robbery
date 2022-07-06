# Austin-Crime-Robbery

This is a dive into the Robbery crimes in Austin Texas for the years 2014 - 2016


# Introduction

Austin Texas in the years 2014 to 2016 according the the data recorded a total of 116,675 crimes of various kinds spanning from the theft and robbery to Bulglary and many others which are sub classified.
This repository takes a look at the Robbery crimes and its sub classes, and also compares the various classes in terms of years, months and days within the time period. 
The data for this project is a public data found in the bigquery public database in the bigquery console.


# Data Preparation

The data used in this project is a public data in the crime table found in the bigquery database under the austin_crime dataset. The columns used in the project are the;

unique_key: Unique identifier for the record

description: The subcategory of the primary description

primary_type: The primary description of the NIBRS/UCR code

timestamp: Time when the incident occurred. This is sometimes a best estimate

year: Indicates the year in which the incident occurred


# Processing Data

For the metrics the project seeks to explore, dropping nulls in the data will not be ncecessary.


# Analysis

The preview of the crime table data shows that there were 116,675 crimes recorded. The mails description category of crimes and its composition is as follows and selected by the following query:
![AUSTIN CRIME TYPES](https://user-images.githubusercontent.com/107520777/177533508-23ec3363-c2ab-4d89-be6f-0ffa39e42315.PNG)

```
SELECT count(unique_key) as number, primary_type 
FROM `bigquery-public-data.austin_crime.crime`
group by primary_type
order by number desc
```

Out of this, we a look at crimes under the robbery primary type which is 2,859 of the total number. Since the primary_type data each has its sub categorisation, the following query was used to check for the various sub categories (description) and its numeric composition under the robbery type.

```
select count(unique_key) as number, description
FROM `bigquery-public-data.austin_crime.crime`
where primary_type = 'Robbery'
group by description
```
![AUSTIN ROBBERY DESCRIPTION](https://user-images.githubusercontent.com/107520777/177533549-0323f5a0-5be2-4a09-8ba2-5c329f22b8e9.PNG)

The years for which the data covers as already mentioned was selected from the year column with the following query

```
select distinct(year)
FROM `bigquery-public-data.austin_crime.crime`
```

The various classes of Robbery are compared per the years to see how each class trends through the period anually. The second where statement is subtituted for the remaining years (2015 and 2016). The resulting tables are copied into google sheets and is organised to be plotted to show how each robbery class has changed through the years.

```
SELECT count(unique_key) as number, description
FROM `bigquery-public-data.austin_crime.crime`
where primary_type = 'Robbery' and year = 2014
group by description
```

Again the robbery types are compared to each other in terms of the months of the year. The query selects the monthly comparison for each robbery type as they are being subtituted into the where statement in the using the wildcards. Likewise, the resulting table for each robbery is copied into google sheets and then organised and sorted to be in order so and then plotted.

```
select distinct(FORMAT_DATE("%B", timestamp)) as Months, count(unique_key) as number
FROM `bigquery-public-data.austin_crime.crime`
where description like 'ROBBERY BY ASSAULT%'
group by Months
```

Finally the robbery classes were compared on terms of days of the week. This following query selects the week days compilation of each robery description and then all are copied into google sheets and prepared to be plotted to show the desired trend.

```
select distinct(FORMAT_DATE("%A", timestamp)) as days, count(unique_key) as number
FROM `bigquery-public-data.austin_crime.crime`
where description like 'ROBBERY BY ASSAULT%'
group by days
```


# Visualisation








