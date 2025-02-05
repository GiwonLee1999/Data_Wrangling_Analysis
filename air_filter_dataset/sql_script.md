-- Simple analysis so far


``` sql
-- Find filter name and its  number 
SELECT
    filter_name,
    count(filter_name)
FROM 
`nimble-ally-449901-n6.air_filter_data.air_filter` 
group by filter_name;
```

```sql
-- See if there's any null values in the filter name
SELECT 
  filter_name
FROM
  `nimble-ally-449901-n6.air_filter_data.air_filter` 
WHERE
  filter_name IS NULL;
```

```sql
-- Check the minimum and maximum filter age
SELECT
  MIN(filter_age_days) as Min_Filter_Age,
  MAX(filter_age_days) as Max_Filter_Age
FROM 
  `nimble-ally-449901-n6.air_filter_data.air_filter`;
```

```sql
-- The correlation between filter age and efficiency
SELECT 
    filter_age_days,
    efficiency*100
FROM
    `nimble-ally-449901-n6.air_filter_data.air_filter`;
```

```sql
-- Since the filter age range from 0 - 68, split the range by 10 then find the average efficiency. 
SELECT
    CASE
        WHEN filter_age_days BETWEEN 0 AND 10 THEN '0 - 10'
        WHEN filter_age_days BETWEEN 10 AND 20 THEN '10 - 20'
        WHEN filter_age_days BETWEEN 20 AND 30 THEN '20 - 30'
        WHEN filter_age_days BETWEEN 30 AND 40 THEN '30 - 40'
        WHEN filter_age_days BETWEEN 40 AND 50 THEN '40 - 50'
        WHEN filter_age_days BETWEEN 50 AND 60 THEN '50 - 60'
        WHEN filter_age_days BETWEEN 60 AND 70 THEN '60 - 70'
    END AS filter_AGE,
    CONCAT(ROUND(AVG(efficiency)*100,2), "%") AS average_efficiency
FROM
    `nimble-ally-449901-n6.air_filter_data.air_filter`
WHERE filter_age_days BETWEEN 0 AND 10
  OR  filter_age_days BETWEEN 10 AND 20
  OR  filter_age_days BETWEEN 20 AND 30
  OR  filter_age_days BETWEEN 30 AND 40
  OR  filter_age_days BETWEEN 40 AND 50
  OR  filter_age_days BETWEEN 50 AND 60
  OR  filter_age_days BETWEEN 60 AND 70
GROUP BY filter_AGE
ORDER BY filter_AGE;
```
