# Final Project Results Notes

## Project scope

This Geo573 final project compares tract-level LST-based and Heat Index-based hotspots in Houston and Phoenix.

Houston is treated as a humid city, while Phoenix is treated as an arid city. The goal is to test whether surface-temperature-based hotspots and humidity-adjusted heat-exposure hotspots identify the same high-risk areas.

## Data and processing

- LST baseline: MODIS summer daytime LST, focused on June-July-August.
- Heat Index: humidity-adjusted thermal exposure metric.
- Spatial unit: census tracts.
- Study cities: Houston, Texas and Phoenix, Arizona.
- Hotspots: top 20% of tracts within each city for each metric.
- Comparison classes:
  - Overlap hotspot
  - LST-only hotspot
  - HI-only hotspot
  - Neither
  - Missing

## Main results

The mismatch map shows that LST-based and Heat Index-based hotspots are not identical.

Houston has visible HI-only and overlap hotspot areas, suggesting that humidity changes the spatial identification of heat exposure. Phoenix also shows mismatch, but the hotspot patterns are more spatially concentrated.

The summary metrics show low Jaccard overlap between LST and Heat Index hotspots in both cities, meaning that surface temperature alone may not fully represent human heat exposure.

## Key metrics to mention in presentation

- Houston Jaccard index: 0.214
- Phoenix Jaccard index: 0.273
- Houston overlap among valid tracts: 8.0%
- Phoenix overlap among valid tracts: 9.0%
- Houston HI-only among valid tracts: 17.5%
- Phoenix HI-only among valid tracts: 13.0%

## Contribution split

Chen Chen:
- Built the MODIS LST pipeline.
- Generated baseline LST outputs and hotspot maps.

Yufei Zhou:
- Added Heat Index comparison.
- Aggregated LST and Heat Index results to census tracts.
- Classified overlap, LST-only, HI-only, neither, and missing tracts.
- Created final mismatch maps, source hotspot panel, and summary metrics.

## Limitations

- Only two cities are included in the final comparison.
- Heat Index and LST represent different physical processes and spatial resolutions.
- Results are aggregated to census tracts, which may smooth local variation.
- Future work could expand to more cities and compare additional heat exposure metrics.
