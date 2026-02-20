# Form 5500 EDA - Notes for Future AI Models

## Project Overview
This project analyzes Department of Labor Form 5500 filings to support company clustering and benefits insurance scoring. The goal is to segment companies by their benefits program characteristics for insurance product recommendations.

## Data Structure

### Processed Data Files (use for detailed analysis)
| File | Rows | Description |
|------|------|-------------|
| `fact_filing-001.csv` | ~4.6M | Main filing data - plan details, participant counts, welfare/pension flags, funding info |
| `dim_company.csv` | ~1.3M | Company dimension - aggregations, industry sector, size classification |
| `dim_naics.csv` | ~374 | NAICS code lookup - maps codes to industry names and sectors |
| `fact_carrier.csv` | ~1.6M | Insurance carrier data - products, premiums, broker commissions |
| `fact_provider.csv` | ~435K | Service provider data - administrators, recordkeepers, brokers |

### Raw Data Files (use for accurate counts by year)
- `form-5500-data/raw/form_5500/F_5500_YYYY_LATEST_FULL.csv` for years 2020-2024
- Key column: `SPONS_DFE_EIN` contains the sponsor/employer EIN for unique company counting

## Key Findings from EDA

### Filing Trends (2020-2024)
- 2020: 726,676 companies
- 2021: 764,272 companies  
- 2022: 805,191 companies
- 2023: 835,088 companies (peak)
- 2024: 816,684 companies

### Company Size Distribution
- 55% have 1-10 employees (Micro)
- 24% have 11-25 employees (Small)
- 12% have 26-50 employees
- 8% have 51-100 employees
- 2% have 100+ employees

### Top Industries (NAICS)
1. 621111 - Offices of Physicians (56K companies)
2. 541990 - Other Professional Services (54K companies)
3. 621210 - Offices of Dentists (48K companies)
4. 541110 - Offices of Lawyers (43K companies)

### Top Brokers
1. USI Insurance Services (1,564 companies)
2. Gallagher Benefit Services (1,299 companies)
3. Lockton Companies (1,165 companies)

### Top Carriers
1. Principal Life Insurance (546 companies)
2. Guardian Life Insurance (522 companies)
3. UnitedHealthcare Insurance (446 companies)

## Important Code Patterns

### Safe NAICS Sector Extraction
When extracting sector codes from business_code, use this pattern to handle NaN values:
```python
def safe_extract_sector(x):
    if pd.isna(x):
        return None
    try:
        code_str = str(int(x))
        if len(code_str) >= 2:
            return code_str[:2]
    except:
        pass
    return None
```

### Reading Raw Data for Company Counts
```python
for year in [2020, 2021, 2022, 2023, 2024]:
    df = pd.read_csv(f'form-5500-data/raw/form_5500/F_5500_{year}_LATEST_FULL.csv', 
                     usecols=['SPONS_DFE_EIN'])
    unique_companies = df['SPONS_DFE_EIN'].nunique()
```

## Known Data Quality Issues

1. **Missing NAICS mappings**: Many companies show "Unknown" for industry - need external enrichment
2. **Name standardization**: Broker/carrier names need fuzzy matching deduplication (e.g., "GALLAGHER BENEFIT SERVICES, INC." vs "GALLAGHER BENEFIT SERVICES INC")
3. **Outlier detection**: Some premium values appear incorrect (e.g., $537M for mid-size companies)
4. **Date placeholders**: Some dates show 1899/1900 as placeholders for missing dates
5. **Unknown providers**: Marked as "Unknown Provider" in fact_provider

## Clustering Model Recommendations

### Recommended Algorithms (in order):
1. **K-Means** - Best for initial segmentation, interpretable
2. **Hierarchical Clustering** - Good for industry-specific groupings
3. **DBSCAN** - Best for outlier detection (unusual benefits profiles)
4. **Gaussian Mixture Models (GMM)** - For probabilistic cluster assignments (recommended for production)

### Key Features for Clustering:
- **Size**: participants, employees eligible, plan_size category
- **Industry**: NAICS sector (2-digit), subsector (3-digit), multi-sector indicator
- **Benefits**: num carriers, num brokers, product types (health/dental/vision/life/etc), welfare/pension flags
- **Geographic**: state/region

### Validation Methods:
- Silhouette score for cluster quality
- Elbow method for K-Means k selection
- Cross-validate across time periods

## Output Files

### Generated During This Project
- `form_5500_eda.ipynb` - Jupyter notebook with full EDA
- `form_5500_presentation.qmd` - Quarto source for PowerPoint
- `form_5500_presentation.pptx` - Rendered presentation (16 slides)
- `eda_output/` - Directory for generated visualizations and data exports

### For Future Work
- Company clustering scores
- Benefits insurance scoring model
- API for scoring new companies
