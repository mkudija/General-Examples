# SQL General How-To


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
	, COUNT(t.distance) AS value_count
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
