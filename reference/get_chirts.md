# Get CHIRTS temperature data

Get daily maximum and minimum temperature data from the "Climate Hazards
Group". CHIRTS-daily is a global 2-m temperature product that combines
the monthly CHIRTSmax data set with the ERA5 reanalysis to produce
routinely updated data to support the monitoring of temperature extreme.
Data is currently available from 1983 to 2016. Soon available to
near-present.

## Usage

``` r
get_chirts(object, dates, var, ...)

# Default S3 method
get_chirts(object, dates, var, as.matrix = FALSE, ...)

# S3 method for class 'SpatVector'
get_chirts(object, dates, var, as.raster = TRUE, ...)

# S3 method for class 'SpatRaster'
get_chirts(object, dates, var, as.raster = TRUE, ...)

# S3 method for class 'SpatExtent'
get_chirts(object, dates, var, as.raster = TRUE, ...)
```

## Arguments

- object:

  an object of class
  [`data.frame`](https://rdrr.io/r/base/data.frame.html) (or any other
  object that can be coerced to a `data.frame`),
  [`SpatVector`](https://rspatial.github.io/terra/reference/SpatVector-class.html),
  or
  [`SpatRaster`](https://rspatial.github.io/terra/reference/SpatRaster-class.html)

- dates:

  a character of start and end dates in that order in the format
  "YYYY-MM-DD"

- var:

  character, A valid variable from the options: “Tmax”, “Tmin”, “RHum”
  and “HeatIndex”

- ...:

  further arguments passed to
  [`terra`](https://rspatial.github.io/terra/reference/terra-package.html)

- as.matrix:

  logical, returns an object of class `matrix`

- as.raster:

  logical, returns an object of class
  [`SpatRaster`](https://rspatial.github.io/terra/reference/SpatRaster-class.html)

## Value

A SpatRaster object if `as.raster=TRUE`, else `matrix`, `list`, or
`data.frame`

## Details

Variable description from
<https://data.chc.ucsb.edu/products/CHIRTSdaily/aaa.Readme.txt>

- Tmax:

  Daily average maximum air temperature at 2 m above ground

- Tmin:

  Daily average minimum air temperature at 2 m above ground

- RHum:

  Daily average relative humidity

- HeatIndex:

  Daily average heat index

## Additional arguments

**interval**: supported intervals are “daily”, “pentad”, “dekad”,
“monthly”, “2-monthly”, “3-monthly”, and “annual”. Currently hard coded
to “daily”.

## Examples

``` r
if (FALSE) { # interactive()
library("chirps")
library("terra")

# Case 1: input a data frame return a data frame in the long format
dates = c("2010-12-15","2010-12-31")
lonlat = data.frame(lon = c(-55.0281,-54.9857),
                     lat = c(-2.8094, -2.8756))

temp1 = get_chirts(lonlat, dates, var = "Tmax")

# Case 2: input a data frame return a matrix
temp2 = get_chirts(lonlat, dates, "Tmax", as.matrix = TRUE)

# Case 3: input a raster and return raster
f = system.file("ex/lux.shp", package="terra")
v = vect(f)
temp3 = get_chirts(v, dates, var = "Tmax", as.raster = TRUE)

# Case 4: input a raster and return raster
temp4 = get_chirts(v, dates, var = "Tmax", as.matrix = TRUE)
}
```
