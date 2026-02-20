# Company Filing Data Analysis Summary

## Overview
Analysis of 1,063,215 companies with ERISA filing data, covering years 1900-2025.

---

## Question 1: How many companies file each year?

### Key Findings:
- **Peak filing year**: 2023 with **835,088 companies**
- **Recent trend**: Massive growth starting in 2020
  - 2020: 726,676 companies
  - 2021: 764,272 companies  
  - 2022: 805,191 companies
  - 2023: 835,088 companies (peak)
  - 2024: 816,684 companies
- **Historical growth**: Steady increase from ~100 companies/year in early 2000s to thousands by 2018
- **2020 spike**: Likely due to increased reporting requirements or data collection improvements

### Insights:
The dramatic increase in 2020+ suggests either:
1. New reporting requirements (e.g., ACA, transparency rules)
2. Improved data collection methodology
3. Expansion of filing requirements to smaller plans

---

## Question 2: Size Range by Enrolled Employees

### Distribution Statistics:
- **Median**: 10 enrolled employees
- **Mean**: 43 employees (after removing outliers)
- **25th percentile**: 4 employees
- **75th percentile**: 30 employees
- **95th percentile**: 184 employees
- **99th percentile**: 633 employees

### ERISA/ACA Size Thresholds:
- **Small (< 50 employees)**: 812,954 companies (**83.0%**)
- **Mid (50-99 employees)**: 73,494 companies (7.5%)
- **Large (100-499 employees)**: 78,569 companies (8.0%)
- **Very Large (500+ employees)**: 14,320 companies (1.5%)

### Suggested Size Bins (Natural Breakpoints):
| Size Range | Count | Percentage |
|-----------|-------|------------|
| 1-10 employees | 539,969 | 55.1% |
| 11-25 employees | 230,742 | 23.6% |
| 26-50 employees | 116,235 | 11.9% |
| 51-100 employees | 73,494 | 7.5% |
| 101-250 employees | 57,856 | 5.9% |
| 251-500 employees | 20,713 | 2.1% |
| 501-1000 employees | 11,112 | 1.1% |
| 1000+ employees | 13,094 | 1.3% |

### Insights:
- **Highly skewed distribution**: Over half of companies have ≤10 enrolled employees
- **Small business focus**: 83% are under ACA small group threshold (<50)
- **Natural breakpoints**: Clear clustering around 10, 25, 50, 100 employee marks
- **Long tail**: Very few companies exceed 500 employees, but they represent significant benefits spending

---

## Question 3: Primary Industry and NAICS Code Analysis

### Top Industries by NAICS Code:
1. **621111** - Offices of Physicians (except Mental Health Specialists): **56,337 companies**
2. **541990** - Other Professional Services: 54,338 companies
3. **621210** - Offices of Dentists: **48,246 companies**
4. **541110** - Offices of Lawyers: 43,013 companies
5. **812990** - Other Personal Services: 32,119 companies

### Industry Sector Distribution (from dim_company):
- Health Care and Social Assistance (dominant)
- Finance and Insurance
- Professional, Scientific, and Technical Services
- Retail Trade
- Information
- Accommodation and Food Services
- Transportation and Warehousing

### NAICS Code Structure:
NAICS codes are hierarchical:
- **2-digit**: Sector (e.g., 62 = Health Care)
- **3-digit**: Subsector
- **4-digit**: Industry Group  
- **5-digit**: Industry
- **6-digit**: National Industry

### Recommendations for Multi-NAICS Analysis:
To analyze companies filing under multiple NAICS codes, you would need to:
1. **Load fact_filing.csv** (2.5GB) - contains filing-level data with potentially multiple NAICS codes per company
2. **Group by EIN** and analyze NAICS code combinations
3. **Look for patterns**: Companies typically file under related codes (same sector/subsector)
4. **Research NAICS co-occurrence**: Industry research shows common patterns (e.g., construction companies often have both construction and real estate codes)

### Web Research Note:
The Census Bureau and NAICS documentation provides information on:
- Common industry combinations
- Multi-establishment reporting patterns
- Industry classification guidelines

---

## Question 4: Benefits Programs Structure by Size/Industry

### Overall Benefits Metrics:
| Metric | Companies with Data | Mean | Median | Total |
|--------|-------------------|------|--------|-------|
| Total Benefits Paid | 583,340 | $355,836 | $51,850 | $207.6B |
| Total Assets (EOY) | 765,031 | $1,538,989 | $515,913 | $1,177.4B |
| Total Expenses | 802,312 | $265,906 | $21,972 | $213.3B |
| Employer Contributions | 660,835 | $61,930 | $24,718 | $40.9B |
| Latest Year Premiums | 78,239 | $145M | $1.08M | $11.3T |

### Benefits by Size Bin:

#### Total Benefits Paid:
- **1-10 employees**: Mean $158,595, Median $0 (many have no benefits)
- **11-25 employees**: Mean $187,206, Median $10,416
- **26-50 employees**: Mean $311,519, Median $46,457
- **51-100 employees**: Mean $428,417, Median $95,178
- **101-250 employees**: Mean $155,778 (many zeros)
- **251-500 employees**: Mean $58,263 (many zeros)

#### Premiums by Size:
- **1-10 employees**: Mean $8,522, Median $0
- **51-100 employees**: Mean $49,162, Median $0
- **101-250 employees**: Mean $720,382, Median $155,140
- **251-500 employees**: Mean $537.5M (likely data quality issue - check outliers)
- **500+ employees**: Mean $1M-$10M range

