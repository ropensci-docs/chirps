# Get CHIRPS precipitation data

Get daily precipitation data from the "Climate Hazards Group". Two
server sources are available. The first, "CHC" (default) is recommended
for multiple data-points, while "ClimateSERV" is recommended when few
data-points are required (~ 50).

## Usage

``` r
get_chirps(object, dates, server, ...)

# Default S3 method
get_chirps(object, dates, server, as.matrix = FALSE, ...)

# S3 method for class 'SpatVector'
get_chirps(object, dates, server = "CHC", as.raster = TRUE, ...)

# S3 method for class 'SpatRaster'
get_chirps(
  object,
  dates,
  server = "CHC",
  as.matrix = TRUE,
  as.raster = FALSE,
  ...
)

# S3 method for class 'SpatExtent'
get_chirps(object, dates, server = "CHC", as.raster = TRUE, ...)

# S3 method for class 'sf'
get_chirps(object, dates, server, as.sf = FALSE, ...)

# S3 method for class 'geojson'
get_chirps(object, dates, server, as.geojson = FALSE, ...)

# S3 method for class 'SpatExtent'
get_chirps(object, dates, server = "CHC", as.raster = TRUE, ...)
```

## Arguments

- object:

  input, an object of class
  [`data.frame`](https://rdrr.io/r/base/data.frame.html) (or any other
  object that can be coerced to `data.frame`),
  [`SpatVector`](https://rspatial.github.io/terra/reference/SpatVector-class.html),
  [`SpatRaster`](https://rspatial.github.io/terra/reference/SpatRaster-class.html),
  [`sf`](https://r-spatial.github.io/sf/reference/sf.html) or `geojson`

- dates:

  a character of start and end dates in that order in the format
  "YYYY-MM-DD"

- server:

  a character that represents the server source "CHC" or "ClimateSERV"

- ...:

  additional arguments passed to
  [`terra`](https://rspatial.github.io/terra/reference/terra-package.html)
  or [`sf`](https://r-spatial.github.io/sf/reference/sf.html) methods
  See details

- as.matrix:

  logical, returns an object of class `matrix`

- as.raster:

  logical, returns an object of class
  [`SpatRaster`](https://rspatial.github.io/terra/reference/SpatRaster-class.html)

- as.sf:

  logical, returns an object of class
  [`sf`](https://r-spatial.github.io/sf/reference/sf.html)

- as.geojson:

  logical, returns an object of class `geojson`

## Value

A matrix, raster or a data frame of CHIRPS data:

- id:

  the index for the rows in `object`

- dates:

  the dates from which CHIRPS was requested

- lon:

  the longitude as provided in `object`

- lat:

  the latitude as provided in `object`

- chirps:

  the CHIRPS value in mm

## Details

Data description at
<https://data.chc.ucsb.edu/products/CHIRPS-2.0/README-CHIRPS.txt>

**Additional arguments when using server = "CHC"**

**resolution**: numeric, resolution of CHIRPS tiles either 0.05
(default) or 0.25 degrees

**Additional arguments when using server = "ClimateSERV"**

**dist**: numeric, buffer distance for each `object` coordinate

**nQuadSegs**: integer, number of segments per buffer quadrant

**operation**: supported operations for ClimateSERV are:

|               |     |                     |
|---------------|-----|---------------------|
| **operation** |     | **value**           |
| max           | =   | 0                   |
| min           | =   | 1                   |
| median        | =   | 2                   |
| sum           | =   | 4                   |
| average       | =   | 5 (*default value*) |

## Note

`get_chirps()` may return some warning messages given by
[`sf`](https://r-spatial.github.io/sf/reference/sf.html), please look
[sf](https://CRAN.R-project.org/package=sf) documentation for possible
issues.

## References

Funk C. et al. (2015). Scientific Data, 2, 150066.  
[doi:10.1038/sdata.2015.66](https://doi.org/10.1038/sdata.2015.66)

## Examples

``` r
if (FALSE) { # interactive()
library("chirps")
library("terra")

# Case 1: return as a data.frame
dates = c("2017-12-15","2017-12-31")
lonlat = data.frame(lon = c(-55.0281,-54.9857), lat = c(-2.8094, -2.8756))

r1 = get_chirps(lonlat, dates, server = "CHC")

# Case 2: return a matrix
r2 = get_chirps(lonlat, dates, server = "CHC", as.matrix = TRUE)

# Case 3: input SpatVector and return raster
f = system.file("ex/lux.shp", package = "terra")
v = vect(f)
r3 = get_chirps(v, dates, server = "CHC", as.raster = TRUE)

# Case 4: input SpatExtent and return a raster within the extent
area = ext(c(-66, -64, -6, -4))

dates = c("2017-12-15", "2017-12-31")

r4 = get_chirps(area, dates, server = "CHC")

# Case 5: using the server "ClimateSERV"
r5 = get_chirps(lonlat, dates, server = "ClimateSERV")

# Case 6: from "ClimateSERV" and return as a matrix
r6 = get_chirps(lonlat, dates, server = "ClimateSERV", as.matrix = TRUE)

}
```
