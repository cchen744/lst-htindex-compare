# Thermal Metric Comparison: LST vs Heat Exposure Index

## Overview

This project compares **Land Surface Temperature (LST)** and **Heat Exposure Index (HTIndex)** to understand their spatial distribution patterns and assess how well they represent human thermal exposure in urban environments.

## Motivation

Different thermal metrics capture urban heat at different scales:

- **LST (MODIS)**: Satellite-based surface radiation, reflects material properties
- **HTIndex**: Human-centric metric (temperature + humidity), relates to thermal comfort

This project asks: **Are these metrics spatially consistent, or do they reveal fundamentally different patterns?**

## Phase 1: LST Analysis (Current)

### Data
- **Source**: MODIS MOD11A1 (Terra satellite, daytime)
- **Resolution**: 1 km
- **Period**: 2020-2024 (configurable)
- **Granularity**: Seasonal (JJA)
- **Quality**: QA-filtered pixels only (GEE-side)

### Analysis
- **Spatial clustering**: Moran's I autocorrelation
- **Hotspot detection**: High-temperature areas (>75th percentile)
- **Temporal trends**: Seasonal and yearly patterns
- **Cities**: Miami (humid subtropical), Phoenix (hot desert) — parametrized for all 7 main project cities

### Key Results
**Miami (2020-2024 JJA)**
- Mean LST: ~35.5°C
- Range: 28–38°C
- Spatial std: ~3–4°C within city

**Phoenix (2020-2024 JJA)**
- Mean LST: ~40.2°C
- Range: 30–45°C
- Spatial std: ~8–10°C within city
- Higher spatial variability → stronger UHI contrasts

## Phase 2: Heat Exposure Index (Planned)

- Apparent temperature calculations
- Humidity data integration
- Cross-metric spatial correlation
- Human thermal comfort indices (WBGT, Humidex)

## Installation

```bash
pip install ee geemap pandas numpy xarray rasterio matplotlib seaborn scipy esda
```

### GEE Setup
```python
import ee
ee.Authenticate()  # One-time, opens browser
ee.Initialize()
```

## Usage

### Basic Pipeline
```python
from lst_pipeline import create_config, LSSTPipeline

# Configure
config = create_config('Miami', start_year=2020, end_year=2024)

# Run
pipeline = LSSTPipeline(config)
results = pipeline.run()

# Results
stats_df = results['statistics']
print(stats_df.groupby('season')[['mean_temp']].mean())
```

### Spatial Visualization
```python
# Get seasonal images
seasonal_data_gee = fetcher.fetch_seasonal_data(config)

# Visualize JJA (summer)
jja_mean = ee.ImageCollection([
    seasonal_data_gee[year]['JJA'] 
    for year in seasonal_data_gee.keys() 
    if seasonal_data_gee[year]['JJA'] is not None
]).mean()

# Map
grid = jja_mean.sampleRectangle(
    defaultValue=0,
    region=config.create_geom()
).getInfo()
```

## File Structure
lst-htindex-compare/
├── README.md
├── lst_pipeline.py          # Production pipeline
├── LST_analysis.ipynb       # Demo notebook
├── outputs/
│   ├── Miami/
│   │   ├── Miami_statistics.csv
│   │   └── [visualizations]
│   └── Phoenix/
└── .gitignore

## Human Living Environment Perspective

Rather than treating LST as abstract surface temperature, this project frames it in terms of **human thermal exposure**:

- **Daytime LST**: Reflects outdoor conditions affecting pedestrians, outdoor workers
- **Spatial clustering**: Identifies neighborhoods with persistent heat stress
- **Hotspots**: Reveals where populations experience highest thermal loads
- **City comparisons**: Shows climate-dependent adaptation needs

Future HTIndex work will make the human component explicit by directly assessing **apparent temperature** (how hot it feels).

## Key Questions

1. **Spatial consistency**: Do LST and HTIndex hotspots align?
2. **Magnitude differences**: Which metric shows stronger spatial clustering?
3. **Climate dependence**: How do humid vs. arid cities differ?
4. **Policy relevance**: Which metric better represents human thermal exposure?

## Contributors

- C. Chen (cchen744@wisc.edu)
- Y. Zhou (yzhou635@wisc.edu)

## References

MODIS LST: [MOD11A1 Documentation](https://lpdaac.usgs.gov/products/mod11a1v006/)

Moran's I: [Spatial Autocorrelation](https://en.wikipedia.org/wiki/Moran%27s_I)

## License

MIT
