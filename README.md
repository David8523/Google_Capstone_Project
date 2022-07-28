
<p align="center">
  <img src="https://raw.githubusercontent.com/labwilliam/data_analysis_projects/main/cyclistic_bike_share/scripts/logo.png" /
width="350" 
height="300"
</p>

# **Cyclistic Bike Share: Case Study**

_This document is created as part of the capstone project of the Google Data Analytics Professional Certificate._

  ## Table of Contents
1. [Introduction and Scenario](#introduction-and-scenario)
2. [ASK](#ask)
3. [Data Preparation](#data-preparation)
4. [Cleaning and Manipulation](#cleaning-and-manipulation)
5. [Analysis](#analysis)
6. [Visualization](#visualization)
7. [Recomendations](#recomendations)


## Introduction and Scenario
  ### Introduction
  In 2016, Cyclistic launched a successful bike-share offering. Since then, the program has grown to a fleet of 5,824 bicycles that are geotracked and locked into a network of 692 stations across Chicago. The bikes can be unlocked from one station and returned to any other station in the system anytime.
  ### Scenario
  You are a junior data analyst working in the marketing analyst team at Cyclistic, a bike-share company in Chicago. The director of marketing believes the company’s future success depends on maximizing the number of annual memberships. Therefore, your team wants to understand how casual riders and annual members use Cyclistic bikes differently. From these insights, your team will design a new marketing strategy to convert casual riders into annual members. But first, Cyclistic executives must approve your recommendations, so they must be backed up with compelling data insights and professional data visualizations.
## ASK
  Identify and understand the bike usage among annual members and casual riders in order to suggest marketing strategies to convert casual riders into annual members.
This comparison along with other tasks will later be used by marketing department for developing strategies aimed at converting casual riders into members

## Data Preparation
  The data that I used was the Cyclistic’s historical trip data from 2021 (Ene-2021 to Dec-2021). The data is available on this [link](https://divvy-tripdata.s3.amazonaws.com/index.html).
  ### Variables Names
* **ride_id**: Unique id of each ride trip
* **rideable_type**: Type of bicycle ride, split between 3 categories — classic, docked, and electric
* **started_at**: Date and time of the start of the trip
* **ended_at**: Date and time of the end of the trip
* **start_station_name**: Start station name
* **start_station_id**: Start station id
* **end_station_name**: Endstation name
* **end_station_id**: Endstation id
* **start_lat**: Latitude of the start location
* **start_lng**: Longitude of the start location
* **end_lat**: Latitude of the end location
* **end_lng**: Longitude of the end location
* **member_casual**: Type of membership, either casual or member

## Cleaning and manipulation
  We need to clean and manipulate the data to ensure certain quality before we proceed to the Analysis and the Visualization. The tools used in this case are **Python, Google Sheets and Tableau.**
  ### Python
  1. Import the necessary libraries
  ```
  import pandas as pd
  ```
  
  2. Merging every monthly CSV into one
  
  ```
  Cyclistic_Data_2021 = pd.concat(
    map(pd.read_csv, ['202101-divvy-tripdata.csv', '202102-divvy-tripdata.csv','202103-divvy-tripdata.csv','202104-divvy-tripdata.csv','202105-divvy-tripdata.csv','202106-divvy-tripdata.csv','202107-divvy-tripdata.csv','202108-divvy-tripdata.csv','202109-divvy-tripdata.csv','202110-divvy-tripdata.csv','202111-divvy-tripdata.csv','202112-divvy-tripdata.csv']), ignore_index=True)
  ```
  3. Changing dates columns to the correct dataframe (from Sring to Date)
  ```
  Cyclistic_Data_2021[['started_at', 'ended_at']] = Cyclistic_Data_2021[['started_at', 'ended_at']].apply(pd.to_datetime)
  ```
  4. Creating a new column with the duration of the trip
  ```
  Cyclistic_Data_2021['Duration'] = (Cyclistic_Data_2021['ended_at'] - Cyclistic_Data_2021['started_at'])
  ```
  5. Cleaning the "Type of Bike" Column
  ```
  Cyclistic_Data_2021['rideable_type'] = Cyclistic_Data_2021['rideable_type'].str.replace('_',' ')
  Cyclistic_Data_2021['rideable_type'] = Cyclistic_Data_2021['rideable_type'].str.capitalize()
  ```
  6. Creating a new column with the weekday where the trip was made
  ```
  Cyclistic_Data_2021['day_of_week'] = Cyclistic_Data_2021['started_at'].dt.day_name()
  ```
  ## Analysis
* **Overall, Casual riders take less number of ride but for longer durations**. Casual users take 16% less rides than Members but for 3x longer rides
* **Casual Riders are most active on Weekends (1.6x) and take longer rides**. Their most active on Saturday and holidays.
* **On Peak July, average duration of casual members is 3x more than members**
 ## Visualization
 I have chosen Tableau as a tool to visualize the data and share my insghts. I have made a dashboard that you can see [here](https://public.tableau.com/app/profile/david.de.la.iglesia/viz/CyclisticBikeShareCaseStudy_16590362027680/Dashboard1)
## Recomendations:
* Create collaborations with different entertainment and tourism companies to take advantage of the vacation season. These collaborations can be touristic tours around the city, group tours, etc
* Know the most popular bike stations. Understand why they are popular and try to replicate them in other neighborhoods by advertising and marketing.
* Try to encourage the use of bicycles by casual users during other vacations such as Christmas or Easter. In which their use is not too different from the rest of the year, unlike the summer.
