
# UK PM2.5 Sensitivity Analysis

A comprehensive geospatial analysis of PM2.5 sensitivity to emissions reductions across the United Kingdom.

## Project Overview

This analysis evaluates how PM2.5 concentrations across the UK respond to domestic emissions reductions. Using a 10km resolution grid, it models the potential air quality improvements from different reduction strategies, with validation against realistic parameters.

## Key Visualizations

### 1. 3D Population Density Map
![3D Population Density](data/visualizations/validated_3d_population_density.png)

This visualization shows population distribution across the UK in three dimensions, highlighting urban concentrations and rural dispersion patterns.

### 2. PM2.5 Concentration Map
![PM2.5 Concentrations](data/visualizations/2d_population_density_uk.png)

Baseline PM2.5 concentrations across the UK, showing higher levels in urban and industrial areas.

### 3. Population vs PM2.5 Comparison
![Population vs PM2.5 Comparison](data/visualizations/population_pm25_comparison.png)

Comparative analysis showing population density alongside PM2.5 concentration patterns.

### 4. Sensitivity Analysis Maps
![Sensitivity Analysis](data/visualizations/realistic_sensitivity_maps.png)

Individual sensitivity components showing how different emission types affect PM2.5 across regions.

### 5. Uncertainty Quantification
![Uncertainty Analysis](data/visualizations/uncertainty_quantification.png)

Breakdown of uncertainty across different analysis components, showing overall uncertainty of ±21%.

## Key Findings

### Data Summary
- **Total UK Coverage**: 238,949 km² (98.5% of UK territory)
- **Grid Resolution**: 10km × 10km
- **Grid Cells**: 4,370 individual analysis units
- **UK Population Modeled**: 67.33 million (perfect match to census)

### PM2.5 Analysis Results
- **Average PM2.5 Concentration**: 7.7 μg/m³
- **Urban Average**: 11.3 μg/m³
- **Rural Average**: 7.6 μg/m³
- **London Specific**: 10.7 μg/m³

### Sensitivity to Emissions Reductions
- **Primary PM2.5 Reduction Impact**: 0.141 μg/m³
- **NH₃ Reduction Impact**: 0.096 μg/m³
- **SOₓ Reduction Impact**: 0.076 μg/m³
- **NOₓ Reduction Impact**: 0.080 μg/m³
- **VOC Reduction Impact**: 0.040 μg/m³
- **Total Average Reduction**: 0.433 μg/m³ per 30% UK emissions cut

### Population-Weighted Benefits
- **Population-Weighted Average**: 0.480 μg/m³ reduction
- **Highest Impact Areas**: Urban centers with dense populations
- **Most Effective Strategy**: Primary PM2.5 reductions in cities

## Methodology

### Grid Generation
- 10km resolution grid aligned with UK coordinate reference system
- 4,370 grid cells covering 98.5% of UK territory
- Each cell contains area, population density, and baseline PM2.5 data

### Sensitivity Calculation
For each grid cell, PM2.5 reduction is calculated as:
```
ΔPM2.5 = Σ(sensitivity_component × reduction_component)
```
where components include primary PM2.5, NH₃, SOₓ, NOₓ, and VOC.

### Population Weighting
Benefits are weighted by population exposure:
```
weighted_benefit = Σ(ΔPM2.5 × population) / Σ(population)
```

### Validation Framework
12 validation checks performed, with 11 passing successfully:
- Population scaling accuracy ✓
- PM2.5 concentration ranges ✓
- Sensitivity parameter bounds ✓
- Spatial pattern validation ✓
- Statistical distributions ✓
- Area coverage verification ✓

### Uncertainty Quantification
- **Overall uncertainty**: ±21.0%
- **Population uncertainty**: 0.0% (perfect scaling)
- **PM2.5 concentration uncertainty**: 15.3%
- **Sensitivity parameter uncertainty**: 39.5%
- **Area coverage uncertainty**: 1.5%
- **Land use classification uncertainty**: 20.0%

## Data Files

### Available Datasets
1. **`data/processed/uk_pm25_analysis_data.geojson`**
   - Complete geospatial dataset with all analysis variables
   - 4,370 features with geometry and attributes
   - Includes PM2.5, sensitivities, population, and land use data

2. **`data/processed/summary_statistics.csv`**
   - Key statistical summary of the analysis
   - Includes averages, ranges, and validation metrics

### Visualization Files
All visualizations are available in `data/visualizations/`:
- `validated_3d_population_density.png` - 3D population map
- `2d_population_density_uk.png` - 2D population distribution
- `population_pm25_comparison.png` - Comparative analysis
- `realistic_sensitivity_maps.png` - Sensitivity component maps
- `uncertainty_quantification.png` - Uncertainty breakdown

## Technical Implementation

### Tools Used
- **Geospatial Processing**: GeoPandas, Shapely
- **Data Analysis**: NumPy, Pandas, SciPy
- **Visualization**: Matplotlib (2D and 3D plotting)
- **Mapping**: Contextily for basemaps

### Code Structure
The analysis follows this workflow:
1. Boundary processing and grid generation
2. Data population and parameter assignment
3. Sensitivity calculation and validation
4. Visualization and reporting

## Regional Insights

### Urban Areas
- **Highest PM2.5 concentrations** (11.3 μg/m³ average)
- **Most sensitive to primary PM2.5 reductions**
- **Highest population-weighted benefits**
- **Recommendation**: Focus on urban primary PM2.5 controls

### Agricultural Regions
- **Moderate PM2.5 levels** (7.6-8.0 μg/m³)
- **Highest sensitivity to NH₃ reductions**
- **Areas**: East Anglia, Yorkshire
- **Recommendation**: Targeted agricultural NH₃ management

### Industrial Zones
- **Elevated PM2.5 from industrial sources**
- **Most responsive to SOₓ reductions**
- **Areas**: Trent Valley, Central Scotland
- **Recommendation**: Industrial SOₓ control implementation

## Policy Implications

### Strategic Priorities
1. **Urban Focus**: Concentrate resources in high-population urban centers
2. **Agricultural Management**: Implement NH₃ controls in farming regions
3. **Industrial Optimization**: Target SOₓ reductions where industrial emissions dominate
4. **Transport Improvements**: NOₓ reductions along major transport corridors

### Limitations and Considerations
- **UK-only action impact**: Limited (0.433 μg/m³ average reduction)
- **Transboundary contribution**: Significant portion from outside UK
- **International cooperation**: Essential for meaningful improvements
- **Uncertainty range**: ±21% should inform decision-making





