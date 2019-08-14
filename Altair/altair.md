# Altair

## Rolling mean on multi series line chart

Computes rolling mean of this [multi-series line chart](https://altair-viz.github.io/gallery/multi_series_line.html):

```python
import altair as alt
from vega_datasets import data

alt.Chart(data.stocks.url).transform_window(
    price_mean = 'mean(price)',
    frame = [-5,5],
    groupby = ['symbol:N']
).mark_line().encode(
    x='date:T',
    y='price_mean:Q',
    color='symbol:N',
)
```
