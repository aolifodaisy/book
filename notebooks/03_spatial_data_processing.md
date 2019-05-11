---
jupyter:
  jupytext:
    formats: ipynb,md
    text_representation:
      extension: .md
      format_name: markdown
      format_version: '1.1'
      jupytext_version: 1.1.1
  kernelspec:
    display_name: Python 3
    language: python
    name: python3
---

<!-- #region {"deletable": true, "editable": true} -->
# Spatial Data Processing

Intro paragraph
* deterministic spatial analysis (SG)

* Explain what we mean by dsa
* outline what we will cover below


 airports.csv
<!-- #endregion -->

<!-- #region {"deletable": true, "editable": true} -->
## Vignette: Airports
<!-- #endregion -->

<!-- #region {"deletable": true, "editable": true} -->
- Querying based on attributes (volume, lon/lat, etc.)
<!-- #endregion -->

```python deletable=true editable=true
import pysal as ps
import pandas as pd
df = pd.read_csv("data/airports/world-airports.csv")
```

```python
df.head()
```

Let's use pandas to query for the airports within the `large_airport` class:

```python
df[df.type == 'large_airport']
```

<!-- #region {"deletable": true, "editable": true} -->
Since both latitude and longitude are columns in the dataframe we can use pandas to carry out a limited number of geospatial queries. For example, extract all the airports in the northern hemisphere:
<!-- #endregion -->

```python
df[df.latitude_deg > 0.0]
```

<!-- #region {"deletable": true, "editable": true} -->
- Subsetting (querying but return dataframe not just indices)
<!-- #endregion -->

```python
gb = df.groupby('type')
```

```python
gb.all()
```

```python
small = df[df.type=='small_airport']
medium = df[df.type=='medium_airport']
large = df[df.type=='large_airport']
```

```python
len(small)
```

```python
len(medium)
```

```python
len(large)
```

<!-- #region {"deletable": true, "editable": true} -->
- spatial join - airports by countries
<!-- #endregion -->

```python deletable=true editable=true
countries_shp = ps.pdio.read_files("data/airports/ne_10m_admin_0_countries/ne_10m_admin_0_countries.shp")
```

```python

```

```python

```

<!-- #region {"deletable": true, "editable": true} -->
- derived features - point sequence to line for the routes
- spatial join - does route pass through a country
- crs: contextily example, 
- knn analysis - find most isolated airport
- voronoi - whats my closest airport
- dissolve - dissovle boundaries in europe
<!-- #endregion -->

## Vignette: House Prices

```python
df = pd.read_csv('data/sandiego/listings.csv')
len(df)
```

```python
df.columns
```

<!-- #region {"deletable": true, "editable": true} -->
- keyword table join (census)
(keyword comes from spatial join with polygon shown below)

- groupby: avg house price by census polygon
- buffer: deriving dummies for houses within x of an amenity
- spatial join: create keyword that we use for the table
- raster/clip with shape: elevation or pollution by tract, or by house, or  noise
- voronoi - what's my closest coffee shop

- Sets: union, intersection, difference: point out that these are really implied by the buffer used to define regimes (intersection dummy = 1, difference dummy=0)

message is, if you have the column in the table use it, but many cases you do not have the column and need to go the spatial join route
<!-- #endregion -->