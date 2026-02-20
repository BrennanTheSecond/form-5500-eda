# Raw Data Analysis Results

**Analysis Date**: February 20, 2026  
**Data Source**: Raw EFAST2 files (Form 5500, 5500-SF, Schedule A)  
**Years Analyzed**: 2020-2024

---

## ✅ Both Scripts Completed Successfully

- **Full Analysis** (`analyze_raw_data.py`): Completed in ~11 minutes
- **Chunked Analysis** (`analyze_raw_data_chunked.py`): Completed in ~19 minutes

Both scripts produced **identical results** for overlapping analyses, confirming data consistency.

---

## 📊 Key Findings

### 1. Companies Filing Each Year

| Year | Form 5500 Filings | Form 5500 Unique EINs | Form 5500-SF Filings | Form 5500-SF Unique EINs |
|------|-------------------|----------------------|---------------------|-------------------------|
| 2020 | 249,623 | 156,805 | 640,689 | 581,030 |
| 2021 | 244,211 | 155,304 | 667,978 | 608,935 |
| 2022 | 243,804 | 155,289 | 713,643 | 651,282 |
| 2023 | 230,009 | 146,403 | 759,569 | 692,182 |
| 2024 | 187,191 | 126,620 | 738,685 | 686,924 |

**Total Unique EINs (all years combined)**: **1,063,215**

**Key Insights**:
- Form 5500-SF (short form) has **3x more filings** than Form 5500 (full form)
- Peak filing year: **2023** (759,569 SF filings)
- 2024 shows decline in Form 5500 filings (likely due to incomplete data collection)
- Most companies file using the short form (5500-SF), indicating small plans dominate

---

### 2. Size Range (Participants - Beginning of Year)

**Statistics**:
- **Total observations**: 4,497,371 filings
- **Mean**: 103 participants
- **Median**: 16 participants
- **25th percentile**: 6 participants
- **75th percentile**: 59 participants
- **99th percentile**: ~4,051 participants (after removing outliers)

**Size Distribution**:
| Size Range | Count | Percentage |
|------------|-------|------------|
| 1-10 participants | 1,638,228 | 36.4% |
| 11-25 participants | 1,036,736 | 23.1% |
| 26-50 participants | 578,697 | 12.9% |
| 51-100 participants | 411,699 | 9.2% |
| 101-250 participants | 447,560 | 10.0% |
| 251-500 participants | 184,315 | 4.1% |
| 501-1000 participants | 103,884 | 2.3% |
| 1000+ participants | 96,252 | 2.1% |

**Key Insights**:
- **59.5%** of plans have ≤25 participants (very small plans)
- **85.6%** of plans have ≤100 participants
- Highly skewed distribution toward small plans
- Median (16) is much lower than mean (103), indicating long tail of large plans

---

### 3. Primary Industry (NAICS / Business Code)

**Total Unique NAICS Codes**: 1,221

**Top 20 NAICS Codes**:
| Code | Count | Industry Name |
|------|-------|---------------|
| 621111 | 273,494 | Offices of Physicians (except Mental Health Specialists) |
| 621210 | 212,600 | Offices of Dentists |
| 541990 | 210,167 | Other Professional Services |
| 541110 | 198,781 | Offices of Lawyers |
| 541600 | 106,186 | Management Consulting Services |
| 812990 | 98,046 | Other Personal Services |
| 611000 | 87,141 | Educational Services |
| 238900 | 87,095 | Other Specialty Trade Contractors |
| 813000 | 85,878 | Religious Organizations |
| 523900 | 84,691 | Other Financial Investment Activities |
| 524210 | 68,072 | Insurance Agencies and Brokerages |
| 541330 | 64,586 | Engineering Services |
| 238220 | 61,087 | Plumbing, Heating, and Air-Conditioning Contractors |
| 236110 | 54,843 | Residential Building Construction |
| 541211 | 52,824 | Offices of Certified Public Accountants |
| 236200 | 49,870 | Nonresidential Building Construction |
| 541519 | 45,103 | Other Computer Related Services |
| 238210 | 44,465 | Electrical Contractors |
| 541511 | 44,359 | Custom Computer Programming Services |
| 339900 | 43,973 | Other Miscellaneous Manufacturing |

