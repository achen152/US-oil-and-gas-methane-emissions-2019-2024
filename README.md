# US oil and gas methane emissions, 2019–2024

Annual gridded oil and gas CH4 emissions for eight inversion scenarios and their arithmetic mean, at 0.5° latitude × 0.625° longitude resolution. This repository contains annual NetCDF data only.

Paper: [U.S. oil and gas methane emission intensity declined 2019–2024 with little indication of federal policy impact](https://doi.org/10.1038/s43247-026-04039-0).

## Table 1. Overview of scenarios used in this study

| Scenario | Initial Conditions | Warm-up | Wetland | Anthropogenic | Parameters* |
| ---: | --- | --- | --- | --- | --- |
| 1 | CAMS | 8 months | WetCHARTs | EDGAR v8 | 1, 25, 30, 500 |
| 2 | CAMS | 8 months | GCP | GHGI | 1, 25, 30, 500 |
| 3 | Chen et al. (2025) | 1 month | WetCHARTs | EDGAR v8 | 1, 25, 30, 500 |
| 4 | Chen et al. (2025) | 1 month | GCP | GHGI | 1, 25, 30, 500 |
| 5 | Chen et al. (2025) | 1 month | WetCHARTs | EDGAR v8 | 1, 15, 30, 500 |
| 6 | Chen et al. (2025) | 1 month | WetCHARTs | EDGAR v8 | 2, 25, 30, 500 |
| 7 | Chen et al. (2025) | 1 month | WetCHARTs | EDGAR v8 | 1, 25, 90, 500 |
| 8 | Chen et al. (2025) | 1 month | WetCHARTs | EDGAR v8 | 1, 15, 30, 200 |

\* Parameters are listed in this order: (1) square root of the diagonal elements of **Q** (10⁻¹⁰ kg m⁻² s⁻¹); (2) square root of the diagonal elements of **R** (ppb); (3) de-correlation time (days); and (4) de-correlation length (km). Scenarios 5–8 are sensitivity tests with perturbed parameters relative to baseline Scenario 3.

**Data note:** Scenarios 3 and 7 use different de-correlation times (30 and 90 days). Their annual grids differ in 2019, 2020, and 2022–2024, but are identical for 2021. The local source workbook also has identical 2021 values for these two scenarios. The reason for the 2021 equality is unresolved.

## Annual variables and units

- `oil_gas_annual_mass`: annual CH4 mass per grid cell, in kg.
- `oil_gas_annual_mass_mean`: equal-weight mean of the eight scenarios, in kg per cell.
- `oil_gas_annual_areal_mass`: annual integrated CH4 mass per unit area, in kg m-2 (NetCDF).
- Coordinates, cell bounds, cell areas, and spatial masks are included.

These are calendar-year totals, including leap days, not CO2 equivalents. Divide kg by 1e9 for Tg. Annual cell mass already includes cell area.

NetCDF dimensions are scenario, year, latitude, longitude. `scenarios.csv` contains the scenario settings shown above.

## Calculation and spatial masks

Oil and gas emissions are estimated by allocating posterior total CH4 emissions according to the oil and gas fraction in the corresponding sector-allocation prior, then integrating to annual totals. Oil and gas are allocated using prior sector proportions rather than independently optimized.

`analysis_mask` is the original land mask. Use `conus_mask` for US national totals; the land mask alone includes cells outside CONUS. Outside-analysis cells are stored as zero and should be masked for plotting.

`cell_area` is HEMCO grid-cell area. `paper_cell_area` is the area used in the original national analysis. To reproduce national totals, sum annual areal mass × `paper_cell_area` × `conus_mask`. Please cite the paper when using these data.
