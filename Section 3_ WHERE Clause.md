# Section 3: WHERE Clause

    SELECT * FROM `bigquery-public-data.usa_names.usa_1910_current` 
    WHERE state = 'FL' AND gender = 'M' 
    AND year = 2000 
    ORDER BY number 
    DESC LIMIT 100

> where clauses where the conditions involved filtering on a numerical
> column

## Equal Operator

> -   Return the number of records where the tripduration was equal to 432 seconds.

    SELECT count(*) AS num_bike_rides  
    FROM`bigquery-public-data.new_york_citibike.citibike_trips`  
    WHERE tripduration = 432

## Not Equal Operator

> -   Return the number of records where the tripduration was not equal to 432 seconds.

    SELECT COUNT(*) AS num_bike_rides  
    FROM`bigquery-public-data.new_york_citibike.citibike_trips`  
    WHERE tripduration != 432

## Less Than

> -   Return the number of records where the tripduration was less than 300 seconds.

    SELECT COUNT(*) AS num_bike_rides  
    FROM`bigquery-public-data.new_york_citibike.citibike_trips`  
    WHERE tripduration < 300

## Less Than Or Equal

> -   Return the number of records where the tripduration was less than or equal to 300 seconds.

    SELECT COUNT(*) AS num_bike_rides  
    FROM`bigquery-public-data.new_york_citibike.citibike_trips`  
    WHERE tripduration <= 300

## Greater Than

> -   Return the number of records where the tripduration was greater than 24 hours.

    SELECT COUNT(*) AS num_bike_rides  
    FROM`bigquery-public-data.new_york_citibike.citibike_trips`  
    WHERE tripduration > 24*60*60

## Greater Than Or Equal

> -   Return the number of records where the tripduration was greater than or equal 24 hours.

    SELECT COUNT(*) AS num_bike_rides  
    FROM`bigquery-public-data.new_york_citibike.citibike_trips`  
    WHERE tripduration >= 24*60*60

## Combining Multiple Conditions using AND

> -   Return the number of records where the tripduration was between 5 hours and 9 hours i.e. greater than or equal to 5 hours and less than
> or equal to 9 hours.

    SELECT COUNT(*) 
    AS num_bike_rides  
    FROM`bigquery-public-data.new_york_citibike.citibike_trips`  
    WHERE tripduration >= 5*60*60 
    AND 
    tripduration <= 9*60*60

## Combining Multiple Conditions using both AND & OR

> -   Return the number of records where the tripduration was between 1 hour and 3 hours OR between 5 and 8 hours. Notice the use of
> parenthesis around the two statements separated by OR. You need these
> brackets when chaining together AND and OR conditions within the same
> clause.

    SELECT COUNT(*) AS num_bike_rides  
    FROM`bigquery-public-data.new_york_citibike.citibike_trips`  
    WHERE (tripduration >= 1*60*60 AND tripduration <= 3*60*60)  
    OR (tripduration >= 5*60*60 AND tripduration <= 8*60*60)

## IN statement

> -   the IN statement can be used to provide a list within a condition. In this example we are counting the records where the tripduration is
> in the list (60,120).

    SELECT COUNT (*) AS num_bike_rides  
    FROM`bigquery-public-data.new_york_citibike.citibike_trips`  
    WHERE tripduration IN (60,120)

> The above query is the same as saying the tripduration is 60 or the
> trip duration is 120.
> 
> For example, this query which uses multiple OR statements,

    SELECT COUNT (*) 
    AS num_bike_rides  
    FROM`bigquery-public-data.new_york_citibike.citibike_trips`  
    WHERE 
    tripduration = 60 
    or tripduration = 120 
    or tripduration = 180 
    or tripduration = 240

> can be replaced with a query using an IN statement that is easier to
> write/read.

    SELECT COUNT (*) AS num_bike_rides  
    FROM`bigquery-public-data.new_york_citibike.citibike_trips`  
    WHERE tripduration IN (60,120,180,240)

## NOT IN Statement

> -   although we did not cover an example in the video (we will do examples in other videos) you can also use use a NOT IN clause. For
> example, you can do the negation of the above query. Count the number
> of records where the trip duration was not one of (60,120,180,240).

    SELECT COUNT (*) AS num_bike_rides  
    FROM`bigquery-public-data.new_york_citibike.citibike_trips`  
    WHERE tripduration NOT IN (60,120,180,240)