**Multi-NAICS Companies**: **76,500 EINs** file under multiple NAICS codes

**Key Insights**:
- **Healthcare dominates**: Top 2 codes are physicians (273K) and dentists (213K)
- **Professional services** heavily represented (lawyers, accountants, consultants)
- **Construction** well-represented (multiple codes in top 20)
- **7.2%** of companies operate in multiple industries (76,500 / 1,063,215)

---

### 4. Benefits / Financials (5500-SF Only)

**All Years (2020-2024)**:
| Metric | Count | Mean | Median |
|--------|-------|------|--------|
| Total Assets EOY | 3,328,616 | $1,539,629 | $603,846 |
| Total Expenses | 3,021,655 | $173,773 | $17,592 |
| Employer Contributions | 2,776,369 | $66,911 | $28,599 |
| Total Benefits Paid | 2,093,856 | $240,839 | $42,069 |

**2024 Only (Sample)**:
| Metric | Count | Mean | Median |
|--------|-------|------|--------|
| Total Assets EOY | 700,408 | $1,570,943 | $573,734 |
| Total Expenses | 640,648 | $184,563 | $16,581 |
| Employer Contributions | 578,705 | $66,676 | $27,783 |
| Total Benefits Paid | 441,321 | $257,166 | $42,204 |

**Key Insights**:
- Median assets (~$600K) much lower than mean (~$1.5M), indicating large plans skew average
- Most plans have modest expenses (median $17K-$18K)
- Employer contributions show consistent pattern across years
- Benefits paid highly variable (median $42K vs mean $240K-$257K)

---

### 5. Brokers and Carriers (Schedule A)

#### Top 15 Carriers (All Years 2020-2024)

| Rank | Carrier Name | Mentions |
|------|--------------|----------|
| 1 | UNITED OF OMAHA LIFE INSURANCE COMPANY | 77,220 |
| 2 | LIFE INSURANCE COMPANY OF NORTH AMERICA | 69,219 |
| 3 | METROPOLITAN LIFE INSURANCE COMPANY | 67,545 |
| 4 | PRINCIPAL LIFE INSURANCE COMPANY | 56,510 |
| 5 | UNUM LIFE INSURANCE COMPANY OF AMERICA | 55,275 |
| 6 | THE LINCOLN NATIONAL LIFE INSURANCE COMPANY | 54,285 |
| 7 | VISION SERVICE PLAN | 51,335 |
| 8 | UNITEDHEALTHCARE INSURANCE COMPANY | 35,536 |
| 9 | THE GUARDIAN LIFE INSURANCE COMPANY OF AMERICA | 34,688 |
| 10 | STANDARD INSURANCE COMPANY | 33,283 |
| 11 | RELIANCE STANDARD LIFE INSURANCE COMPANY | 30,844 |
| 12 | CIGNA HEALTH AND LIFE INSURANCE COMPANY | 29,367 |
| 13 | HARTFORD LIFE AND ACCIDENT | 25,653 |
| 14 | SUN LIFE ASSURANCE COMPANY OF CANADA | 21,966 |
| 15 | LINCOLN NATIONAL LIFE INSURANCE COMPANY | 17,074 |

**Total**: 1,607,839 carrier mentions across 19,870 unique carriers

#### Top 15 Brokers (All Years 2020-2024)