### Insights:
- **Scale effects**: Benefits spending increases non-linearly with size
- **Small company pattern**: Many small companies (1-10 employees) report $0 benefits, suggesting:
  - Pension-only plans (no welfare benefits)
  - Missing data
  - Self-insured arrangements not captured
- **Mid-size sweet spot**: Companies with 26-100 employees show consistent benefits programs
- **Large company complexity**: Very large companies (>500) have highly variable benefits structures

---

## Question 5: Most Prominent Brokers and Carriers

### Top 20 Brokers (by company count):
1. **USI INSURANCE SERVICES LLC**: 1,564 companies
2. **GALLAGHER BENEFIT SERVICES, INC.**: 1,299 companies
3. **LOCKTON COMPANIES, LLC**: 1,165 companies
4. **MARSH & MCLENNAN AGENCY LLC**: 954 companies
5. **ALLIANT INSURANCE SERVICES, INC.**: 402 companies
6. **EDGEWOOD PARTNERS INSURANCE CENTER**: 246 companies
7. **SEQUOIA BENEFITS & INS SVCS LLC**: 228 companies
8. **GALLAGHER BENEFIT SERVICES INC**: 218 companies (note: likely same as #2)
9. **HUB INTERNATIONAL MIDWEST LIMITED**: 184 companies
10. **DIGITAL INSURANCE LLC**: 160 companies

**Total**: 76,860 broker mentions across 54,414 unique brokers

### Top 20 Carriers (by company count):
1. **PRINCIPAL LIFE INSURANCE COMPANY**: 546 companies
2. **THE GUARDIAN LIFE INSURANCE COMPANY OF AMERICA**: 522 companies
3. **UNITEDHEALTHCARE INSURANCE COMPANY**: 446 companies
4. **UNITED OF OMAHA LIFE INSURANCE COMPANY**: 443 companies
5. **METROPOLITAN LIFE INSURANCE COMPANY**: 386 companies
6. **SUN LIFE ASSURANCE COMPANY OF CANADA**: 242 companies
7. **THE LINCOLN NATIONAL LIFE INSURANCE COMPANY**: 229 companies
8. **UNUM LIFE INSURANCE COMPANY OF AMERICA**: 209 companies
9. **NATIONAL FRANCHISE ASSOCIATION HEALTH PLUS-CELL**: 161 companies
10. **AULTCARE INSURANCE COMPANY**: 150 companies

**Total**: 79,142 carrier mentions across 66,836 unique carriers

### Service Codes (Products) from fact_provider:
Top service codes by frequency:
- **60.0**: 44,767 records
- **64.0**: 42,159 records
- **50.0**: 37,980 records
- **99.0**: 35,844 records
- **13.0**: 19,930 records

*Note: Service codes need mapping to actual product names (e.g., health insurance, dental, vision, disability, etc.)*

### Insights:
- **Broker concentration**: Top 3 brokers serve ~4,000 companies combined
- **Carrier diversity**: More carriers (66K) than brokers (54K), suggesting:
  - Companies use multiple carriers
  - Carrier specialization by product type
- **Name standardization needed**: Some duplicates (e.g., "GALLAGHER BENEFIT SERVICES, INC." vs "GALLAGHER BENEFIT SERVICES INC")
- **Product analysis opportunity**: Service codes can reveal product portfolios when mapped

---

## Recommendations for Further Analysis

### 1. **Multi-NAICS Code Analysis**
- Load full `fact_filing.csv` to analyze companies filing under multiple codes
- Create co-occurrence matrix of NAICS codes
- Research industry patterns (construction + real estate, healthcare + professional services, etc.)

### 2. **Visualizations**
- **Time series**: Companies filing by year (line chart)
- **Size distribution**: Histogram of enrolled employees (log scale)
- **Industry breakdown**: Bar chart of top NAICS codes
- **Broker/Carrier market share**: Pie charts or treemaps
- **Benefits by size**: Scatter plots with size bins

### 3. **Broker/Carrier Relationships**
- Analyze which brokers work with which carriers
- Product portfolios by broker
- Geographic patterns (state-level analysis)
- Market concentration metrics (HHI index)

### 4. **Geographic Analysis**
- State-level filing patterns
- Regional broker/carrier preferences
- Benefits spending by state

### 5. **Data Quality Improvements**
- Standardize broker/carrier names (fuzzy matching)
- Map service codes to product names
- Handle missing NAICS codes (many show as "Unknown")
- Investigate premium outliers (some values seem incorrect)

### 6. **Advanced Analytics**
- Time series forecasting of filing trends
- Clustering companies by benefits profile
- Predictive modeling of benefits spending
- Network analysis of broker-carrier relationships

---

## Data Quality Notes

1. **Missing NAICS mappings**: Many companies show "Unknown" for industry name - need to enrich from external sources
2. **Name standardization**: Broker/carrier names need deduplication (e.g., "GALLAGHER BENEFIT SERVICES, INC." vs "GALLAGHER BENEFIT SERVICES INC")
3. **Outlier detection**: Some premium values appear incorrect (e.g., $537M average for 251-500 employee companies)
4. **Service code mapping**: Need to map numeric service codes to product names
5. **Year parsing**: Successfully handled numpy array format in `years_with_filings` column

---

## Files Generated

- `analyze_data.py`: Main analysis script
- `analysis_output.txt`: Full text output of analysis
- `ANALYSIS_SUMMARY.md`: This summary document

---

*Analysis completed: February 20, 2026*
