# Get Integrated Multisatellite Retrievals for GPM (IMERG) data

The IMERG dataset provides near-real time global observations of
rainfall at 10km resolution, which can be used to estimate total
rainfall accumulation from storm systems and quantify the intensity of
rainfall and flood impacts from tropical cyclones and other storm
systems. IMERG is a daily precipitation dataset available from 2015 to
present within the latitudes 70 and -70 degrees.

## Usage

``` r
get_imerg(object, dates, operation = 5, ...)

# Default S3 method
get_imerg(object, dates, operation = 5, ...)

# S3 method for class 'sf'
get_imerg(object, dates, operation = 5, as.sf = FALSE, ...)

# S3 method for class 'geojson'
get_imerg(object, dates, operation = 5, as.geojson = FALSE, ...)
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

A data frame of imerg data:

- id:

  the index for the rows in `object`

- dates:

  the dates from which imerg was requested

- lon:

  the longitude as provided in `object`

- lat:

  the latitude as provided in `object`

- imerg:

  the IMERG value

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

## Examples

``` r
if (FALSE) { # interactive()
lonlat <- data.frame(lon = c(-55.0281,-54.9857),
                     lat = c(-2.8094, -2.8756))

dates <- c("2017-12-15", "2017-12-31")

dt <- get_imerg(lonlat, dates)

dt
}
```
