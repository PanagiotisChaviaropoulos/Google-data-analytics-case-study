# Google-data-analytics-case-study
## Summary
In this project I am working for a fictional company named Cyclistic along with some other key team members, and I will be performing several junior data analyst real life tasks to adress the business problem.
In order to answer the business questions, I will utilize the six steps of the data analysis process: Ask, Prepare, Process, Analyze, Share and Act.
## Company information
In 2016, Cyclistic launched a successful bike-share offering. Since then, the program has grown to a fleet of 5,824 bicycles that are geotracked and locked into a network of 692 stations across Chicago. 
Cyclistic sets itself apart by also offering reclining bikes, hand tricycles, and cargo bikes, making bike-share more inclusive to people with disabilities and riders who can’t use a standard two-wheeled bike. The majority of riders opt for traditional bikes; about 8% of riders use the assistive options. Cyclistic users are more likely to ride for leisure, but about 30% use the bikes to commute to work each day.

Customers who purchase single-ride or full-day passes are referred to as casual riders. Customers who purchase annual memberships are Cyclistic members. Cyclistic’s finance analysts have concluded that annual members are much more profitable than casual riders. The director of marketing (Moreno) has set a clear goal: Design marketing strategies aimed at converting casual riders into annual members. In order to do that, however, the team needs to better understand how annual members and casual riders differ.

## Scenario
Let's assume I am a junior data analyst working on the marketing analyst team at Cyclistic. The director of marketing believes the company’s future success depends on maximizing the number of annual memberships. Therefore, our team wants to understand how casual riders and annual members use Cyclistic bikes differently. From these insights, the team will design a new marketing strategy to convert casual riders into annual members. But first, Cyclistic executives must approve the recommendations, so they must be backed up with compelling data insights and professional data visualizations.

## Ask
The director of marketing, Moreno has assigned me to answer the question: How do annual members and casual riders use Cyclistic bikes differently?
### Business task
Determine how to maximize annual memberships by converting casual riders to members. 

## Prepare
The data I will use are the historical trip data from January 2023 to December 2023 and it can be found and downloaded from [divvy_tripdata](https://divvy-tripdata.s3.amazonaws.com/index.html).
There are 12 files one for each month of 2023 and each file contains 13 columns named ride_id, rideable_type, started_at, ended_at, start_station_name, start_station_id, end_station_name, end_station_id, start_lat, start_lng, end_lat, end_lng and member_casual.
The data has been made available by Motivate International Inc. under this [licence](https://divvybikes.com/data-license-agreement). However due to data-privacy issues I can't use riders’ personally identifiable information. This means that I won’t be able to connect pass purchases to credit card numbers to determine if casual riders live in the Cyclistic service area or if they have purchased multiple single passes.

## Process
In order to combine, clean and analyze the data I will use BigQuery because the size of the files is too big for spreadsheets to handle and even if it could, it would take a substantial amount of time.
### Data combination
First I created a dataset named 2023_biketrips. In that dataset I created 12 tables, one for each month, and I uploaded all the csv files. Then I combined all the tables in a unified one containing all the data from 2023. From the details in the new table we see that there are 5.719.877 rows.
### Data cleaning
Now I need to clean my new table in order to be ready for my analysis. The steps I use to determine how to clean my table are the following.
1. I run a Query to determine the number of null values in each column. The following table shows the results.
   
   ![null_values](https://github.com/user-attachments/assets/180c8d26-750c-4cd9-8f19-14fd5b8f2656)
2. I want to check if there are any duplicate rows in order to remove them. After I run the appropriate Query I determine that there are not any duplicate rows.
3. I notice that all the values in the ride_id column have a length of 16 as shown in the table below. So there are no mistakes there.

   ![length_ride_id](https://github.com/user-attachments/assets/92b28384-f90b-40de-adfd-5633edb4d4c1)
4. The different types of bikes are three as shown below.

  ![types_of_bikes](https://github.com/user-attachments/assets/38e77784-7d0b-4832-8163-c8ea90759cc0)
  
5. From the columns started_at and ended_at I can create two new helpful columns ride_length and day_of_week that will help in the analysis.
6. In the new column ride_length I want to remove too short trips (under a minute) to get rid of irrelvant to the analysis trips, and negative trips (trips where the started_at column is later than the ended_at column) which is a mistake in the entry.
7. The columns start_station_id, end_station_id, start_lat, start_lng, end_lat, end_lng will not add anything to the analysis, so I need to remove them.
8. There are 875.716 missing values in the start_station_name and 929.202 missing values in the end_station_name, so the respective rows need to be removed.

## Analyze
Now it is time to perform my analysis on the clean table. In order to identify trends and patterns I will query the following.
1. The minimum, maximum and average ride_length for members and casuals.
2. The number of rides by each type of bike for members and casuals.
3. The number of trips per day of week.
4. The number of trips per hour.
5. The average ride_length per day.
