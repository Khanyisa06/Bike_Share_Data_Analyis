This file contains metadata for Trips, Tripdata and Stations files.

For more information, visit http://DivvyBikes.com/data or email questions to data@DivvyBikes.com. 


Metadata for Cyclists Quarterly Trips Data:

Variables:

Trip_ID                    : ID attached to each trip taken
Start_Time               : day and time trip started, in CST
Stop_Time                : day and time trip ended, in CST
Bike_ID                    : ID attached to each bike
Trip_Duration             : time of trip in seconds 
From_Station_Name   : name of station where trip originated
To_Station_Name       : name of station where trip terminated 
From_Station_ID        : ID of station where trip originated
To_Station_ID            : ID of station where trip terminated
User_Type                 : "Customer" is a rider who purchased a 24-Hour Pass; "Subscriber" is a rider who purchased an Annual Membership
gender                      : gender of rider 
Birth_Year                 : birth year of rider


Notes:

* First row contains column names
* Trips that did not include a start or end date are excluded
* Trips less than 1 minute in duration are excluded
* Trips greater than 24 hours in duration are excluded
* Gender and birthday are only available for Subscribers
* The latitude and longitude columns were deleted
* Cyclists_Trips_Q1 has 325, 279 rows
* Cyclists_Trips_Q2 has 818, 439 rows
* Cyclists_Trips_Q3 has 800, 001 rows
* Cyclists_Trips_Q4 has 580, 573 rows
 


Metadata for Cyclists_Trips_Data:

Ride_ID                      : ID attached to each ride taken
Ride_type                    : The type of bycicle ride
Started_at                   :  where the ride starts             
Ended_at                     : where the ride ends
Ride_Legth                   : the length of each ride, how long it takes
Day-Of_Week                : the day the ride was taken
Start_Station_Name       : name station where the ride is taken
Start_Station_ID            : ID attached to each  start station
End_Station_Name         : name of end station
End_Station_ID              : ID attached to each end station
Customer_Type               : type of customer casual or anual

* First row contains column names
* Rides that did not include a start or end time are excluded
* Trips less than 1 minute in duration are excluded
* Trips greater than 24 hours in duration are excluded
* Cyclists_Trips_Data has 396, 952 rows



Metadata for Stations:

Variables:

id: ID attached to each station
name: station name    
latitude: station latitude
longitude: station longitude
dpcapacity: number of total docks at each station as of 6/30/2019
online_date: date the station was created in the system

Notes:

* Divvy_Stations has 582 rows
