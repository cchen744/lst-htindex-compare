# Heat Index Analysis: LST vs Heat Index Hotspot Comparison

## Project question

How does the spatial pattern of urban heat exposure change when moving from satellite-based Land Surface Temperature (LST) to humidity-adjusted Heat Index (HI)?

## Study cities

- Houston, Texas: humid city
- Phoenix, Arizona: arid city

## Motivation

Land Surface Temperature captures surface heat from satellite observations, but it does not include humidity. Heat Index incorporates temperature and humidity and is closer to how heat is experienced by people. This project compares whether the same census tracts are identified as hotspots under LST and Heat Index.

## Workflow

1. Use existing LST baseline outputs from the MODIS JJA LST pipeline.
2. Add Heat Index data as a humidity-adjusted exposure metric.
3. Aggregate LST and Heat Index values to census tracts.
4. Define city-specific top 20% hotspot tracts for each metric.
5. Classify each tract as:
   - Overlap hotspot
   - LST-only hotspot
   - HI-only hotspot
   - Neither
   - Missing
6. Create final comparison maps and summary metrics.

## Main outputs

### Figures

- `figures/final/lst_hi_hotspot_mismatch_final_project.png`
- `figures/final/lst_hi_hotspot_mismatch_final_project.pdf`
- `figures/final/lst_hi_hotspot_source_panel_final_project.png`
- `figures/final/lst_hi_hotspot_source_panel_final_project.pdf`

### Tables

- `outputs/final_project_city_summary_metrics.csv`
- `outputs/final_project_hotspot_category_breakdown.csv`

### Notebook

- `notebooks/01_two_city_lst_hi_workflow_final_project.ipynb`

## Main findings

LST-based hotspots and Heat Index-based hotspots are not identical. The mismatch map shows that humidity-adjusted exposure can identify different hotspot tracts than satellite-based surface temperature alone. This suggests that LST alone may not fully capture human heat exposure.

## Team contributions

Chen Chen:
- Built the MODIS LST pipeline.
- Generated baseline LST statistics and hotspot visualizations.

Yufei Zhou:
- Added Heat Index comparison.
- Created tract-level hotspot classifications.
- Generated final mismatch maps and summary metrics.
