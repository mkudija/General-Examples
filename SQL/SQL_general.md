# SQL General How-To


## Find tables with `colName` column

```SQL
select t.table_schema,
       t.table_name
from information_schema.tables t
inner join information_schema.columns c 
           on c.table_name = t.table_name 
           and c.table_schema = t.table_schema
where c.column_name = 'colName'
      and t.table_schema not in ('information_schema', 'pg_catalog')
      and t.table_type = 'BASE TABLE'
order by t.table_schema;
```


## Unique items in **`column`**

```SQL
SELECT 
    t.device
FROM 
    database.table t
GROUP BY t.device
```

|   | device       |
|---|--------------|
| 1 | "iPhone10,1" |
| 2 | "iPhone10,2" |
| 3 | "iPhone10,3" |
| 4 | "iPhone10,4" |
| 5 | "iPhone10,5" |


## value_count of **`column`**

```SQL
SELECT 
    t.device
    ,COUNT(t.distance) AS value_count
FROM 
    database.table t
GROUP BY t.device
ORDER BY value_count DESC
```

|   | device     | value_count |
|---|------------|-------|
| 1 | iPhone10,5 | 23832 |
| 2 | iPhone10,2 | 14553 |
| 3 | iPhone10,4 | 3487  |
| 4 | iPhone10,3 | 3078  |
| 5 | iPhone10,1 | 23    |


## `np.where` equivalent for cases

```SQL
CASE
    WHEN t.score BETWEEN 0  AND 24  THEN '0-24'
    WHEN t.score BETWEEN 25 AND 49  THEN '25-49'
    WHEN t.score BETWEEN 50 AND 74  THEN '50-74'
    WHEN t.score BETWEEN 75 AND 100 THEN '75-100'
    ELSE 'OTHER'
END AS score_group
```


## Select only first/last record using `RANK() OVER PARTITION BY`

In this example, there may be many records for a given `user_id`, but we only want to select the most recent record for each `user_id`. Alternatively, we could select the first record by using `ASC`:

```SQL
SELECT
    ...
    ...
    FROM(
    SELECT
        ...
	...
        ,RANK() OVER (PARTITION BY t.user_id ORDER BY t.created_at DESC) AS RANK
        FROM
            database.table AS t
    )
WHERE RANK = 1
```

## Round

`ROUND` rounds the number, and if you don't want the additional `.000` you can `CAST` as an integer:

`CAST(ROUND(col_name, 0) AS INT) AS col_name_rounded`

## Decile

To get actual deciles you can use a `CASE` statement:
```SQL
SELECT 
    score_decile, 
    COUNT(score_decile) AS count
FROM (
    SELECT
        *,
        CASE
            WHEN score < 10 THEN '0-9'
            WHEN score > 9 AND score < 20 THEN '10-19'
            WHEN score > 19 AND score < 30 THEN '20-29'
            WHEN score > 29 AND score < 40 THEN '30-39'
            WHEN score > 39 AND score < 50 THEN '40-49'
            WHEN score > 49 AND score < 60 THEN '50-59'
            WHEN score > 59 AND score < 70 THEN '60-69'
            WHEN score > 69 AND score < 80 THEN '70-79'
            WHEN score > 79 AND score < 90 THEN '80-89'
            WHEN score > 89 THEN '90-100'
        END as score_decile
    FROM database.table
)
GROUP BY score_decile
ORDER BY score_decile
```

A quick trick is to `ROUND` with `-1` to approximate deciles if score is in the range from 0-100. This is not exact as your buckets will be `0-5`, `6-15`...`86-95`, `96-100` so the first and last buckets will be small, but if you are just comparing between two distributions and care less about the absolute distribution, this may be an easy trick.

```SQL
SELECT 
    score_decile_approx, 
    COUNT(score_decile_approx) AS count
FROM (
    SELECT
        *,
        ROUND(score, -1) AS score_decile_approx
    FROM database.table
)
GROUP BY score_decile_approx
ORDER BY score_decile_approx
```

Finally, we may want the *rate* rather than the count, which we can get with the `RATIO_TO_REPORT(count) OVER () AS rate` command. This gives `rate` for each row as a fraction of the sum of count `count` column.

```SQL
SELECT 
    score_decile_approx, 
    COUNT(score_decile_approx) AS count,
    RATIO_TO_REPORT(count) OVER () AS rate
FROM (
    SELECT
        *,
        ROUND(unmapped_score, -1) AS score_decile_approx
    FROM database.table

)
GROUP BY score_decile_approx
ORDER BY score_decile_approx
```

## Last 7 days of data

```SQL
SELECT 
    *
FROM 
    database.table t
WHERE
    t.created_at > GETDATE() - INTERVAL '7 days'
```
