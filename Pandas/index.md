# Index Pandas Dataframe

See the [Pandas Documentation](https://pandas.pydata.org/pandas-docs/stable/indexing.html)

## Index

`.loc` is primarily *label*-based

`.iloc` is primarily *integer position*-based


|         | Column by Position   | Column by Label  |
| ------------- |:-------------:|:-----:|
| **Row by Position** | `df.iloc[2,3]` | `df.loc[df.index[row],'column_name']` |
| **Row by Label**    | *?* | `df.loc['row_name','column_name']` |
