
# UK PM2.5 Sensitivity Analysis

A geospatial analysis of how PM2.5 concentrations across the United Kingdom respond to domestic emissions reductions.

## Overview

This project analyzes the potential impact of UK emissions reductions on PM2.5 air quality. Using a 10km resolution grid covering the UK, it models how different types of emissions reductions (primary PM2.5, NH₃, SOₓ, NOₓ, VOC) might affect PM2.5 concentrations across different regions and population centers.

The analysis includes validation against realistic parameters and uncertainty quantification, providing a framework for understanding the technical possibilities and limitations of domestic air quality improvements.

## Key Features

- **10km resolution grid** covering 98.5% of UK territory
- **Realistic population distribution** scaled to UK census data
- **Multi-component sensitivity analysis** for different emission types
- **Validation framework** with parameter checking
- **Uncertainty quantification** across all analysis components
- **Geospatial visualizations** including 3D population density maps
- **Reproducible workflow** with documented methodology

## Project Structure

```
uk-pm25-sensitivity-analysis/
├── data/                    # Data files and outputs
│   ├── processed/          # Processed analysis data
│   ├── visualizations/     # Generated plots and maps
│   └── reports/           # Analysis reports
├── notebooks/              # Jupyter notebooks
│   ├── 01_data_preparation.ipynb
│   ├── 02_analysis_core.ipynb
│   └── 03_visualization.ipynb
├── src/                    # Source code
│   ├── data_processing.py
│   ├── analysis.py
│   ├── validation.py
│   └── visualization.py
├── environment.yml         # Conda environment
├── requirements.txt        # Pip requirements
└── README.md
```

## Installation

### Using Conda (Recommended)

```bash
# Clone the repository
git clone https://github.com/yourusername/uk-pm25-sensitivity-analysis.git
cd uk-pm25-sensitivity-analysis

# Create and activate conda environment
conda env create -f environment.yml
conda activate uk-pm25-analysis
```

### Using pip

```bash
pip install -r requirements.txt
```

## Usage

### Running the Complete Analysis

```python
# In a Jupyter notebook or Python script
from src.data_processing import load_uk_boundaries, generate_grid
from src.analysis import run_sensitivity_analysis
from src.validation import validate_results
from src.visualization import create_visualizations

# Load UK boundaries
uk_boundary = load_uk_boundaries()

# Generate analysis grid
grid = generate_grid(uk_boundary, resolution_km=10)

# Run sensitivity analysis
results = run_sensitivity_analysis(grid)

# Validate results
validation_report = validate_results(results)

# Create visualizations
create_visualizations(results, uk_boundary)
```

### Step-by-step in Notebooks

1. **Data Preparation** (`notebooks/01_data_preparation.ipynb`):
   - Load UK boundary data
   - Create analysis grid
   - Generate synthetic PM2.5 and population data

2. **Core Analysis** (`notebooks/02_analysis_core.ipynb`):
   - Calculate sensitivity to emissions reductions
   - Apply population weighting
   - Perform regional breakdowns

3. **Visualization** (`notebooks/03_visualization.ipynb`):
   - Create 3D population density maps
   - Generate sensitivity analysis plots
   - Build uncertainty visualization

## Methodology

### Grid Generation
- 10km resolution grid aligned with UK coordinate system
- Covers 4370 grid cells across UK territory
- Each cell contains area, population, and baseline PM2.5 data

### Sensitivity Calculation
For each grid cell, calculates PM2.5 reduction per 30% emissions reduction:
```
ΔPM2.5 = sensitivity_primary × reduction_primary + 
         sensitivity_nh3 × reduction_nh3 + 
         sensitivity_sox × reduction_sox + 
         sensitivity_nox × reduction_nox + 
         sensitivity_voc × reduction_voc
```

### Population Weighting
Benefits are weighted by population density:
```
population_weighted_benefit = Σ(ΔPM2.5 × population) / Σ(population)
```

### Validation
12 validation checks covering:
- Population scaling accuracy
- PM2.5 concentration ranges
- Sensitivity parameter bounds
- Spatial pattern consistency
- Statistical distribution properties

### Uncertainty Quantification
Uncertainty estimated across:
- Population distribution (±0%)
- PM2.5 concentrations (±15.3%)
- Sensitivity parameters (±39.5%)
- Spatial coverage (±1.5%)
- Land use classification (±20.0%)

**Overall uncertainty:** ±21.0%

## Results

