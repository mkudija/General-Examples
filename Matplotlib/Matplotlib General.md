# Matplotlib

# Axis Format
## 1,000 Format
```python
plt.gca().yaxis.set_major_formatter(plt.FuncFormatter(lambda x, loc: "{:,}".format(int(x))))
```

## $XM Format
```python
plt.gca().yaxis.set_major_formatter(plt.FuncFormatter(lambda x, loc: "${:,}M".format(int(x/1e6))))
```

## $ format
```python
import matplotlib.ticker as mtick
yticks = mtick.FormatStrFormatter('$%1.1fmm')
plt.gca().yaxis.set_major_formatter(yticks)
```

## Date Format
```python
# format x-axis ticks as dates
import matplotlib.dates as mdates
years = mdates.YearLocator()   # every year
months = mdates.MonthLocator()  # every month
yearsFmt = mdates.DateFormatter('\n%Y')
moFmt = mdates.DateFormatter('%m') # (%b for Jan, Feb Mar; %m for 01 02 03)
ax.xaxis.set_major_locator(years)
ax.xaxis.set_minor_locator(months)
ax.xaxis.set_major_formatter(yearsFmt)
ax.xaxis.set_minor_formatter(moFmt)
```

## Grid On/Off
```python
ax.xaxis.grid(False)
```
or 
```python
plt.gca().xaxis.grid(False)
```

## Grid Style
```python
plt.gca().xaxis.grid(linestyle='-.',linewidth=.25)
```

## Axis Minimum
```python
plt.ylim(ymin=0) # yaxis min
```

# Save Fig
```python
plt.savefig(path,bbox_inches='tight')
```

or 

```python
fig = ax.get_figure()
fig.savefig(savePath, bbox_inches='tight', dpi=300) 
```

# Text & Annotations
## Chart Footer Notes
Often you will want to add chart footer notes, which may include data source, date updated, filters applied, etc. Since the range of the chart may vary based on the data, it is preferable to specify the location of these footer notes relative to the figure or axes instead of the data contained. You can do this with [`ax.annotate()`](https://matplotlib.org/users/annotations_intro.html). In this example we specify relative to `axes fraction` but other options are available. 

```python
ax.annotate('Filter: '+filtersStr, xy=(0, 0),  xycoords='figure fraction',
        xytext=(0.0, -0.2), textcoords='axes fraction',
        horizontalalignment='left', verticalalignment='center',
        )
```

Note that if you are just placing text, the position of the thing being annotated, `xy=(0,0)`, doesn't matter.

# Legend
## Legend outside of plot
```python
plt.legend(loc="upper left", bbox_to_anchor=(1,1))
```

