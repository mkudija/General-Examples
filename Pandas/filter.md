# Filter Pandas Dataframe

### Filter by one condition
```python
df_new = df[df['AircraftType']=='S-92']
```
or
```python
df_new = df[df.AircraftType=='S-92']
```

### Filter by two conditions: this `OR` that
```python
fleet_ukn = fleet[(fleet['OperatorCountry']=='United Kingdom') | (fleet['OperatorCountry'] == 'Norway')]
```

### Filter by multiple conditions
```python
ft_less = ft[ft['Size-TRB'].isin(['1-Heavy','3-Medium','4-Lt. Twin']) & 
             ft.BuildRegion.isin(['Western']) & 
             ft.OperatorCategory.isin(['Civil']) & 
             ft.AircraftStatus.isin(['In Service','Storage'])
            ]
```
