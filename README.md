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






