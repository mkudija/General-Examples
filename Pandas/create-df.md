# Create DataFrame

## [`from_dict`](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.DataFrame.from_dict.html#pandas.DataFrame.from_dict)

```python
dict = {'YOM': YOM, 'leaseTerm': leaseTerm, 'downTime': downTime, 'remarketCost': remarketCost,
        'transitionCost': transitionCost, 'transitionAge': transitionAge, 'leasableLife': leasableLife, 'lrf': lrf,
        'wacc': wacc, 'inflation': inflation, 'startingRent': startingRent}
assumptions = pd.DataFrame.from_dict(dict, orient='index')
```
