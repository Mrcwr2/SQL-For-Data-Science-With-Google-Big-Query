
# Section 2: Counting Records, Returning Distinct Records, & Ordering Records

## Count & Alias

    SELECT COUNT(DISTINCT gender) AS distinct_gender_count,  
    COUNT (DISTINCT year) AS distinct_year_count,  
    COUNT (DISTINCT state) AS distinct_state_count,  
    COUNT (DISTINCT name) AS distinct_name_count,  
    COUNT (*) AS num_records,  
    COUNT (name) AS cnt  
    FROM`bigquery-public-data.usa_names.usa_1910_2013`

## Count with nulls

> count(*) —-> number of records in the table and NULL values have no
> effect on results
> 
> count(column_name) —-> returns the number of non null records for the
> column_name
> 
> count(distinct column_name)returns the number of distinct values for
> the column (does not count NULL records)

    SELECT COUNT(*) AS num_rows,  
    COUNT (borough) AS borough_count,  
    COUNT (DISTINCT borough) AS distinct_borough_count,  
    COUNT (contributing_factor_vehicle_3) AS contributing_factor_vehicle_3_count,  
    COUNT (contributing_factor_vehicle_1) AS contributing_factor_vehicle_1_count,  
    COUNT (DISTINCT contributing_factor_vehicle_1) AS distinct_contributing_factor_vehicle_1_count  
    FROM`bigquery-public-data.new_york_mv_collisions.nypd_mv_collisions`

> Returning a distinct set of values from a column and ordering results

    SELECT DISTINCT
    year
    FROM`bigquery-public-data.usa_names.usa_1910_current`  
    ORDER BY year DESC

> Or if we wanted to return a list of the first 10 names sorted in
> alphabetical order we could execute this query:

    SELECT DISTINCT name   
    FROM`bigquery-public-data.usa_names.usa_1910_current`  
    ORDER BY name ASC LIMIT10

> If we wanted to see the last 100 names we could execute:

    SELECT DISTINCT name  
    FROM`bigquery-public-data.usa_names.usa_1910_current`  
    ORDER BY name DESC LIMIT 100

> returning a distinct set of values from multiple column’s and ordering
> results

    SELECT DISTINCT borough,  
    major_category,  
    minor_category  
    FROM`bigquery-public-data.london_crime.crime_by_lsoa`  
    ORDER BY borough,  
    major_category,  
    minor_category

