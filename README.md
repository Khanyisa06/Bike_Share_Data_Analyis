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

In the preparation phase I performed the following tasks

__*For Cyclist_Trip_Data I:*__
1. load the data for inspection
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
__*Based on my analysis of the data this are my summerized findings*__

                  Annual members ride more frequently than casual riders

  ![User_Destributin](https://github.com/Khanyisa06/Cyclist_Bike-Share_Analysis/assets/106344554/4737d00d-668f-4a96-abcd-6241371f1a6f)
  

- On average, customers have a longer trip duration of 14 minutes compared to subscribers, who have an average trip duration of 9 minutes based on the provided data.
  
- June and May stand out as the peak months for user activity, with both annual subscribers and casual users showing the highest engagement in these periods.
- This suggests a notable difference in the gender distribution within the subscriber category, with a higher number of male subscribers compared to female subscribers.
- Classic bikes are more popular among subscribers, with significantly higher usage compared to electric bikes.
- The classic bike is more popular than the electric bike, with significantly higher usage by both subscribers and customers

- The route from "Lake Shore Dr & Monroe St" to "Streeter Dr & Grand Ave" is the most popular among customers, with 4786 trips recorded.
- Streeter Dr & Grand Ave" is a central station for customers, being either the starting or ending point in several popular routes.

- Canal St & Adams St" to "Michigan Ave & Washington St" is the most frequented route among subscribers, with 4587 trips recorded.
-  Stations like "Michigan Ave & Washington St," "Canal St & Adams St," and "Columbus Dr & Randolph St" are central to the subscriber routes.

-  For Customers, Monday has the highest ride count, while Sunday has the lowest.
For Subscribers, Wednesday has the highest ride count, while Sunday still has a lower count compared to other weekdays.
For Customers, Monday is the peak day, while for Subscribers, Wednesday is the peak day.

Customers contribute more to the overall ride counts on weekends, especially on Saturday.
On weekdays, their contribution is lower compared to Subscribers.



- both Subscribers and Customers have an average start time for rides at 13:00 PM. This suggests that, on average, users from both categories tend to initiate their rides around 1:00 PM.

- service is more popular during the daytime, especially in the afternoon, for both Subscribers and Customers.
- Subscribers contribute significantly to the overall ride counts, with a higher frequency during peak hours.
- Both Subscribers and Customers have similar patterns in terms of hourly ride distribution, with peaks during the late afternoon and valleys during the late-night and early morning hours.
- There is a significant drop in ride counts during late-night hours (from 22:00 to 5:00), for both Subscribers and Customers.
- The busiest hours seem to be in the afternoon, particularly around 5 PM (17:00), with 30,782 and 12,758 rides by Subscribers and Customers, respectively.
- There is also notable activity in the morning hours around 8 AM and 9 AM.


subscribers born in the 1990s and early 1980s are more numerous compared to those born in the 1970s and earlier.
There is a noticeable presence of subscribers born in the late 1990s and early 2000s, suggesting engagement from a younger audience.
There is a general trend of decreasing subscriber counts as birth years move further away from the 1990s, indicating a potential decline in user engagement or adoption among older age groups.
The counts generally decrease as birth years move away from the 1990s, indicating a decline in subscriber numbers for older age groups.
The birth years from the early 1980s to the mid-1990s have relatively high counts, indicating a significant user presence in these age groups
The birth year 1992 has the highest count, with 207,341 subscribers.


## Recommendation
 
Implement referral programs that reward current annual members for referring casual riders who successfully convert to annual memberships.
Leverage word-of-mouth marketing to encourage casual riders to consider the benefits of long-term membership.

## Limitations
I have removed all the tables and colmns from the dataset that I didnt need because they would have affected the accuracy of my analysis and findings

## References

