# Form 5500 Benefits Insurance Analysis

![Python](https://img.shields.io/badge/python-3.10+-blue.svg)
![License](https://img.shields.io/badge/license-MIT-green.svg)
![Status](https://img.shields.io/badge/status-EDA-orange.svg)

Exploratory Data Analysis (EDA) of Department of Labor Form 5500 filings to support company clustering and benefits insurance scoring.

## Table of Contents

- [About This Project](#about-this-project)
- [Quick Start](#quick-start)
- [Directory Structure](#directory-structure)
- [Data Overview](#data-overview)
- [Data Dictionary](#data-dictionary)
- [Analysis Notebooks](#analysis-notebooks)
- [Usage Examples](#usage-examples)
- [Known Issues](#known-issues)
- [Contributing](#contributing)
- [License](#license)

---

## About This Project

This project analyzes Department of Labor Form 5500 filings—a required annual report for employee benefit plans in the United States. The goal is to segment companies by their benefits program characteristics for insurance product recommendations.

### What is Form 5500?

Form 5500 is an annual return/report that employers and plan sponsors must file for employee benefit plans. It provides information about:

- **Pension plans** (401k, defined benefit, etc.)
- **Welfare benefit plans** (health, life, dental, vision, disability)
- Plan financials, participants, and operations
- Insurance carriers and service providers

### Key Findings from EDA

- ~150K companies file annually (2020-2023)
- 83% of companies have fewer than 50 enrolled employees
- Top industries: Healthcare, Professional Services, Construction
- Top Brokers: USI, Gallagher, Lockton, Marsh & McLennan
- Top Carriers: Met Life, Unum, Principal, Lincoln National
- Premium per life varies significantly by industry ($309-$790)

---

## Quick Start

### Prerequisites

```bash
# Python 3.10+
python --version

# Required packages
pip install pandas numpy matplotlib seaborn jupyter
```

### Running the Analysis

```bash
# Open the notebook
jupyter notebook form_5500_eda.ipynb

# Or render the presentation
quarto render form_5500_presentation.qmd --to pptx
```

### Getting Started Checklist

- [ ] Review this README
- [ ] Read the Data Dictionary section
- [ ] Understand the Known Issues
- [ ] Run `form_5500_eda.ipynb` to reproduce EDA
- [ ] Review `DATA_DICTIONARY.md` for column details

---

## Directory Structure

```
EDA/
├── form-5500-data/
│   ├── raw/                    # Original source files from DOL
│   │   ├── form_5500/         # Main Form 5500 filings (2020-2024)
│   │   ├── form_5500_sf/      # Form 5500-SF (small plan filings)
│   │   ├── schedule_a/        # Insurance information
│   │   └── schedule_c/        # Service provider information
│   │
│   └── processed/             # Transformed/aggregated data
│       ├── dim_company.csv    # Company dimension table
│       ├── dim_naics.csv      # NAICS code lookups
│       ├── fact_filing-001.csv# Filing fact table
│       ├── fact_carrier.csv   # Carrier/insurance data
│       └── fact_provider.csv  # Service provider data
│
├── eda_output/                # Generated during EDA
│   ├── summary_statistics.csv
│   ├── company_summary.csv
│   ├── broker_carrier_products.csv
│   └── *.png                 # Visualization files
│
├── plots/                     # Presentation-ready visualizations
│   └── *.png
│
├── form_5500_eda.ipynb        # Main EDA notebook
├── form_5500_presentation.qmd # Quarto presentation source
├── form_5500_presentation.pptx # Rendered presentation
├── DATA_DICTIONARY.md         # This file
├── agents.md                  # Notes for AI agents
└── ANALYSIS_SUMMARY.md        # Analysis summary
```

---

## Data Overview

### Data Sources

| Source | Years | Records | Description |
|--------|-------|---------|-------------|
| Form 5500 | 2020-2024 | ~250K/year | Main filings |
| Form 5500-SF | 2020-2024 | ~50K/year | Small plans |
| Schedule A | 2020-2024 | Varies | Insurance info |
| Schedule C | 2020-2024 | Varies | Provider info |

### Companies Filing by Year

| Year | Companies |
|------|-----------|
| 2020 | 156,805 |
| 2021 | 155,304 |
| 2022 | 155,289 |
| 2023 | 146,403 |
| 2024 | 126,620* |

*2024 data may be incomplete due to reporting delays

### Top Industries (by NAICS Code)

| Rank | NAICS | Industry | Filings |
|------|-------|----------|---------|
| 1 | 621111 | Offices of Physicians | 32,269 |
| 2 | 621210 | Offices of Dentists | 22,643 |
| 3 | 541990 | Other Professional Services | 21,457 |
| 4 | 541110 | Offices of Lawyers | 20,926 |
| 5 | 611000 | Elementary/Secondary Schools | 10,737 |

### Top Brokers

| Rank | Broker | Filings |
|------|--------|---------|
| 1 | USI Insurance Services | 12,891 |
| 2 | Gallagher Benefit Services | 9,932 |
| 3 | Lockton Companies | 9,861 |
| 4 | Marsh & McLennan Agency | 9,492 |
| 5 | Mercer Health & Benefits | 6,033 |

### Top Carriers

| Rank | Carrier | Filings |
|------|---------|---------|
| 1 | Life Insurance Company of North America | 23,175 |
| 2 | United of Omaha Life | 21,419 |
| 3 | Lincoln National Life | 19,100 |
| 4 | Metropolitan Life | 18,841 |
| 5 | Unum Life Insurance | 18,477 |

---

## Data Dictionary

⚠️ **IMPORTANT: The processed data in `form-5500-data/processed/` is DUBIOUS AT BEST.**

See [Known Issues](#known-issues) for details.

### Raw Data (`form-5500-data/raw/`)

#### `form_5500/`
Main Form 5500 filings for large and medium-sized plans.

| Column | Type | Description |
|--------|------|-------------|
| `SPONS_DFE_EIN` | string | Employer Identification Number |
| `PLAN_NUMBER` | int | Plan number within company |
| `PLAN_YEAR_BEGIN` | date | Plan year start date |

#### `form_5500_sf/`
Form 5500-SF (Short Form) for small plans (<100 participants).

#### `schedule_a/`
Insurance information - carriers, premiums, persons covered.

#### `schedule_c/`
Service provider compensation and relationships.

---

### Processed Data (`form-5500-data/processed/`)

⚠️ **USE WITH CAUTION - SEE KNOWN ISSUES**

#### `dim_naics.csv` (47 KB)
NAICS industry code lookups.

| Column | Type | Description |
|--------|------|-------------|
| `naics_code` | int | 6-digit NAICS code |
| `industry_name` | string | Industry description |
| `subsector_name` | string | NAICS 3-digit subsector |
| `sector_name` | string | NAICS 2-digit sector |
| `sector_code` | string | 2-digit sector code |
| `sector_short_name` | string | Abbreviated sector name |

#### `dim_company.csv` (310 MB)
⚠️ Company-level data with quality issues.

| Column | Type | Description | Notes |
|--------|------|-------------|-------|
| `ein` | string | Employer ID | Primary key |
| `company_name` | string | Company name | Duplicates exist |
| `city` | string | City | Some nulls |
| `state` | string | State | Generally good |
| `business_code` | int | NAICS code | Many nulls |
| `industry_name` | string | Industry | Often "Unknown" |
| `industry_sector` | string | Sector | Often null |
| `plan_size` | string | "small"/"large"/"mixed" | Derived |
| `total_employees` | int | Total employees | Check values |
| `benefits_eligible` | int | Benefits eligible | May be inflated |
| `unique_carriers` | int | Carrier count | Verify |
| `unique_brokers` | int | Broker count | Verify |
| `has_welfare_filings` | bool | Has welfare | |
| `has_pension_filings` | bool | Has pension | |
| `total_filings_count` | int | Filing count | |
| `dq_issues` | string | DQ flags | Check this! |
| `dq_flag` | string | Quality flag | |

#### `fact_filing-001.csv` (2.5 GB)
Individual filing records.

| Column | Type | Description |
|--------|------|-------------|
| `ein` | string | Employer ID |
| `plan_number` | int | Plan identifier |
| `plan_size` | string | "small" or "large" |
| `state` | string | State code |
| `business_code` | int | NAICS code |
| `total_all_participants` | int | Total participants |
| `is_pension` | bool | Pension plan flag |
| `is_welfare` | bool | Welfare plan flag |
| `total_benefits_paid` | float | Benefits paid |
| `total_expenses` | float | Total expenses |
| `employer_contissions` | float | Employer contributions |
| `total_assets_eoy` | float | Assets at year-end |
| `is_401k_plan` | bool | 401(k) indicator |
| `year` | int | Filing year |

#### `fact_carrier.csv` (697 MB)
Insurance carrier information.

| Column | Type | Description |
|--------|------|-------------|
| `ein` | string | Employer ID |
| `carrier_name` | string | Carrier name |
| `carrier_ein` | string | Carrier EIN |
| `premium` | float | Premium amount |
| `persons_covered` | int | Persons covered |
| `broker_name` | string | Broker name |
| `broker_commission` | float | Commission paid |
| `is_health` | bool | Health |
| `is_dental` | bool | Dental |
| `is_vision` | bool | Vision |
| `is_life` | bool | Life |
| `is_std` | bool | Short-term disability |
| `is_ltd` | bool | Long-term disability |
| `claims_paid` | float | Claims paid |
| `year` | int | Policy year |

#### `fact_provider.csv` (100 MB)
Service provider information.

| Column | Type | Description |
|--------|------|-------------|
| `ein` | string | Employer ID |
| `provider_name` | string | Provider name |
| `provider_type` | string | Type |
| `service_code` | |
| `total int | Service code_compensation` | float | Compensation |
| `is_broker` | bool | Is broker |
| `year` | int | Year |

---

## Analysis Notebooks

### `form_5500_eda.ipynb`

Main EDA notebook covering:

1. **Data Loading** - Loading raw and processed data
2. **Filing Trends** - Companies filing by year (2020-2024)
3. **Size Distribution** - Employee/participant counts
4. **Industry Analysis** - NAICS codes and sectors
5. **Benefits Structure** - Welfare vs pension, premiums
6. **Brokers & Carriers** - Top providers analysis
7. **Product Offerings** - Health, dental, vision, etc.
8. **Geographic Distribution** - State-level analysis
9. **Summary Statistics** - Key metrics
10. **Clustering Recommendations** - Next steps

### `form_5500_presentation.qmd`

Quarto-based PowerPoint presentation covering key findings.

```bash
# Render to PowerPoint
quarto render form_5500_presentation.qmd --to pptx
```

---

## Usage Examples

### Example 1: Get Accurate Company Counts

```python
import pandas as pd

RAW_DATA_DIR = 'form-5500-data/raw/form_5500/'
years = [2020, 2021, 2022, 2023, 2024]

for year in years:
    df = pd.read_csv(f'{RAW_DATA_DIR}F_5500_{year}_LATEST_FULL.csv', 
                     usecols=['SPONS_DFE_EIN'])
    print(f"{year}: {df['SPONS_DFE_EIN'].nunique()} companies")
```

### Example 2: Analyze Carrier Market Share

```python
import pandas as pd

fact_carrier = pd.read_csv('form-5500-data/processed/fact_carrier.csv', nrows=500000)
top_carriers = fact_carrier['carrier_name'].value_counts().head(20)
print(top_carriers)
```

### Example 3: Size Distribution Analysis

```python
import pandas as pd

fact_filing = pd.read_csv('form-5500-data/processed/fact_filing-001.csv', nrows=500000)
print(fact_filing['total_all_participants'].describe())
```

### Example 4: Safe NAICS Sector Extraction

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

---

## Known Issues

### ⚠️ Critical Data Quality Problems

1. **Processed company counts are INFLATED**
   - Processed data shows ~1M+ companies
   - Raw data shows ~150K/year
   - **ALWAYS use raw data for accurate counts**

2. **Duplicate EINs**
   - Same company appears with conflicting information
   - Need to deduplicate before analysis

3. **Missing NAICS Codes**
   - Many companies show "Unknown" for industry
   - Need external data enrichment

4. **Name Standardization Lacking**
   - "Gallagher Benefit Services, INC." ≠ "Gallagher Benefit Services INC"
   - Fuzzy matching required for accurate broker/carrier analysis

5. **Premium Outliers**
   - Some values are clearly wrong (e.g., $537M for small company)
   - Validate against company size

6. **Date Placeholders**
   - Some dates show 1899/1900 as placeholders
   - Filter these out for time-series analysis

### Recommendations

- **For accurate counts**: Use raw data files only
- **For carrier/broker analysis**: `fact_carrier.csv` is relatively reliable
- **For industry analysis**: Verify against raw data
- **For size analysis**: Use `total_all_participants` from filings

---

## Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

### Adding New Analysis

1. Add new analysis to `form_5500_eda.ipynb`
2. Update this README with findings
3. Update `DATA_DICTIONARY.md` if new columns
4. Add visualizations to `plots/`

---

## License

MIT License - See LICENSE file for details.

---

## References

- [DOL Form 5500 Documentation](https://www.dol.gov/agencies/ebsa/about-ebsa/our-activities/public-disclosure/form-5500)
- [NAICS Code Reference](https://www.census.gov/naics/)
- [Form 5500 Instructions](https://www.irs.gov/retirement-plans/form-5500-corner)

---

## Contact

For questions or issues, please open a GitHub issue.
