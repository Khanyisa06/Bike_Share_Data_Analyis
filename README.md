# Bike_Share_Data_Analyis

Welcome to the Cyclistic bike-share analysis case study! In this case study,I perform many real-world tasks of a junior data
analyst. I work for a fictional company, Cyclistic, and meet different characters and team members. In order to answer the
key business questions, I follow the steps of the data analysis process: **ask, prepare, process, analyze, share, and act**.
 
- I will work in the marketing analyst team at Cyclistic , a bike-share company in Chicago as a junior data analyst .
- As a team we have to understand how casual riders and annual members use Cyclistic bikes differently.
- From these insights, design a new marketing strategy to convert casual riders into annual members.
 
 ## *Table of Contents*
 
  2. [Project Objectives](#project-objectives)
  3. [Data Sources](#data-sources)
  4. [Project Tools](#project-tools)
  5. [Data cleaning](#data-cleaning)
  6. [Exploratory Data Analysis](#exploratory-data-analysis)
  7. [Data Analysis](#data-analysis)
  8. [Findings](#findings)
  9. [Recommendation](#recommendation)
  10. [Limitations](#limitations)
  11. [References](#references)

## Objectives

__*Produce a report with the following deliverables:*__

1. A clear statement of the business task
2. A description of all data sources used
3. Documentation of any cleaning or manipulation of data
4. A summary of your analysis
5. Supporting visualizations and key findings
6. Your top three recommendations based on your analysis
 
## Business Task

The primary business task is to understand how casual riders and annual members use Cyclistic bikes differently. As a junior data analyst in the marketing team, the goal is to gather insights that will inform the development of a targeted marketing strategy. The overarching objective is to maximize the number of annual memberships(convert casual riders into annual members), as identified by the director of marketing. 

To achieve this, the data analysis process will be followed, encompassing key steps such as asking relevant questions, preparing and processing the data, conducting a thorough analysis, and ultimately sharing actionable insights. The success of the proposed marketing strategy hinges on obtaining approval from Cyclistic executives, necessitating the presentation of compelling data insights and professional data visualizations. The outcome of this analysis will not only address the immediate task of understanding user behavior but will also serve as the foundation for strategic decisions aimed at enhancing Cyclistic's future success in the bike-share market.


## Data Sources

I  used Cyclistic’s historical trip data to analyze and identify trends. [Download the Cyclistic trip data here](https://divvy-tripdata.s3.amazonaws.com/index.html).
  
**Note:**
- The datasets have a different name because Cyclistic is a fictional company.
- For the purposes of this case study, the datasets are appropriateand will enable you to answer the business questions.
- The data has been made available by Motivate International Inc. [Under this license](https://divvybikes.com/data-license-agreement)
- You can choose to work with an entire year of data, or just one quarter of a year.
- If you are working in Google Sheets, there are some files that might be too large to view.
- This is public data that you can use to explore how different customer types are using Cyclistic bikes.
- But note that data-privacy issues prohibit you from using riders’ personally identifiable information

## Project Tools

- R Studio/Posit Cloud
- EXCEL
- Tableau
- SQL Server Management Studio
- Google 
 
## Data cleaning Steps

Below I outline the data cleaning steps I performed for the "Cyclist_Trip_Data" and "Quarterly data" datasets using both Excel and SQL Server Management Studio (SSMS). 

__*For Cyclist_Trip_Data I:*__

1. Deleted unnecessary columns.
2. Removed rides with durations greater than 24 hours or less than one minute.
3. Created a "Ride_Length" column calculated as (Ended_at - Started_at) in HH:MM:SS format.
4. Created a "Day_of_Week" column using the WEEKDAY function on "Started_at" and formatted as a number with 0 decimals.
5. Renamed the "member" column to "Customer_Type," replacing "casual" with "Casual_Riders" and "member" with "Cyclist_Member."
6. Filtered and deleted rows with blank values.
7. Manually corrected any inconsistent or erroneous data.

__*For Quarterly data  I:*__

1. Renamed columns to standardize names
 - "tripduraton" to "Trip_Duration"
 - "usertype" to "User_Type"
 - "birthyear" to "Birth_Year", Replaced null values in the Birth_Year column with 0.
 - "gender" to "Gender" , Replaced null values in the "Gender" column with "Not-Applicable."
5. Converted time from seconds to minutes for Trip_duration.
6. Formatted "Start_Time" and "End_Time" as "y:m:d h:s."
7. Filtered and deleted rows with blank values.
 
The data cleaning process resulted in a cleaned and standardized dataset ready for analysis. Further details and insights can be explored in the cleaned_data.csv file.
 
## Exploratory Data Analysis(EDA)

1. __*Distinguishing Usage Patterns:*__
   - Explore ride frequency, duration, and popular routes for both annual members and casual riders.
   - Analyze peak usage times for each group to understand when they use Cyclistic bikes differently.
   - Investigate any noticeable patterns or trends in user behavior, such as preferred ride times or specific days of the week.

2. __*Motivations for Annual Memberships:*__
   - Examine data related to casual riders who transitioned to annual memberships.
   - Identify common factors among these riders, such as frequency of use, cost-effectiveness, or special promotions.
   - Investigate if there are certain time periods when casual riders are more likely to convert to annual memberships.

3. __*Digital Media Influence:*__
   - Analyze the effectiveness of current digital media campaigns in attracting casual riders.
   - Identify key demographics of casual riders and tailor digital content accordingly.
   - Assess the correlation between promotional campaigns and the conversion of casual riders to annual memberships.
     
These exploratory analyses will help Cyclistic gain valuable insights into the differences in bike usage patterns between annual members and casual riders. 

## Data Analysis

- I utilized SQL queries to analyze the Cyclist_Trip_Data and Quarterly datasets..
- I merged all Quarterley data into one full year.
  
To extract valuable insights and patterns fro the datasets you have to,  

__*Determine the distribution of user types (Casual Rider vs. Annual Subscriber)*__
``` sql
SELECT
    User_Type,
    COUNT(*) AS User_Count
FROM
    DBO.Cyclist_Data_FullYear
GROUP BY
    User_Type;
```

__*Determine the number of users per month (Casual Rider vs. Annual Subscriber)*__
``` sql
 SELECT
    CASE MONTH(Start_Time)
        WHEN 1 THEN 'Jan'
        WHEN 2 THEN 'Feb'
        WHEN 3 THEN 'Mar'
        WHEN 4 THEN 'Apr'
        WHEN 5 THEN 'May'
        WHEN 6 THEN 'Jun'
        WHEN 7 THEN 'Jul'
        WHEN 8 THEN 'Aug'
        WHEN 9 THEN 'Sep'
        WHEN 10 THEN 'Oct'
        WHEN 11 THEN 'Nov'
        WHEN 12 THEN 'Dec'
    END AS Month,
    User_Type,
    COUNT(*) AS  Monthly_Users   
FROM
    DBO.Cyclist_Data_FullYear
GROUP BY
    MONTH(Start_Time),
    User_Type
ORDER BY
       Monthly_Users    DESC;
```

__*Determine the number of users by gender (Annual Subscriber)*__
``` sql
   SELECT
    User_Type,
    Gender,
    COUNT(*) AS Gender_Count
FROM
   DBO.Cyclist_Data_FullYear
 WHERE 
   User_Type = 'Subscriber' 
 
GROUP BY
    User_Type,
    Gender;
```
__* Determine the prefered bike type (Casual Rider vs. Annual Subscriber)*__
``` sql
 SELECT
	User_Type, Ride_Type,
	 COUNT(*) AS Ride_Count
  FROM
 DBO.Cyclist_Trip_Data
GROUP BY
 Ride_Type,
  User_Type
ORDER BY
  User_Type,
Ride_Count DESC;
```

__*Determine the average trip duration the distribution of user types (Casual Rider vs. Annual Subscriber)*__
``` sql
 SELECT
    User_Type,
    AVG(Trip_Duration) AS Avg_Trip_Duration
FROM
    DBO.Cyclist_Data_FullYear
GROUP BY
    User_Type
ORDER BY
    Avg_Trip_Duration DESC;
```
__*Determine the popular ride start and end  stations (Casual Rider vs. Annual Subscriber)*__
``` sql
   SELECT  
    User_Type,
    From_Station_Name,
    To_Station_Name,
    COUNT(*) AS Route_Count
FROM
     DBO.Cyclist_Data_FullYear
GROUP BY
    User_Type,
    From_Station_Name,
    To_Station_Name
ORDER BY
    User_Type,
    Route_Count DESC;
```

__*Determine the popular weekday for rides (Casual Rider vs. Annual Subscriber)*__
``` sql
 SELECT
    CASE
        WHEN Day_of_week = 1 THEN 'Monday'
        WHEN Day_of_week = 2 THEN 'Tuesday'
        WHEN Day_of_week = 3 THEN 'Wednesday'
        WHEN Day_of_week = 4 THEN 'Thursday'
        WHEN Day_of_week = 5 THEN 'Friday'
        WHEN Day_of_week = 6 THEN 'Saturday'
        WHEN Day_of_week = 7 THEN 'Sunday'
        ELSE 'Unknown'  -- Add this line to handle unexpected values
    END AS Day_of_week,
    User_Type,
    COUNT(*) AS Ride_Count
FROM
    DBO.Cyclist_Trip_Data
GROUP BY
    Day_of_week,
    User_Type
ORDER BY
 User_Type,
    Ride_Count DESC;
```

__*Determine the popular time of the day for for rides (Casual Rider vs. Annual Subscriber)*__
``` sql
   SELECT
    User_Type,
    COUNT(*) AS Ride_Count,
    DATEPART(HOUR,  Started_at) AS Hour_Of_Day
FROM
    DBO.Cyclist_Trip_Data
GROUP BY
    User_Type,
    DATEPART(HOUR,  Started_at)
ORDER BY
    Ride_Count DESC;
```

__*Determine the popular average time of the day for rides (Casual Rider vs. Annual Subscriber)*__
``` sql
  
	 SELECT
    User_Type,
    AVG(CAST(DATEPART(HOUR, Started_at) AS int)) AS Avg_Hour_of_Day
FROM
    DBO.Cyclist_Trip_Data
GROUP BY
   User_Type;
```

__*Determine the popular  birth year (Annual Subscriber)*__
``` sql
  SELECT  User_Type,Birth_Year, COUNT(*) AS Birthyear_Count
	FROM DBO.Cyclist_Data_FullYear  
	GROUP BY User_Type,  Birth_Year
	ORDER BY  Birthyear_Count DESC
```

## Findings
Based on the analysis of the data this were my findings


## Recommendation
 

## Limitations
I have removed all the tables and colmns from the dataset that I didnt need because they would have affected the accuracy of my analysis and findings

## References

