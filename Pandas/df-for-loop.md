# Create Dataframes In For Loop

It is often useful to create multiple dataframes in a for loop. For instance, in this example we have a dataframe `table` that was created using the Pandas `pivot_table` method. We want to create a new dataframe for several filters of the current dataframe. We create a dictionary `pivots` that we can fill with these resulting dataframes.

```python
pivots = {}
for msn in msn_list:
    conditions = 'SerialNo == ["' + str(msn) + '"]'
    pivots[msn] = table.query(conditions)

```

tags: python, pandas, filter, query, pivot