| Rank | Broker Name | Mentions |
|------|-------------|----------|
| 1 | USI INSURANCE SERVICES LLC | 44,126 |
| 2 | MARSH & MCLENNAN AGENCY LLC | 41,610 |
| 3 | LOCKTON COMPANIES, LLC | 36,996 |
| 4 | GALLAGHER BENEFIT SERVICES, INC. | 35,225 |
| 5 | MERCER HEALTH AND BENEFITS, LLC | 20,540 |
| 6 | WILLIS TOWERS WATSON US LLC | 16,049 |
| 7 | ALLIANT INSURANCE SERVICES, INC. | 14,616 |
| 8 | MERCER HEALTH & BENEFITS LLC | 14,491 |
| 9 | GALLAGHER BENEFIT SERVICES INC | 11,435 |
| 10 | EDGEWOOD PARTNERS INSURANCE CENTER | 10,297 |
| 11 | HUB INTERNATIONAL MIDWEST LIMITED | 8,221 |
| 12 | AON CONSULTING INC | 7,839 |
| 13 | DIGITAL INSURANCE LLC | 7,527 |
| 14 | IMG | 7,110 |
| 15 | LOCKTON COMPANIES LLC | 6,752 |

**Total**: 1,421,211 broker mentions across 52,655 unique brokers

**2024 Only (for comparison)**:
- Top carrier: UNITED OF OMAHA (13,003 mentions)
- Top broker: MARSH & MCLENNAN AGENCY LLC (7,895 mentions)

**Key Insights**:
- **Top 3 brokers** account for ~122K mentions (8.6% of total)
- **Top 3 carriers** account for ~214K mentions (13.3% of total)
- Broker market more fragmented (52K unique) than carrier market (20K unique)
- Some name variations exist (e.g., "GALLAGHER BENEFIT SERVICES, INC." vs "GALLAGHER BENEFIT SERVICES INC")

---

## 🔍 Comparison: Raw Data vs Preprocessed Data

### Companies Filing Each Year
- **Raw**: 1,063,215 unique EINs (matches preprocessed exactly!)
- **Preprocessed**: 1,063,215 unique EINs
- ✅ **Match**: Confirms ETL correctly captured all companies

### Size Distribution
- **Raw**: Median 16 participants, Mean 103 participants
- **Preprocessed**: Median 10 "benefits_eligible", Mean 43 "benefits_eligible"
- ⚠️ **Difference**: Raw uses "participants BOY" (broader), preprocessed uses "benefits_eligible" (narrower)
- **Note**: Participants includes all plan participants; benefits_eligible is subset enrolled in benefits

### NAICS Codes
- **Raw**: Top code 621111 (Physicians) with 273,494 filings
- **Preprocessed**: Top code 621111 with 56,337 companies
- ⚠️ **Difference**: Raw counts **filings** (one company can file multiple times), preprocessed counts **companies** (one per EIN)
- **Multi-NAICS**: Raw shows 76,500 EINs with multiple codes (matches preprocessed analysis)

### Brokers/Carriers
- **Raw**: Top broker USI (44,126 mentions), Top carrier United of Omaha (77,220 mentions)
- **Preprocessed**: Top broker USI (1,564 companies), Top carrier Principal (546 companies)
- ⚠️ **Difference**: Raw counts **mentions** (one company can have multiple broker/carrier relationships), preprocessed counts **companies** (one per EIN)
- **Note**: Raw data shows true relationship frequency; preprocessed shows company-level presence

---

## 📝 Recommendations

1. **Use raw data for**:
   - Filing-level analysis (multiple filings per company)
   - Relationship frequency (broker/carrier mentions)
   - Year-over-year trends at filing level

2. **Use preprocessed data for**:
   - Company-level aggregations
   - Unique company counts
   - Company-level attributes (one row per EIN)

3. **Data Quality Notes**:
   - Raw data confirms preprocessed ETL captured all companies correctly
   - Differences in counts are expected (filings vs companies, participants vs benefits_eligible)
   - Both datasets are consistent and valid for their intended purposes

---

## 📁 Output Files

- `raw_analysis_summary.txt` - Brief summary (from full script)
- Terminal outputs saved in `.cursor/projects/.../terminals/` folder

---

*Analysis completed successfully using raw EFAST2 data files.*
