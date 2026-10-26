# US oil and gas methane emissions, 2019–2024

Annual and daily gridded oil and gas CH4 emissions for eight inversion scenarios and their arithmetic mean, at 0.5° latitude × 0.625° longitude resolution.

Paper: https://doi.org/10.1038/s43247-026-04039-0

The annual NetCDF and MATLAB files contain the same data. Daily files are in [`daily/`](daily/), with one NetCDF per month containing all eight scenarios and the daily ensemble mean. See the [daily data description](daily/README.md) for variables and units. `scenarios.csv` identifies the posterior run and sector-allocation prior for each scenario.

## Annual variables and units

- `oil_gas_annual_mass`: annual CH4 mass per grid cell, in kg.
- `oil_gas_annual_mass_mean`: equal-weight mean of the eight scenarios, in kg per cell.
- `oil_gas_annual_areal_mass`: annual integrated CH4 mass per unit area, in kg m-2 (NetCDF).
- Coordinates, cell bounds (NetCDF), cell areas and spatial masks are included.

These are calendar-year totals, including leap days, not CO2 equivalents. Divide kg by 1e9 for Tg. Annual cell mass already includes cell area.

NetCDF dimensions are scenario, year, latitude, longitude. MATLAB mass arrays are longitude, latitude, year, scenario; the mean is longitude, latitude, year. MATLAB variable names include unit suffixes, e.g. `oil_gas_annual_mass_kg`.

## Calculation

For each day, oil and gas flux is the posterior total CH4 flux multiplied by (prior Oil + prior Gas) / prior Total, using the corresponding prior. Daily values are integrated over each year. Oil and gas are allocated using prior sector proportions, rather than independently optimized.

`analysis_mask` is the original land mask. Use `conus_mask` for US national totals; the land mask alone includes cells outside CONUS. Outside-analysis cells are stored as zero and should be masked for plotting.

`cell_area` is HEMCO grid-cell area. `paper_cell_area` is the area used in the original national analysis. To reproduce national totals, sum annual areal mass × `paper_cell_area` × `conus_mask`. In MATLAB these area variables are `cell_area_m2` and `paper_cell_area_m2`.

Please cite the paper when using these data.
