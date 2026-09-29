# Methods to coerce geographical coordinates into a geojson polygon

Take single points from geographical coordinates and coerce into a
geojson of geometry 'Polygon'

## Usage

``` r
as.geojson(lonlat, dist = 1e-05, nQuadSegs = 2L, ...)

# Default S3 method
as.geojson(lonlat, dist = 1e-05, nQuadSegs = 2L, ...)

# S3 method for class 'sf'
as.geojson(lonlat, dist = 1e-05, nQuadSegs = 2L, ...)
```

## Arguments

- lonlat:

  a `data.frame` or matrix with geographical coordinates 'lonlat', in
  that order, or an object of class
  [`sf`](https://r-spatial.github.io/sf/reference/sf.html) with geometry
  type 'POINT' or 'POLYGON'

- dist:

  numeric, buffer distance for all `lonlat`

- nQuadSegs:

  integer, number of segments per quadrant

- ...:

  further arguments passed to
  [`sf`](https://r-spatial.github.io/sf/reference/sf.html) methods

## Value

An object of class 'geosjon' for each row in `lonlat`

## Examples

``` r
if (FALSE) { # interactive()
# Default S3 Method
# random geographic points within bbox(10, 12, 45, 47)
library("sf")

set.seed(123)
lonlat = data.frame(lon = runif(1, 10, 12),
                     lat = runif(1, 45, 47))

gjson = as.geojson(lonlat)

#################

# S3 Method for objects of class 'sf'
# random geographic points within bbox(10, 12, 45, 47)
library("sf")

set.seed(123)
lonlat = data.frame(lon = runif(5, 10, 12),
                     lat = runif(5, 45, 47))

lonlat = st_as_sf(lonlat, coords = c("lon","lat"))

gjson = as.geojson(lonlat)
}
```
