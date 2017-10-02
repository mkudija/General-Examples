# Matplotlib

# Axis Format
## 1,000 Format
```python
plt.gca().yaxis.set_major_formatter(plt.FuncFormatter(lambda x, loc: "{:,}".format(int(x))))
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

# Save Fig
```python
plt.savefig(path,bbox_inches='tight')
```
