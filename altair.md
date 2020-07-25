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

## Single selection

```python
select_ctry = alt.selection(type="single",encodings=["x"])

temp = weather_df.groupby(["city","country"]).mean().reset_index()

ranking_city = alt.Chart(temp).mark_bar().encode(
    x=alt.X("city",
            sort=alt.Sort(field="temp",
                          op="mean",
                          order="descending"),
            
            ),
    y="mean(temp)",
    tooltip="city"
).properties(
    width=800,
    title="Ranking de ciudades por temperatura media"
).transform_filter(
    select_ctry
)

ranking_country = alt.Chart(temp).mark_bar().encode(
    x=alt.X("country",
            sort=alt.Sort(field="temp",
                          op="mean",
                          order="descending"),
            axis=None
            ),
    y="mean(temp)",
    tooltip="country"
).properties(
    width=800,
    title="Ranking de ciudades por temperatura media",
    selection=select_ctry
)

ranking_country&ranking_city

```

## Interval Selection

```python

select_time = alt.selection(type="interval",encodings=["x"])

trends_line = alt.Chart(trends).mark_line().encode(
    x="yearmonth(date):T",
    y='mean(value)',
    color="search_term"
).properties(
    width=600,
    height=400
).transform_filter(
    select_time
)

trends_line_zoom = alt.Chart(trends).mark_line().encode(
    x="yearmonth(date):T",
    y='mean(value)',
    color="search_term"
).properties(
    width=600,
    height=100,
    selection=select_time
)

trends_line&trends_line_zoom
````
