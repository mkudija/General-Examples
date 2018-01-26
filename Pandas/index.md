# Index Pandas Dataframe

See the [Pandas Documentation](https://pandas.pydata.org/pandas-docs/stable/indexing.html)

## Index

`.loc` is primarily *label*-based

`.iloc` is primarily *integer position*-based

### Value Selection Matrix
In different situations, it can be helpful to select a value from a dataframe by using different combinations of position and label identify the column and row of the value. The following chart gives a quick reference for each combination.

|         | Column by Position   | Column by Label  |
| ------------- |:-------------:|:-----:|
| **Row by Position** | `df.iloc[2,3]` | `df.loc[df.index[1],'column_name']` <br> or <br> `df.iloc[1,df.columns.get_loc('column_name')]` |
| **Row by Label**    | `df.loc['row_name',df.columns[1]]` <br> or <br> `df.iloc[df.index.get_loc('row_name'),1]` | `df.loc['row_name','column_name']` |

tags: python, pandas, index, select
