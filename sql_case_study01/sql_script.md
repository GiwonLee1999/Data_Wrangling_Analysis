1. Identify the museums which are open on both Sunday and Monday. Display Museum name and city
```sql
-- This displays the museums that open on both Sunday and Monday
SELECT 
    *    
FROM
    nimble-ally-449901-n6.SQL_Case_Study01.museum_hours mh1
WHERE day = 'Sunday' AND EXISTS(
    SELECT 1 FROM nimble-ally-449901-n6.SQL_Case_Study01.museum_hours mh2
        WHERE mh2.museum_id = mh1.museum_id AND mh2.day = 'Monday'); 

SELECT 
    m.name AS museum_name,
    m.city    
FROM
    nimble-ally-449901-n6.SQL_Case_Study01.museum_hours mh1
JOIN nimble-ally-449901-n6.SQL_Case_Study01.museum m ON m.museum_id = mh1.museum_id
WHERE day = 'Sunday' AND EXISTS(SELECT 1 FROM nimble-ally-449901-n6.SQL_Case_Study01.museum_hours mh2
        WHERE mh2.museum_id = mh1.museum_id AND mh2.day = 'Monday')
ORDER BY m.name, m.city;   
```

2. Which museum is open for the longest during a day. Display mesume name, state, and hours open and which day.
```sql
-- I have a trial account and does not let me update the wrong data and its type.
-- I tried to extract hours from the time stamp
SELECT 
  *,
  CASE
    WHEN RIGHT(open, 2) = 'PM' THEN 
      12 + CAST(LEFT(open, 2) AS INT64) + CAST(RIGHT(LEFT(open, 5), 2) AS INT64) / 60
    ELSE 
      CAST(LEFT(open, 2) AS INT64) + CAST(RIGHT(LEFT(open, 5), 2) AS INT64) / 60
  END AS OPEN1,
  CASE
    WHEN RIGHT(TRIM(close), 2) = 'PM' THEN 
      12 + CAST(LEFT(TRIM(close), 2) AS INT64) + CAST(RIGHT(LEFT(TRIM(close), 5), 2) AS INT64) / 60
    ELSE 
      CAST(LEFT(TRIM(close), 2) AS INT64) + CAST(RIGHT(LEFT(TRIM(close), 5), 2) AS INT64) / 60
  END AS CLOSE2
FROM nimble-ally-449901-n6.SQL_Case_Study01.museum_hours;

-- This is the correct answer if the type and coorect data is input.
SELECT * FROM(
  SELECT m.name AS museum_name, m.state, mh.day,
  RANK() OVER(ORDER BY(timestamp(close,'HH:MI PM') - TIMESTAMP(open,'HH:MI AM'))) AS rnk
FROM nimble-ally-449901-n6.SQL_Case_Study01.museum_hours mh
JOIN nimble-ally-449901-n6.SQL_Case_Study01.museum m on m.museum_id = mh.museum_id ) x
WHERE x.rnk = 1;
```
