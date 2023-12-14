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


### Objectives

*Produce a report with the following deliverables:*

1. A clear statement of the business task
2. A description of all data sources used
3. Documentation of any cleaning or manipulation of data
4. A summary of your analysis
5. Supporting visualizations and key findings
6. Your top three recommendations based on your analysis
 
### Business Task

The primary business task is to understand how casual riders and annual members use Cyclistic bikes differently. As a junior data analyst in the marketing team, the goal is to gather insights that will inform the development of a targeted marketing strategy. The overarching objective is to maximize the number of annual memberships(convert casual riders into annual members), as identified by the director of marketing. 

To achieve this, the data analysis process will be followed, encompassing key steps such as asking relevant questions, preparing and processing the data, conducting a thorough analysis, and ultimately sharing actionable insights. The success of the proposed marketing strategy hinges on obtaining approval from Cyclistic executives, necessitating the presentation of compelling data insights and professional data visualizations. The outcome of this analysis will not only address the immediate task of understanding user behavior but will also serve as the foundation for strategic decisions aimed at enhancing Cyclistic's future success in the bike-share market.


### Data Sources
- I  used Cyclistic’s historical trip data to analyze and identify trends. [Download the Cyclistic trip data here](https://divvy-tripdata.s3.amazonaws.com/index.html).
  
**Note:**
- The datasets have a different name because Cyclistic is a fictional company.
- For the purposes of this case study, the datasets are appropriateand will enable you to answer the business questions.
- The data has been made available by Motivate International Inc. [Under this license](https://divvybikes.com/data-license-agreement)
- You can choose to work with an entire year of data, or just one quarter of a year.
- If you are working in Google Sheets, there are some files that might be too large to view.
- This is public data that you can use to explore how different customer types are using Cyclistic bikes.
- But note that data-privacy issues prohibit you from using riders’ personally identifiable information

### Project Tools
- R Studio/Posit Cloud
- EXCEL
- Tableau
- SQL Server Management Studio
- Google 
 
### Data cleaning Steps
Below I outline the data cleaning steps I performed for the "Cyclist_Trip_Data" and "Quarterly" datasets using both Excel and SQL Server Management Studio (SSMS). 

**For Cyclist_Trip_Data:**

1. Deleted unnecessary columns.
2. Removed rides with durations greater than 24 hours or less than one minute.
3. Created a "Ride_Length" column calculated as (Ended_at - Started_at) in HH:MM:SS format.
4. Created a "Day_of_Week" column using the WEEKDAY function on "Started_at" and formatted as a number with 0 decimals.
5. Renamed the "member" column to "Customer_Type," replacing "casual" with "Casual_Riders" and "member" with "Cyclist_Member."
6. Filtered and deleted rows with blank values.
7. Manually corrected any inconsistent or erroneous data.

**For Quarterly data I:**

1. Renamed columns to standardize names (e.g., "tripduraton" to "Trip_Duration").
2. Standardized column names (e.g., "usertype" to "User_Type").
3. Renamed columns for clarity (e.g., "birthyear" to "Birth_Year").
    - Replaced null values in the "Birth_Year" column with 0.
4. Standardized column names (e.g., "gender" to "Gender").
    - Replaced null values in the "Gender" column with "Not-Applicable."
5. Converted time from seconds to minutes.
6. Formatted "Start_Time" and "End_Time" as "y:m:d h:s."
7. Filtered and deleted rows with blank values.
 
The data cleaning process resulted in a cleaned and standardized dataset ready for analysis. Further details and insights can be explored in the cleaned_data.csv file.

 

### Exploratory Data Analysis

1. How do annual members and casual riders use Cyclistic bikes differently?
2. Why would casual riders buy Cyclistic annual memberships?
3. How can Cyclistic use digital media to influence casual riders to become members?

  
### Data Analysis
 


### Findings
 



### Recommendation
 

### Limitations
I have removed all the tables and colmns from the dataset that I didnt need because they would have affected the accuracy of my analysis and findings

### References

