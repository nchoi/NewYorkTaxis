
# Blog Post #4
# Predicting Tip Percentages Using Random Forest after Integrating Weather

For our fourth blog post, we decided to investigate tip percentages, finally taking into account weather from Wunderground. Again, we did this using random forest regression. Our input variables were 

- Temperature
- Weather Conditions
- Time of Day
- Month

While the target variable was percentage tip, calculated in the SQL query below.

## Getting and Cleaning the Data
```
WITH taxiweather AS
(
   SELECT tip_amount/yellow_tripdata.total_amount as tip_pct,
     pickup_neighborhood,
     extract(month from pickup_datetime) as month,
     extract(hour from pickup_datetime) as hour,
     temperature,
     conditions
   FROM yellow_tripdata
 JOIN (SELECT * FROM hourly_weather WHERE random() < 0.01) AS hw ON
                       yellow_tripdata.pickup_datetime >= hw.date_time AND
                       yellow_tripdata.pickup_datetime < hw.date_time + interval ‘1 hour’
)
SELECT * FROM taxiweather
WHERE tip_pct != 0 AND temperature != -9999 AND pickup_neighborhood IS NOT NULL LIMIT 10000;
```

To set up our testing and training X vectors, we ran the above SQL query and saved the output to a csv. 

We cleaned our data set by ignoring zero dollar tips and fares. Although we recognize that customers may tip zero dollars, a large percentage of tips in the dataset are recorded as zero dollars leading us to believe that there was a discrepancy. Most of these tips were associated with cash payments so we also ignored all rides paid for with cash. Finally we ignored rides with latitude and longitude values of 0 since these are physically impossible, and rides which could not be mapped to a neighborhood or borough since null values would be hard to perform regression on.

## Using Flask
set up website using flask, unpickled encoder and 


## Visualization


# Results
