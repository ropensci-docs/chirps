# Compute precipitation indices over a time series

Compute precipitation indices over a time series

## Usage

``` r
precip_indices(object, timeseries = FALSE, intervals = NULL)
```

## Arguments

- object:

  an object of class `chirps` as provided by
  [`get_chirps`](https://docs.ropensci.org/chirps/reference/get_chirps.md)

- timeseries:

  logical, `FALSE` for a single point time series observation or `TRUE`
  for a time series based on `intervals`

- intervals:

  integer no lower than 5, for the days intervals when `timeseries` =
  `TRUE`

## Value

A data frame with precipitation indices:

- MLDS:

  maximum length of consecutive dry day, rain \< 1 mm (days)

- MLWS:

  maximum length of consecutive wet days, rain \>= 1 mm (days)

- R10mm:

  number of heavy precipitation days 10 \>= rain \< 20 mm (days)

- R20mm:

  number of very heavy precipitation days rain \>= 20 (days)

- Rx1day:

  maximum 1-day precipitation (mm)

- Rx5day:

  maximum 5-day precipitation (mm)

- R95p:

  total precipitation when rain \> 95th percentile (mm)

- R99p:

  total precipitation when rain \> 99th percentile (mm)

- Rtotal:

  total precipitation (mm) in wet days, rain \>= 1 (mm)

- SDII:

  simple daily intensity index, total precipitation divided by the
  number of wet days (mm/days)

## References

Aguilar E., et al. (2005). Journal of Geophysical Research, 110(D23),
D23107.

Kehel Z., et al. (2016). In: Applied Mathematics and Omics to Assess
Crop Genetic Resources for Climate Change Adaptive Traits (eds Bari A.,
Damania A. B., Mackay M., Dayanandan S.), pp. 151–174. CRC Press.

## Examples

``` r
if (FALSE) { # interactive()
lonlat = data.frame(lon = c(-55.0281,-54.9857),
                     lat = c(-2.8094, -2.8756))

dates = c("2017-12-15", "2017-12-31")

dt = get_chirps(lonlat, dates, server = "ClimateSERV")

# take the indices for the entire period
precip_indices(dt, timeseries = FALSE)

# take the indices for periods of 7 days
precip_indices(dt, timeseries = TRUE, intervals = 7)
}
```
