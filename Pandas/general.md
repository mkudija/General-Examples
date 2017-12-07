## New column that take the part between "()" in previous column
For example, `Equipment Type` is **S-92 A (O&G)** and we want just the mission, **O&G**:
```python
df['Mission'] = df['Equipment Type'].str.extract('.*\((.*)\).*')
```