> where clause with a column of type string

## Equal Operator

> -   Filter on records where the string column, in this case minor_category, is an exact match of the given string “Harassment”.

    SELECT COUNT (*) AS num_crimes  
    FROM`bigquery-public-data.london_crime.crime_by_lsoa`  
    WHERE minor_category = "Harassment"

## Not Equal Operator

> -   Filter on records where the string column, in this case minor_category, is not an exact match of the given string
> “Harassment”.

    SELECT COUNT (*) AS num_crimes  
    FROM`bigquery-public-data.london_crime.crime_by_lsoa`  
    WHERE minor_category != "Harassment"

## IN statement

> -   Filter on records where the string column, in this case minor_category, is within a given list of strings (“Harassment”,
> “Assault with Injury”).

    SELECT COUNT (*) AS num_crimes  
    FROM`bigquery-public-data.london_crime.crime_by_lsoa`  
    WHERE minor_category in ("Harassment", "Assault with Injury")

> The above query is the same as using multiple OR statements:

    SELECT COUNT (*) AS num_crimes  
    FROM`bigquery-public-data.london_crime.crime_by_lsoa`  
    WHERE 
    minor_category = 'Harassment'
    or 
    minor_category = 'Assault with Injury'

## Like Statement

> A common technique is to search for a specific pattern within a string
> column. - You can look for a pattern anywhere in the string by using
> like '%pattern%' - You can look for a pattern at the end of the string
> by using like '%pattern' - You can look for a pattern at the start of
> the string by using like 'pattern%' - The pattern given is any pattern
> of characters and it’s case sensitive.
> 
> Here is an example of returning distinct list of records from the
> minor_category column that contain the pattern Drug anywhere in the
> string. This query returns Possession Of Drugs, Other Drugs, Drug
> Trafficking.

    SELECT distinct minor_category  
    FROM`bigquery-public-data.london_crime.crime_by_lsoa`  
    WHERE minor_category  like '%Drug%'

> Here is an example of returning distinct list of records from the
> minor_category column that contain the pattern Drug at the start of
> the string. This query returns Drug Trafficking.

    SELECT distinct minor_category  
    FROM`bigquery-public-data.london_crime.crime_by_lsoa`  
    WHERE minor_category like 'Drug%'

> Here is an example of returning distinct list of records from the
> minor_category column that contain the pattern Drugs at the end of the
> string. This query returns Possession Of Drugs, Other Drugs.

    SELECT distinct minor_category  
    FROM`bigquery-public-data.london_crime.crime_by_lsoa`  
    WHERE minor_category like '%Drugs'

> Here is an example of returning distinct list of records from the
> minor_category column that contain the pattern eh anywhere in the
> string. Run this query in Big Query to see the records it will return
> as it will help your understanding.

    SELECT distinct minor_category  
    FROM`bigquery-public-data.london_crime.crime_by_lsoa`  
    WHERE minor_category like '%eh%'

> Often when looking for a pattern, we lower case the column in which we
> are looking. This way we can just use lower case in our like
> statement. This example used the lower function which lowers the case
> of the string column. We will work with these functions more in future
> videos. Run this query in Big Query to see the records it will return
> as it will help your understanding.

    SELECT distinct minor_category  
    FROM`bigquery-public-data.london_crime.crime_by_lsoa`  
    WHERE lower (minor_category) like '%motor%'

> In this video we covered examples using WHERE clauses on a column of
> type TIMESTAMP. A TIMESTAMP column will typically have the year,
> month, day, hour, minute and second. For example 2014-10-26 15:12:00
> UTC. A DATE column will just have the year, month and day. For
> example, 2014-10-26. You can change a TIMESTAMP into a DATE by casting
> it i.e. cast(TIMESTAMP AS DATE). This would convert 2014-10-26
> 15:12:00 UTC into 2014-10-26.

## Some Useful TIMESTAMP Functions

