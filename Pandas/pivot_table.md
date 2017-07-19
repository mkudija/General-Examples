# Pandas `pivot_table`
Date: 2017-07-18
Tags: Python, pandas, pd.pivot_table, pd.concat

### References:
- Pandas [`pivot_table` documentation](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.pivot_table.html)
- See [Pandas Pivot Table Explained](http://pbpython.com/pandas-pivot-table-explained.html) from Practical Business Python for a helpful overview.

### Simple Pivot Table
```python
table = pd.pivot_table(df2017,
                       index=['AircraftType','Year'],
                       columns=['Appraiser'],
                       values=['July 2017 CMV'],
                       margins=True,
                       margins_name='Total',
                       aggfunc=[len,np.mean])
table
```
Some notes:
- We pivot a df **`df2017`** and produce a df **`table`**
- **`index`** and **`columns`** are not both required, but at least one must be passed so there is a dimension to pivot. Each may have one or more values.
- **`values`** are what is averaged (default), or otherwise controlled by **`aggfunc`**, which may have multiple arguments.
- **`margins`** sum columns and rows

---

## Common Issues
Making a pivot table is usually easy enough, but I often find myself needing to perform a number of operations to get exactly the desired cut of data.

### Reordering Level Index
We may want to reorder the level index. For example, instead of:

<table>
  <tr>
    <td colspan="3">CMV</td>
    <td colspan="3">2017</td>
    <td colspan="3">2032</td>
  </tr>
  <tr>
    <td>Ascend</td>
    <td>Helivalues</td>
    <td>IBA</td>
    <td>Ascend</td>
    <td>Helivalues</td>
    <td>IBA</td>
    <td>Ascend</td>
    <td>Helivalues</td>
    <td>IBA</td>
  </tr>
</table>

...we want:

<table>
  <tr>
    <td colspan="3">Ascend</td>
    <td colspan="3">Helivalues</td>
    <td colspan="3">IBA</td>
  </tr>
  <tr>
    <td>CMV</td>
    <td>2017</td>
    <td>20132</td>
    <td>CMV</td>
    <td>2017</td>
    <td>CMV</td>
    <td>2017</td>
    <td>20132</td>
  </tr>
</table>

I am not aware of an easy way to do this. Because `CMV`,`2017`, and `2032` are columns and not labels in a column like `appraiser` (which has labels of Ascend, Helivalues, and IBA), we cannot simply create pivot colums from these.

Therefore the method given in the below example is to create dfs individually with the top level filter (`appraiser`) and then concatenate. Each df is housed in the dictionary `tables`, from which we concatenate the final dataframe. Note the use of `keys` in concatenation to label these top level columns.

```python
tables = {}
for appraiser in appraisers:
    tables[appraiser] = {}
    df = dfBoth[dfBoth.Appraiser==appraiser]
    tables[appraiser]['CMV'] = (pd.pivot_table(df,
                                               index=['AircraftType','Appraisal Year'],
                                               values=['CMV'],
                                               aggfunc=[len,np.sum])
                               ).round(1)
    tables[appraiser]['Base2017'] = (pd.pivot_table(df,
                                               index=['AircraftType','Appraisal Year'],
                                               values=[2017],
                                               aggfunc=[np.sum])
                               ).round(1)
    tables[appraiser]['Base2032'] = (pd.pivot_table(df,
                                               index=['AircraftType','Appraisal Year'],
                                               values=[2032],
                                               aggfunc=[np.sum])
                               ).round(1)

tablesComb = {}
for appraiser in appraisers:
    tablesComb[appraiser] = {}
    tablesComb[appraiser] = pd.concat((tables[appraiser]['CMV'],tables[appraiser]['Base2017'],tables[appraiser]['Base2032']),axis=1)

tablesAll = pd.concat((tablesComb['Ascend'],tablesComb['Helivalues'],tablesComb['IBA']),
                      axis=1,
                      keys=['Ascend', 'Helivalues', 'IBA'])
```
