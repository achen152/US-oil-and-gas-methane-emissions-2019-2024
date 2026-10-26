# US oil and gas methane emissions, 2019–2024

Annual mean oil and gas CH4 emission grids from the [study](https://doi.org/10.1038/s43247-026-04039-0), at **0.5° latitude × 0.625° longitude** resolution.

Each NetCDF file contains one calendar year's grid, averaged across the original study ensemble. There are six files, one for each year from 2019 to 2024. These are annual fields, not a mean across the six years.

## Data and units

- `oil_gas_annual_mass_mean(lat, lon)`: **kg CH4 per grid cell**, integrated over the calendar year identified by `year`.
- `lat`, `lon`, `lat_bounds`, `lon_bounds`: grid coordinates and bounds in degrees.
- `cell_area` and `paper_cell_area`: grid-cell areas in m².
- `analysis_mask` and `conus_mask`: original analysis and contiguous-US masks.

Cell area is already included in the mass variable. Sum grid-cell masses within the desired region to obtain its annual emissions; use fractional overlap for boundary cells if needed. Divide kg by 10⁹ to convert to Tg CH4. These are CH4 masses, not CO2 equivalents.

The files preserve the original study's annual ensemble means. Oil and gas emissions were allocated from posterior total CH4 using prior sector fractions. They cover the inventory Oil + Gas sectors, not only upstream production.

## Spatial masks

The analysis grid includes land outside the contiguous United States. Use `conus_mask` for CONUS totals. Outside-analysis cells are stored as zero and should be masked when plotting.

To reproduce the paper's national integration convention, calculate:

`sum(oil_gas_annual_mass_mean * paper_cell_area / cell_area * conus_mask) / 1e9`

The result is Tg CH4 for that year. Please cite the paper when using these data.
