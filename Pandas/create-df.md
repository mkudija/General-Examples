# Create DataFrame

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
