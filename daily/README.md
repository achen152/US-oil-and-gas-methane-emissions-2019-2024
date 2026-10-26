# Daily oil and gas methane emissions

Monthly NetCDF files contain daily gridded emissions for 2019–2024, with eight scenarios and their equal-weight arithmetic mean.

- `oil_gas_daily_mass(time, scenario, lat, lon)`: kg CH4 per grid cell integrated over the indicated day.
- `oil_gas_daily_mass_mean(time, lat, lon)`: arithmetic mean of the eight daily scenario fields, in the same units.
- `time_bounds` gives each daily interval; `time` is its midpoint.

Sum daily mass over a calendar year to obtain annual cell mass. To recover daily mean flux (kg CH4 m-2 s-1), divide by `cell_area` and 86400. All days are retained, including February 29 in 2020 and 2024. Arrays use float64 with lossless NetCDF compression.

Scenario numbering follows Table 1 of the paper and `../scenarios.csv`. Coordinates, grid bounds, cell areas and the original masks are included in every file. Use `conus_mask` for US national totals. To reproduce the original paper area convention, multiply cell mass by `paper_cell_area / cell_area` before summing.

Paper: https://doi.org/10.1038/s43247-026-04039-0
