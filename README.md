# Austin-Crime-Robbery

This is a dive into the Robbery crimes in Austin Texas for the years 2014 - 2016


# Introduction

Austin Texas in the years 2014 to 2016 according the data recorded a total of 116,675 crimes of various kinds spanning from the theft and robbery to Burglary and many others which are sub classified.
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

For the metrics the project seeks to explore, dropping nulls in the data will not be necessary.


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

The various classes of Robbery are compared per the years to see how each class trends through the period annually. The second where statement is substituted for the remaining years (2015 and 2016). The resulting tables are copied into google sheets and is organised to be plotted to show how each robbery class has changed through the years.

```
SELECT count(unique_key) as number, description
FROM `bigquery-public-data.austin_crime.crime`
where primary_type = 'Robbery' and year = 2014
group by description
```

Again the robbery types are compared to each other in terms of the months of the year. The query selects the monthly comparison for each robbery type as they are being substituted into the where statement in the using the wildcards. Likewise, the resulting table for each robbery is copied into google sheets and then organised and sorted to be in order so and then plotted.

```
select distinct(FORMAT_DATE("%B", timestamp)) as Months, count(unique_key) as number
FROM `bigquery-public-data.austin_crime.crime`
where description like 'ROBBERY BY ASSAULT%'
group by Months
```

Finally the robbery classes were compared on terms of days of the week. This following query selects the weekday’s compilation of each robbery description and then all are copied into google sheets and prepared to be plotted to show the desired trend.

```
select distinct(FORMAT_DATE("%A", timestamp)) as days, count(unique_key) as number
FROM `bigquery-public-data.austin_crime.crime`
where description like 'ROBBERY BY ASSAULT%'
group by days
```


# Visualisation

As the various resulting tables were selected, copied into google sheets and organises to be plotted, these were the various plots that was generated.

_**Various classes of Robbery crime**_

![AUSTIN ROBBERY CRIMES CLASSES, 2014 - 2016](https://user-images.githubusercontent.com/107520777/177555724-665e8b2c-277f-4e72-85eb-63cc8e2f74f6.png)
![AUSTIN ROBBERY DESCRIPTION](https://user-images.githubusercontent.com/107520777/177555800-fcf794ed-d26f-4e2f-8396-05c78534b305.PNG)


**_The change in various robbery types over the years_**

![AUSTIN ROBBERY CRIMES CATEGORY, 2014 - 2016](https://user-images.githubusercontent.com/107520777/177556263-2cef3ff5-3fef-4597-bfce-5e96e835e428.png)


_**Comparing the robberies to each other based on the months of the years.**_

![AUSTIN ROBBERY CRIME PER MONTH, 2014 - 2016](https://user-images.githubusercontent.com/107520777/177556516-4b6216a1-83e7-462b-9ac4-f4d4b2e9ce3a.png)

_**The variation in robbery types when compared based on the days of the week**_

![AUSTIN ROBBERY CRIME BY WEEKDAYS, 2014 - 2016](https://user-images.githubusercontent.com/107520777/177556723-b9f66133-74bd-4694-93b8-01b00fdf1281.png)


# Insights

1. Out of 2859 Robbery cases reported on the period, the highest of all the robberies happen to be AGG ROBBERY/DEADLY WEAPON with a little over 50% of the total number whiles AGG ROBBERY BY ASSAULT occurred the least with less than 5% of the total. Though ROBBERY BY ASSAULT also has a high number, instance of aggravation in the Assault robberies were low
2. Comparing the robberies to identify their annual trends, it is seen that AGG ROBBERY/DEADLY WEAPON significantly increased through the years unlike the other types where the variation through the years were not as significant. This could be due to the fact that security agencies might have lost their touch as to ways to apprehend the situation.
3. Generally seasonal cases show that the winter season which is mostly a holiday has a relatively lower value than other seasons. This could be due to the fact that people are home most often and so suspects less likely plan robberies.
4. There is a similar trend through the days for the AGG ROBBERY/DEADLY WEAPON and ROBBERY BY ASSAULT crimes. They all show a rising trend starting during the midweek through to the weekend whiles ROBBERY BY THREAT and AGG ROBBERY BY ASSAULT appears to be on an almost steady trend through the days.


# Recommendations

1. It is recommended that the security forces study cases of AGG ROBBERY/DEADLY WEAPON and identify what they are failing to do that is causing the rise in the numbers annually.
2. Seasonally unlike the holiday season that shows a relatively low number of cases as compared to the other seasons, the security forces can beef up their security tactics so as to alleviate the crimes in the other seasons. As shown on the daily comparison chart, the greater number of crimes starts to increase into the weekend from the late midweeks, thus security forces are here by advised to increase security over areas where such crimes are mostly reported.
















