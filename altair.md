# Snippets of Altair

## Import Altair
import altair as alt


## Histogram

```python
hist_body = alt.Chart(brain).mark_bar().encode(
    x=alt.X('Body Weight', bin=alt.Bin(maxbins=100)),
    y='count()'
).properties(
    title='Distribución del peso de los cuerpos',
    width=400
).interactive()
)

```

## Scatter Plot

```python
scatter_brain_body = alt.Chart(brain).mark_point().encode(
    x='Brain Weight',
    y='Body Weight'
).properties(
    title='Distribución del peso de los cerebros y cuerpos',
    width=800
).interactive()

```

## Bar Chart
```python
comp_trends = alt.Chart(trends).mark_bar().encode(
    x='search_term',
    y='mean(value)',
    color='search_term'
)


```


## Line Chart

```python
line_trends = alt.Chart(trends).mark_line().encode(
    x='yearmonth(date):T', #especifica que es una fecha. Para coger solo el año "year(date):T"
    y='mean(value)',
    color='search_term'
  )

```

## Map

### Horizontal concatenation
```python
comp_trends|line_trends
```

### Vertical concatenation
```python
comp_trends&line_trends
````



