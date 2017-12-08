# Pickle

I have a lot of code that [reads](https://github.com/mkudija/General-Examples/blob/master/Pandas/import-data.md) and [writes](https://github.com/mkudija/General-Examples/blob/master/Pandas/save-data.md) to `.xlsx` or `.csv` files. It can take a suprising amount of time to read and write these files, especially when you have a script that is passing a lot of data around.

While sometimes we want to save these to be able to open in Excel, often times we just want to manipulate the data with Python for consumption in another format (chart, webpage, etc.). In these cases, it can save time to export your data as a Pickle (`.p`) file.

[Pickle](https://pythontips.com/2013/08/02/what-is-pickle-in-python/) is "used for serializing and de-serializing a Python object structure": read more in the [official docs](https://docs.python.org/2/library/pickle.html). Since I usually work in pandas, we can use the [`DataFrame.to_pickle`](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.DataFrame.to_pickle.html) and [`DataFrame.read_pickle`](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.read_pickle.html) methods.

In this example, we pickle all the `.xlsx` files in the current directory:

```python
import pandas as pd
from pathlib import Path

files = Path.cwd().glob('*.xlsx')
for file in files:
	print('{}'.format(file.name))
	print('\tReading Excel')
	df = pd.read_excel(file)
	print('\tSaving pickle')
	df.to_pickle('pickle/'+file.stem+'.p')
```

Then, when we want to use this data, we can simple import it back into pandas:
```python
df = pd.read_pickle('pickled.p')
```
