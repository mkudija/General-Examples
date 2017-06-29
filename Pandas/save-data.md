# Save Data from Pandas to File

```python
save = 'xls'
if save=='csv':
    df.to_csv('name.csv', index=False)
elif save=='xls':
    from pandas import ExcelWriter
    writer = ExcelWriter(name.xlsx')
    df.to_excel(writer, sheet_name='Sheet 1', index=False)
    writer.save()
```
