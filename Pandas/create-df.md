# Create DataFrame

## Random

`df = pd.DataFrame({ 'x': np.random.randn(100), 'y': np.random.randn(100) })`

## [`from_dict`](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.DataFrame.from_dict.html#pandas.DataFrame.from_dict)

```python
dict = {'YOM': YOM, 'leaseTerm': leaseTerm, 'downTime': downTime, 'remarketCost': remarketCost,
        'transitionCost': transitionCost, 'transitionAge': transitionAge, 'leasableLife': leasableLife, 'lrf': lrf,
        'wacc': wacc, 'inflation': inflation, 'startingRent': startingRent}
assumptions = pd.DataFrame.from_dict(dict, orient='index')
```

## Single Blank Row From Known Columns

```python
columns = ['Col 1','Col 2','Col 3','Col 4','Col 5']
df = pd.DataFrame(index=range(0,1), columns=columns).fillna(0)
```

```bash
>>> df
   Col 1  Col 2  Col 3  Col 4  Col 5
0      0      0      0      0      0

```
# Create Dictionary of DataFrames In For Loop
It is often useful to create multiple DataFrames in a for loop. For instance, in this example we have a DataFrame `table` that was created using the Pandas `pivot_table` method. We want to create a new DataFrame for several filters of the current DataFrame. We create a dictionary `pivots` that we can fill with these resulting DataFrames.

```python
pivots = {}
for msn in msn_list:
    conditions = 'SerialNo == ["' + str(msn) + '"]'
    pivots[msn] = table.query(conditions)

```

# Concat DataFrames in Dictionary
```FlightIDs``` is a dictionary of DataFrames

```python
dfFlightIDs = pd.concat(FlightIDs.values(), ignore_index=True)
```

tags: python, pandas, filter, query, pivot

# Concat all files in directory to DF
```python
import pandas as pd
from pathlib import Path

# get files
p = Path('../data').glob('**/*')
files = [x for x in p if x.is_file() and x.suffix=='.csv']

# concat files
dfs = {}
for index, value in enumerate(files):
    dfs[value] = pd.read_csv(files[index])
df = pd.concat(dfs.values(), ignore_index=True)
```
