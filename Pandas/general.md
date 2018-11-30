## New column that take the part between "()" in previous column
For example, `Equipment Type` is **S-92 A (O&G)** and we want just the mission, **O&G**:
```python
df['Mission'] = df['Equipment Type'].str.extract('.*\((.*)\).*')
```


## Bins
```python
df['AircraftAgeBin'] = pd.cut(df['Age'], list(range(0,66,5)), include_lowest=True,
                              labels=['00-05yr','06-10yr','11-15yr','16-20yr','21-25yr','26-30yr','31-35yr',
                                      '36-40yr','41-45yr','46-50yr','51-55yr','56-60yr','61-65yr'])
```