> Run this query in Big Query and review the results to learn several
> functions we can use when working with TIMESTAMP columns.

    SELECT start_time as start_time_timestamp,  
    cast (start_time as date) as start_time_date,  
    extract (hour from start_time) as start_time_hour,  
    extract (minute from start_time) as start_time_minute,  
    extract (day from start_time) as start_time_day,  
    extract (year from start_time) as start_time_year,  
    extract (month from start_time) as start_time_month,  
    extract (week from start_time) as start_time_week  
    FROM`bigquery-public-data.austin_bikeshare.bikeshare_trips`  
    LIMIT 100

## Filtering For Records After A Date

    SELECT start_time as start_time_timestamp,  
    cast (start_time as date) as start_time_date,  
    extract (hour from start_time) as start_time_hour,  
    extract (minute from start_time) as start_time_minute,  
    extract (day from start_time) as start_time_day,  
    extract (year from start_time) as start_time_year,  
    extract (month from start_time) as start_time_month,  
    extract (week from start_time) as start_time_week  
    FROM`bigquery-public-data.austin_bikeshare.bikeshare_trips`  
    WHERE start_time > '2018-10-01' LIMIT 100

## Filtering For Records Equal To A Date

> -   notice that we cast the TIMESTAMP column as a DATE in the WHERE clause. If the column was already a DATE we would not have to do that.

    SELECT start_time as start_time_timestamp,  
    cast (start_time asdate) as start_time_date,  
    extract (hour from start_time) as start_time_hour,  
    extract (minute from start_time) as start_time_minute,  
    extract (day from start_time) as start_time_day,  
    extract (year from start_time) as start_time_year,  
    extract (month from start_time) as start_time_month,  
    extract (week from start_time) as start_time_week  
    FROM`bigquery-public-data.austin_bikeshare.bikeshare_trips`  
    WHERE cast (start_time as date) ='2018-10-01'
    LIMIT 100

## Filtering For Records Between Two Dates

    SELECT start_time as start_time_timestamp,  
    cast (start_time as date) as start_time_date,  
    extract (hour from start_time) as start_time_hour,  
    extract (minute from start_time) as start_time_minute,  
    extract (day from start_time) as start_time_day,  
    extract (year from start_time) as start_time_year,  
    extract (month from start_time) as start_time_month,  
    extract (week from start_time) as start_time_week  
    FROM`bigquery-public-data.austin_bikeshare.bikeshare_trips`  
    WHERE start_time >= '2018-09-01'
    and
    start_time <= '2018-09-30'
    LIMIT 100

## Filtering For Records In Given List Of Hours

    SELECT start_time as start_time_timestamp,  
    cast (start_time as date) as start_time_date,  
    extract (hour from start_time) as start_time_hour,  
    extract (minute from start_time) as start_time_minute,  
    extract (day from start_time) as start_time_day,  
    extract (year from start_time) as start_time_year,  
    extract (month from start_time) as start_time_month,  
    extract (week from start_time) as start_time_week  
    FROM`bigquery-public-data.austin_bikeshare.bikeshare_trips`  
    where extract (hour from start_time) 
    IN
    (17,18,19,20)  
    LIMIT 100

> In this shorter video we showed how to use a WHERE clause to filter
> for NULL and NOT NULL records.
> 
> First run this query:

    SELECT COUNT (*) AS count1, 
    -- the number of records 
    COUNT(dropoff_location) AS count2 
    -- the number of records where dropoff_location is not null
    FROM`bigquery-public-data.chicago_taxi_trips.taxi_trips`

> If we only want to consider records where the column dropoff_location
> is NOT NULL then we can use a WHERE clause with a IS NOT NULL
> statement.

    SELECT COUNT (*) AS count1, 
    -- the number of records  
    COUNT(dropoff_location) AS count2 
    -- the number of records where dropoff_location is not null FROM`bigquery-public-data.chicago_taxi_trips.taxi_trips`   WHERE dropoff_location IS NOT NULL

> Similarly, if we want to filter for only NULL records then we use:

    SELECT COUNT (*) AS count1, 
    -- the number of records 
    COUNT(dropoff_location) AS count2 
    -- the number of records where dropoff_location is not null
    FROM`bigquery-public-data.chicago_taxi_trips.taxi_trips`  
    WHERE dropoff_location IS NULL

