# Get evaporative stress index (ESI) data

Get evaporative stress index (ESI) from SERVIR Global via ClimateSERV
API Client. ESI is available every four (or twelve) weeks from 2001 to
present. The dataset may contain cloudy data which is returned as `NA`s.
ClimateSERV works with 'geojson' of type 'Polygon'. The input `object`
is then transformed into polygons with a small buffer area around the
point.

## Usage

``` r
get_esi(object, dates, operation = 5, period = 1, ...)

# Default S3 method
get_esi(object, dates, operation = 5, period = 1, ...)

# S3 method for class 'sf'
get_esi(object, dates, operation = 5, period = 1, as.sf = FALSE, ...)

# S3 method for class 'geojson'
get_esi(object, dates, operation = 5, period = 1, as.geojson = FALSE, ...)
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

- operation:

  optional, an integer that represents which type of statistical
  operation to perform on the dataset

- period:

  an integer value for the period of ESI data, four weeks period = 1,
  twelve weeks = 2

- ...:

  additional arguments passed to
  [`terra`](https://rspatial.github.io/terra/reference/terra-package.html)
  or [`sf`](https://r-spatial.github.io/sf/reference/sf.html) methods
  See details

- as.sf:

  logical, returns an object of class
  [`sf`](https://r-spatial.github.io/sf/reference/sf.html)

- as.geojson:

  logical, returns an object of class `geojson`

## Value

A data frame of ESI data:

- id:

  the index for the rows in `object`

- dates:

  the dates from which ESI was requested

- lon:

  the longitude as provided in `object`

- lat:

  the latitude as provided in `object`

- esi:

  the ESI value

## Details

**operation**: supported operations are:

|               |     |                     |
|---------------|-----|---------------------|
| **operation** |     | **value**           |
| max           | =   | 0                   |
| min           | =   | 1                   |
| median        | =   | 2                   |
| sum           | =   | 4                   |
| average       | =   | 5 (*default value*) |

**dist**: numeric, buffer distance for each `object` coordinate

**nQuadSegs**: integer, number of segments per buffer quadrant

## Note

`get_esi()` may return some warning messages given by
[`sf`](https://r-spatial.github.io/sf/reference/sf.html), please check
the [sf](https://CRAN.R-project.org/package=sf) documentation for
possible issues.

## Examples

``` r
if (FALSE) { # interactive()

lonlat = data.frame(lon = c(-55.0281,-54.9857),
                     lat = c(-2.8094, -2.8756))

dates = c("2017-12-15","2018-06-20")

# by default the function sets a very small buffer around the points which
# can return NAs due to cloudiness in ESI data

dt = get_esi(lonlat, dates = dates)

# the argument dist passed through sf increase the buffer area

dt = get_esi(lonlat, dates = dates, dist = 0.1)
}
```
