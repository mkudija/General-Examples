# Import Data into Pandas

- [Excel](#excel)
- [CSV](#csv)
- [HTML](#html)

<a id='excel'></a>
## Excel
See the [`pandas.read_excel`](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.read_excel.html) documentation.

### Simple
```python
df = pd.read_excel('path/file.xlsx')
```

### Specify Sheetname
```python
df = pd.read_excel('path/file.xlsx',
                   sheetname='Sheet 1')
```

### Skip Rows
To skip the first *n* (4 in this example) rows:
```python
df = pd.read_excel('path/file.xlsx',
                   skiprows=4)
```
To skip specified (2, 4, and 5 in this example) rows:
```python
df = pd.read_excel('path/file.xlsx',
                   skiprows=[1,3,4])
```

### Skip Footer
To skip the last *n* (1 in this example) rows:
```python
df = pd.read_excel('path/file.xlsx',
                   skip_footer=1)
```

### Specify Column Data Type
To specify the dtype of a column, use converters:
```python
df = pd.read_excel('path/file.xlsx',
                   converters={'MSN':str,'YOM':int})
```



### Full Example
In this example, we import a file, skipping the first two rows and last row from a particular sheetname, and drop an unnamed column:

```python
mile_001 = (pd.read_excel('//casloukpappv/myfile.xlsx',
                         sheetname='Asset Listing',
                         skiprows=2,
                         skip_footer=1)
            .drop('Unnamed: 0',axis=1)
           )
```

<a id='csv'></a>
## CSV
See the [`pandas.read_csv`](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.read_csv.html) documentation.

### Simple
```python
df = pd.read_csv('path/file.csv')
```

<a id='html'></a>
## HTML
See the [`pandas.read_html`](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.read_html.html) documentation.


