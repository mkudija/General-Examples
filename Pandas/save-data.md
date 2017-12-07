# Save Data from Pandas to File

## XLSX
```python
writer = pd.ExcelWriter('name.xlsx')
df.to_excel(writer, sheet_name='Sheet 1', index=False)
writer.save()
```

## CSV or XLSX
```python
save = 'xls'
if save=='csv':
    df.to_csv('name.csv', index=False)
elif save=='xls':
    writer = pd.ExcelWriter('name.xlsx')
    df.to_excel(writer, sheet_name='Sheet 1', index=False)
    writer.save()
```

## Customize XLSX Format

See [here](http://xlsxwriter.readthedocs.io/example_pandas_column_formats.html) and [here](http://pbpython.com/improve-pandas-excel-output.html) for more examples.

```python
sheetname = 'ID'
writer = pd.ExcelWriter(filename+'.xlsx', engine='xlsxwriter')
df.to_excel(writer, sheet_name=sheetname, index=False)

# get xlsxwriter objects
workbook  = writer.book
worksheet = writer.sheets[sheetname]
worksheet.hide_gridlines(2)

# define formats
date_fmt = workbook.add_format({'align': 'center', 'num_format': 'yyyy-mm-dd'})
center_fmt = workbook.add_format({'align': 'center'})
number_fmt = workbook.add_format({'align': 'center', 'num_format': '#,##0.000'})
cur_fmt = workbook.add_format({'align': 'center', 'num_format': '$#,##0.00'})
perc_fmt = workbook.add_format({'align': 'center', 'num_format': '0%'})
grey_fmt = workbook.add_format({'font_color': '#B1B3B3'})

# set column width and format over columns
worksheet.set_column('A:A', 13, center_fmt)
worksheet.set_column('B:B', 12, center_fmt)
worksheet.set_column('C:C', 12)
worksheet.set_column('D:E', 9, center_fmt)
worksheet.set_column('F:G', 12, center_fmt)
worksheet.set_column('H:H', 16, center_fmt)
worksheet.set_column('I:I', 23, center_fmt)
worksheet.set_column('J:AR', 6, number_fmt)

# set format over range
worksheet.conditional_format('J6:AR9', {'type': 'cell',
                             'criteria': '>=',
                             'value': 0, 'format': perc_fmt})
# save
writer.save()
```