### Key Findings
- **Average PM2.5 reduction**: 0.433 μg/m³ per 30% UK emissions reduction
- **Population-weighted benefit**: 0.480 μg/m³ reduction
- **Urban vs rural**: Urban areas (11.3 μg/m³) show higher PM2.5 than rural (7.6 μg/m³)
- **Spatial variation**: Different regions respond to different emission types

### Regional Patterns
- **Urban areas**: Most sensitive to primary PM2.5 reductions
- **Agricultural regions**: Highest NH₃ sensitivity
- **Industrial zones**: Most responsive to SOₓ reductions
- **Transport corridors**: Benefit most from NOₓ reductions

## Output Files

### Data Files
- `uk_pm25_analysis_grid.geojson` - Complete analysis grid with all variables
- `sensitivity_results.csv` - Tabular results by grid cell
- `regional_summary.csv` - Aggregated results by UK region
- `validation_report.json` - Complete validation results

### Visualizations
- `population_density_3d.png` - 3D population distribution map
- `pm25_baseline_map.png` - Baseline PM2.5 concentrations
- `sensitivity_maps/` - Individual sensitivity component maps
- `uncertainty_breakdown.png` - Uncertainty component visualization
- `regional_comparison.png` - Regional benefit comparison

### Reports
- `analysis_summary.pdf` - Technical summary of methods and results
- `validation_report.pdf` - Detailed validation documentation

## Dependencies

### Core Dependencies
- Python 3.8+
- GeoPandas >= 0.12.0
- NumPy >= 1.21.0
- Pandas >= 1.3.0
- Matplotlib >= 3.4.0
- Contextily >= 1.2.0

### Optional Dependencies
- Jupyter Lab (for running notebooks)
- Seaborn (enhanced visualizations)
- SciPy (additional statistical functions)

## Contributing

This is primarily a personal analysis project, but suggestions and improvements are welcome:

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Submit a pull request

Please ensure any changes maintain the reproducibility and documentation standards of the project.

## Limitations

- Uses synthetic data for demonstration purposes
- Does not include meteorological factors
- Assumes linear response to emissions reductions
- Seasonal variations not considered
- Economic costs of reductions not evaluated

## Future Work

Potential extensions to this analysis:
- Integration with real monitoring data
- Inclusion of meteorological variables
- Seasonal and diurnal pattern analysis
- Economic cost-benefit assessment
- Climate change scenario projections
- Higher spatial resolution modeling

## Citation

If you use this methodology or code in your work, please acknowledge the project. For formal academic use, please contact the maintainer.

## License

MIT License - see [LICENSE](LICENSE) file for details.

## Contact

For questions about the analysis or code:
- Open an issue on GitHub
- Check the documentation in the notebooks
- Review the methodology section above

## Acknowledgments

- Natural Earth for boundary data
- UK Office for National Statistics for population reference data
- Python geospatial community for open-source tools
- Environmental science researchers whose work informed the methodology
```

---

## Additional Files You Should Create

### 1. `environment.yml`
```yaml
name: uk-pm25-analysis
channels:
  - conda-forge
  - defaults
dependencies:
  - python=3.9
  - geopandas>=0.12.0
  - numpy>=1.21.0
  - pandas>=1.3.0
  - matplotlib>=3.4.0
  - contextily>=1.2.0
  - jupyterlab>=3.0.0
  - seaborn>=0.11.0
  - scipy>=1.7.0
  - shapely>=1.8.0
  - rasterio>=1.2.0
  - pip
  - pip:
    - -r requirements.txt
```

### 2. `requirements.txt`
```
geopandas>=0.12.0
numpy>=1.21.0
pandas>=1.3.0
matplotlib>=3.4.0
contextily>=1.2.0
seaborn>=0.11.0
scipy>=1.7.0
shapely>=1.8.0
rasterio>=1.2.0
jupyter>=1.0.0
```

### 3. `.gitignore`
```
# Data files
*.geojson
*.csv
*.json
*.png
*.pdf

# Python
__pycache__/
*.py[cod]
*$py.class
*.so
.Python
build/
develop-eggs/
dist/
downloads/
eggs/
.eggs/
lib/
lib64/
parts/
sdist/
var/
wheels/
*.egg-info/
.installed.cfg
*.egg

# Jupyter Notebook
.ipynb_checkpoints

# Environment
.env
.venv
env/
venv/
ENV/
env.bak/
venv.bak/

# IDE
.vscode/
.idea/
*.swp
*.swo
