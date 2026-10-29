# Get raw CHIRTS-ERA5 raster data

Download CHIRTS-ERA5 daily temperature data in its original raster
format.

## Usage

``` r
get_chirts_era5_raw(
  dates,
  var = c("Tmin", "Tmax"),
  use_vsicurl = FALSE,
  verbose = FALSE,
  ...
)
```

## Arguments

- dates:

  Character vector of length two with start and end dates in
  `"YYYY-MM-DD"` format.

- var:

  Character. Variable to download. Supported values are `"Tmin"` and
  `"Tmax"`.

- use_vsicurl:

  Logical. If `TRUE`, prepends `"/vsicurl"` to remote URLs.

- verbose:

  Logical. If `TRUE`, prints the URLs used.

- ...:

  Additional arguments reserved for future use.

## Value

A
[`SpatRaster`](https://rspatial.github.io/terra/reference/SpatRaster-class.html)
with one layer per day.

## Details

CHIRTS-ERA5 is a quasi-global (60°S to 70°N), high-resolution (0.05° ×
0.05°) dataset of daily maximum and minimum temperatures, heat index,
and wet bulb globe temperature from 1980 to near-present.

The dataset combines the Climate Hazards Center Infrared Temperature
with Stations (CHIRTS) product (1983–2016) with the regularly updated
ERA5 reanalysis. ERA5 fields are downscaled and bias-corrected relative
to CHIRTS to provide a temporally consistent climate record.

Users of this dataset should cite:

"CHIRTS-ERA5 Data Repository. https://doi.org/10.15780/G2F08J. Data
accessed on \[DATE\]."

Additional information is available at:
<https://www.chc.ucsb.edu/data/chirts-era5>

## References

Climate Hazards Center (CHC). CHIRTS-ERA5 Data Repository.
[doi:10.15780/G2F08J](https://doi.org/10.15780/G2F08J)

## Examples

``` r
if (interactive()) {
  tmin = get_chirts_era5_raw(dates = c("1980-01-01", "1980-01-31"),
                             var = "Tmin")

  tmax = get_chirts_era5_raw(dates = c("1980-01-01", "1980-01-31"),
                             var = "Tmax")
}
```
