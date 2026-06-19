A **Spatial Data Cube** extends the traditional data cube concept (used in OLAP) to handle **spatial data**. In a standard data cube, dimensions are typically non-spatial (e.g., time, product, city name). In a spatial data cube, dimensions can be **spatial** or **non-spatial**, and measures can be **spatial** or **non-spatial** as well.

The three categories you asked about refer to different ways dimensions and measures are classified based on whether they contain spatial properties (geometry, location, shape, topology).

**"Geographical locations are represented using these mathematical concepts points, lines, polygons, and THAT is spatial data."**


```
note : 
- **Dimensions** are the **"who, what, where, and when"**—they are the **categories or filters** you use to slice and group your data. (e.g., _Time, Product Category, Store Location, Customer Age Group_).
    
- **Measures** are the **"how much"**—they are the **numeric facts** you are actually analyzing. (e.g., _Total Sales Dollars, Number of Units Sold, Profit_).
```

---
## 1. Non-Spatial Dimension

In this case, **both the dimension and the measure are non-spatial**, but the data is organized using a spatial context or hierarchy.

### Characteristics:
- Dimensions are standard categorical or numerical attributes (e.g., time, product type, age group).
- Measures are aggregated using traditional functions (SUM, COUNT, AVG).
- The cube is **sliced or filtered** by spatial regions (e.g., city, state, country), but those regions are treated as labels, not as geometric objects.

### Example:
- **Dimension**: Year (2020, 2021, 2022) → non-spatial.
- **Measure**: Total sales amount → non-spatial.
- **Spatial context**: Sales grouped by `City` (but City is just a name; no geometry used in aggregation).

### SQL-like OLAP query:
```sql
SELECT City, Year, SUM(SalesAmount)
FROM SalesTable
GROUP BY City, Year;
```
Here, `City` is a label, not a spatial object. No distances, adjacencies, or shapes are considered.

---

## 2. Spatial-to-Non-Spatial Dimension

Here, **dimensions are spatial**, but **measures are non-spatial**. Aggregation is performed over spatial extents, but the result is a standard numeric or categorical value.

### Characteristics:
- Dimensions represent spatial objects or regions (e.g., polygons, points, lines).
- Measures are non-spatial (e.g., count of crimes, average temperature, total population).
- Aggregation often uses **spatial operations** like `inside`, `contains`, `intersects`, `within distance`.

### Example:
- **Spatial dimension**: `Neighborhood` (polygon geometry).
- **Non-spatial measure**: Average house price (number).
- **Query**: “For each neighborhood, compute the average price of houses located entirely inside it.”

### Another example:
- **Spatial dimension**: `Distance zone` (buffers around a hospital: 0–1 km, 1–2 km, 2–5 km).
- **Non-spatial measure**: Count of ambulance calls.

### Key point:
The grouping is based on **spatial relationships**, but what you get back is a table of numbers (non-spatial). For instance:  

| Zone (spatial) | Avg Response Time (non-spatial) |
|----------------|----------------------------------|
| 0–1 km         | 4.2 min                          |
| 1–2 km         | 6.7 min                          |

---

## 3. Spatial-to-Spatial Dimension

Here, **both the dimensions and the measures are spatial**. This is the most complex case, where aggregation yields new spatial objects (e.g., centroids, unions, convex hulls, or density surfaces).

### Characteristics:
- Dimensions are spatial (e.g., regions, points, lines).
- Measures are also spatial (e.g., geometry of a cluster, a road network, a density heatmap).
- Aggregation functions are **spatial**:
  - `Union` (merge geometries)
  - `Intersection`
  - `Centroid` (point representing a region)
  - `ConvexHull`
  - `Buffer`
  - `SpatialClustering` (e.g., DBSCAN)

### Example 1:
- **Spatial dimension**: `Earthquake epicenter points`.
- **Spatial measure**: `Convex hull` (smallest polygon containing all points in a given cell).
- **Result**: A set of polygons representing the spread of earthquakes per spatial cell.

### Example 2:
- **Spatial dimension**: `ZIP code polygon`.
- **Spatial measure**: `Centroid` of all store locations inside each ZIP code.
- **Result**: A point layer where each point represents the “center” of stores per ZIP code.

### Example 3 (advanced):
- **Spatial dimension**: `City boundary`.
- **Spatial measure**: `Line union` of all roads in that city.
- **Result**: A merged road network geometry per city.

### Visualization:
| City (spatial polygon) | Aggregated Road Network (spatial line) |
|------------------------|----------------------------------------|
| Polygon A              | MultiLineString                        |
| Polygon B              | MultiLineString                        |

---

## Summary Table

| Type                   | Dimension Type | Measure Type | Example                                             | Aggregation Function        |
| ---------------------- | -------------- | ------------ | --------------------------------------------------- | --------------------------- |
| Non-Spatial Dimension  | Non-spatial    | Non-spatial  | Sales by City (as label) and Year                   | SUM, COUNT, AVG             |
| Spatial-to-Non-Spatial | Spatial        | Non-spatial  | Avg house price per neighborhood polygon            | Spatial join + numeric AVG  |
| Spatial-to-Spatial     | Spatial        | Spatial      | Convex hull of earthquake points per region polygon | Union, Centroid, ConvexHull |

---

## Why does this matter in spatial data mining?

- **Non-spatial dimensions** → Traditional OLAP on spatial data (e.g., drill down by region name).
- **Spatial-to-non-spatial** → Discover patterns like “high crime density near highways” (spatial grouping → numeric measure).
- **Spatial-to-spatial** → Create new spatial layers for further mining, e.g., generating a map of clustering polygons or density surfaces.

A **Spatial Data Cube** is typically implemented in spatial databases (PostGIS, Oracle Spatial) or GIS-aware OLAP tools (GeoCube, spatial extensions to MDX).

---

## [[Mining Spatial Associations]]

