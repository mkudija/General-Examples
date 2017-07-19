# Pandas `pivot_table`
Date: 2017-07-18
Tags: Python, pandas, pd.pivot_table, pd.concat, pd.multiindex.droplevel, df.loc

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
Making a pivot table is usually easy enough, but I often find myself needing to perform a number of operations to get exactly the desired data format.

### Drop Level
The easiest way to get rid of the extra column headers created from the `aggfunc` is often to `droplevel`:

```python
table2017.columns = table2017.columns.droplevel(1)
```

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
    <td>2032</td>
    <td>CMV</td>
    <td>2017</td>
    <td>CMV</td>
    <td>2017</td>
    <td>2032</td>
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

### Add Calculation Rows
Let's say we have a multiindex with levels of Aircraft Type (AS332 L2) and year (2016, 2017): 

<table>
  <tr>
    <td rowspan="2">AS332 L2</td>
    <td>2016</td>
  </tr>
  <tr>
    <td>2017</td>
  </tr>
</table>

We want to add two rows for each Aircraft Type where we calculate the $ difference and % difference between the two years:

<table>
  <tr>
    <td rowspan="4">AS332 L2</td>
    <td>2016</td>
  </tr>
  <tr>
    <td>2017</td>
  </tr>
  <tr>
    <td>$ Diff</td>
  </tr>
  <tr>
    <td>% Diff</td>
  </tr>
</table>

First, we add items to the multiindex as placeholders for $ Diff and % Diff. I use `2018` and `2019` to enable later sorting. Note that we need to include all items of the index in this operation.

```python
# add $ diff and % diff to tableAll index
tablesAll.index.set_levels = [['AS332 L2', 'AS365 N3', ...], 
                              [2016,2017,2018,2019]]
```

Next, we iterate over the resulting df (with additional rows), perform the calculations, and assign these values to the appropriate column in the new rows. Note that this gives a good example of using `df.loc` on a multiindex.

```python
# add $ diff and % diff to tableAll
for appraiser in appraisers[0:3]:
    for column in ['CMV',2017,2032]:
        for ac_type in tablesAll.index.levels[0]:
            tablesAll.loc[(ac_type,2018),(appraiser,column)] = tablesAll.loc[(ac_type,2017),(appraiser,column)] - tablesAll.loc[(ac_type,2016),(appraiser,column)]
            tablesAll.loc[(ac_type,2019),(appraiser,column)] = -(1-(tablesAll.loc[(ac_type,2017),(appraiser,column)] / tablesAll.loc[(ac_type,2016),(appraiser,column)]))     
```

Finally, we reset the index which allows for manual sorting in Excel after this is [exported](https://github.com/mkudija/General-Examples/blob/master/Pandas/save-data.md) (as well as replace some values, etc.):

```python
# sort and print 
tablePrint = tablesAll.reset_index(level=1).sortlevel(level=1, sort_remaining=True)
tablePrint = tablePrint.replace([np.inf,-np.inf],'')
tablePrint.head()
```

I replace the labels `2018` and `2019` with $ Diff and % Diff in the Excel final product.

This method is not elegant, and I would love to find a better way. However, it performs *most* of what is needed to do automatically. The remaining manual step is to sort the table by `=concatenate(Aircraft Type, " - ", Year)` in Excel and past the values into the pre-formatted template, without having to worry about the calculations.
