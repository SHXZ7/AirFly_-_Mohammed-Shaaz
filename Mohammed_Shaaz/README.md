# Flight Delay Analysis Project 🛫

## Project Overview
This project analyzes flight delay patterns across multiple datasets spanning from 2008 to 2024, providing insights into delay causes, trends, and patterns across different time periods and airlines.

---

## 📋 Week 1 Report – Project Initialization and Dataset Setup

**Report Date:** October 18, 2025  
**Status:** ✅ Completed

### 🎯 Week 1 Goals
- Build a unified understanding of flight delay datasets (2008 → 2024)
- Prepare optimized, memory-efficient DataFrames for analysis
- Quantify nulls, types, and structure consistency before cleaning
- Establish baseline metrics for data quality assessment

---

### 📊 Dataset Overview

#### Dataset 1: DelayedFlights (2008)
**File:** `dataset/DelayedFlights.csv`

| Metric | Value |
|--------|-------|
| **Total Records** | 1,936,758 rows |
| **Total Columns** | 30 columns |
| **Memory Usage** | 923.51 MB (raw) → 692.63 MB (optimized) |
| **Time Period** | 2008 |

**Column Type Distribution:**
- Float64: 14 columns
- Int64: 11 columns
- Object: 5 columns

**Top Missing Values:**
- NASDelay: 689,270 (35.6%)
- CarrierDelay: 689,270 (35.6%)
- LateAircraftDelay: 689,270 (35.6%)
- SecurityDelay: 689,270 (35.6%)
- WeatherDelay: 689,270 (35.6%)
- ActualElapsedTime: 8,387 (0.4%)
- AirTime: 8,387 (0.4%)
- ArrDelay: 8,387 (0.4%)
- TaxiIn: 7,110 (0.4%)
- ArrTime: 7,110 (0.4%)

**Key Observations:**
- Delay reason columns (CarrierDelay, WeatherDelay, NASDelay, SecurityDelay, LateAircraftDelay) have consistent 35.6% missing values - likely representing flights without delays
- Other missing values are minimal (<0.5%)
- Dataset represents comprehensive 2008 flight data

---

#### Dataset 2: flight_delays (2019–2023)
**File:** `dataset/flight_delays.csv`

| Metric | Value |
|--------|-------|
| **Total Records** | 1,747,627 rows |
| **Total Columns** | 16 columns |
| **Memory Usage** | 1,169.84 MB (raw) → 1,131.51 MB (optimized) |
| **Time Period** | 2019–2023 |

**Column Type Distribution:**
- Object: 10 columns
- Int64: 4 columns
- Bool: 2 columns

**Top Missing Values:**
- DelayReason: 468,873 (26.8%)
- All other columns: 0 missing values

**Key Observations:**
- More recent dataset with different schema structure
- 26.8% of flights have no delay reason recorded
- Contains boolean fields for Cancelled and Diverted status
- Includes aircraft identification (TailNumber, AircraftType)
- More text-heavy data structure (more object columns)

---

#### Dataset 3: flights_sample_3m (2024)
**File:** `dataset/flights_sample_3m.csv`

| Metric | Value |
|--------|-------|
| **Total Records** | 3,000,000 rows |
| **Total Columns** | 32 columns |
| **Memory Usage** | 2,174.67 MB (raw) → 1,888.57 MB (optimized) |
| **Time Period** | 2019–2024 (sample) |

**Column Type Distribution:**
- Float64: 19 columns
- Object: 9 columns
- Int64: 4 columns

**Top Missing Values:**
- CANCELLATION_CODE: 2,920,860 (97.4%)
- DELAY_DUE_LATE_AIRCRAFT: 2,466,137 (82.2%)
- DELAY_DUE_CARRIER: 2,466,137 (82.2%)
- DELAY_DUE_SECURITY: 2,466,137 (82.2%)
- DELAY_DUE_NAS: 2,466,137 (82.2%)
- DELAY_DUE_WEATHER: 2,466,137 (82.2%)
- ARR_DELAY: 86,198 (2.9%)
- ELAPSED_TIME: 86,198 (2.9%)
- AIR_TIME: 86,198 (2.9%)
- WHEELS_ON: 79,944 (2.7%)

**Key Observations:**
- Largest dataset with 3 million records
- Most comprehensive column set (32 columns)
- High percentage of cancellation codes missing (97.4%) - most flights not cancelled
- 82.2% missing delay reason data - representing on-time flights
- Most granular data with detailed timing information
- Contains geographic city information alongside airport codes

---

### 📈 KPI Summary

#### 1. Missing Values Analysis
| Dataset | Critical Missing % | Total Completeness |
|---------|-------------------|-------------------|
| DelayedFlights (2008) | 35.6% (delay reasons) | ~64% |
| flight_delays (2019-23) | 26.8% (delay reasons) | ~73% |
| flights_sample_3m (2024) | 82.2% (delay reasons) | ~18% |

**Insight:** Missing delay reason data is expected and represents on-time flights. This will require careful handling in analysis.

#### 2. Memory Optimization Results
| Dataset | Before | After | Reduction |
|---------|--------|-------|-----------|
| DelayedFlights (2008) | 923.51 MB | 692.63 MB | 0.0%* |
| flight_delays (2019-23) | 1,169.84 MB | 1,131.51 MB | 0.0%* |
| flights_sample_3m (2024) | 2,174.67 MB | 1,888.57 MB | 0.0%* |

*Note: Memory optimization was applied via dtype downcasting, but actual memory savings were minimal due to the presence of object/string columns which cannot be optimized this way.

#### 3. Sampling Strategy
| Dataset | Original Rows | Sample Size | Retention % |
|---------|---------------|-------------|-------------|
| DelayedFlights (2008) | 1,936,758 | 10,000 | 0.52% |
| flight_delays (2019-23) | 1,747,627 | 10,000 | 0.57% |
| flights_sample_3m (2024) | 3,000,000 | 1,000 | 0.03% |

**Purpose:** These samples enable rapid prototyping and exploration before applying transformations to full datasets.

#### 4. Schema Alignment Status
| Feature | 2008 Dataset | 2019-23 Dataset | 2024 Dataset |
|---------|-------------|----------------|--------------|
| Delay Information | ✅ | ✅ | ✅ |
| Airport Codes | ✅ | ✅ | ✅ |
| Date/Time | ✅ | ✅ | ✅ |
| Carrier Info | ✅ | ✅ | ✅ |
| Cancellation | ✅ | ✅ | ✅ |
| Aircraft Info | ❌ | ✅ | ❌ |
| City Names | ❌ | ❌ | ✅ |

---

### 🔍 Key Findings

1. **Data Volume**: Total of ~6.7M flight records across all datasets
2. **Temporal Coverage**: 16-year span (2008, 2019-2024)
3. **Schema Heterogeneity**: Each dataset has different column structures requiring harmonization
4. **Data Quality**: 
   - Consistent missing patterns in delay-related columns (expected behavior)
   - Minimal missing values in core flight information
   - High data completeness for operational metrics

5. **Memory Footprint**: Total raw data size ~4.3 GB
   - Optimization strategies needed for full dataset analysis
   - Consider chunked processing or Polars/Dask for large-scale operations

---

### ⚠️ Challenges Identified

1. **Schema Inconsistency**
   - Different column names across datasets
   - Different representations of similar data
   - Requires mapping/standardization layer

2. **Missing Data Patterns**
   - Delay reasons missing for on-time flights
   - Need to establish clear imputation strategy vs. filtering strategy

3. **Memory Management**
   - Large combined dataset size
   - Limited success with basic dtype optimization
   - May require alternative approaches (Parquet format, chunked processing)

4. **Data Integration**
   - Merging datasets requires careful feature engineering
   - Time period gaps between datasets
   - Different granularity levels

---

### ✅ Deliverables Completed

- [x] All 3 datasets successfully loaded
- [x] Initial data profiling completed
- [x] Missing value analysis documented
- [x] Memory usage baseline established
- [x] Sample datasets created for rapid testing
- [x] Data type optimization attempted
- [x] Schema comparison completed

---

## � Week 2 Report – Preprocessing and Feature Engineering

**Report Date:** October 25, 2025  
**Status:** ✅ Completed

### 🎯 Week 2 Goals
- Handle nulls in delay and cancellation columns
- Create derived features: Month, Day of Week, Hour, Route
- Format datetime columns properly
- Optimize memory usage through type conversions
- Save preprocessed data for fast reuse

---

### 🔧 Preprocessing Steps Completed

#### 1. **Column Standardization**
- Normalized all column names to lowercase with underscores
- Created consistent naming convention across dataset

#### 2. **Missing Value Handling**
✅ **Delay Reason Columns** (CarrierDelay, WeatherDelay, NASDelay, SecurityDelay, LateAircraftDelay)
- Filled NaN values with 0 (representing on-time flights)
- 100% completeness achieved

✅ **Cancellation Codes**
- Filled missing values with 'NONE' for non-cancelled flights

✅ **Small Missing Numeric Fields**
- Applied median imputation for columns with <5% missing values
- Affected fields: ActualElapsedTime, AirTime, ArrDelay, DepTime, ArrTime, TaxiIn, TaxiOut

#### 3. **Datetime Engineering**
✅ **Date Construction**
- Created `fl_date` from Year, Month, DayofMonth columns
- Parsed to proper datetime format

✅ **Time Conversion**
- Converted HHMM format (e.g., 930) to time strings (09:30)
- Created `dep_time_str` and `arr_time_str` from numeric time fields

✅ **Datetime Combination**
- Generated `dep_datetime` and `arr_datetime` by combining date and time
- Handled midnight crossings (flights landing after midnight)

#### 4. **Feature Engineering**

**Temporal Features:**
- `month` - Month number (Int8)
- `day_of_week` - Day name (Monday, Tuesday, etc.)
- `dep_hour` - Departure hour (Int8)

**Route Features:**
- `route` - Origin-Destination pair (e.g., "ORD-LAX")

**Delay Indicators:**
- `is_delayed` - Binary flag (1 if arrival delay > 15 min)
- `any_delay_reason` - Binary flag (1 if any delay cause present)
- `total_delay_minutes` - Sum of all delay types
- `dep_delayed` - Binary flag (1 if departure delay > 15 min)

**Duration Features:**
- `scheduled_duration_min` - Flight duration from datetimes
- `actual_duration_min` - Actual elapsed time

#### 5. **Memory Optimization**

**Type Conversions Applied:**
- ✅ Categorical encoding for low-cardinality strings:
  - `uniquecarrier`, `origin`, `dest`, `cancellation_code`, `route`, `day_of_week`
- ✅ Numeric downcasting:
  - Int64 → signed integer (int8/int16/int32)
  - Float64 → float32

**Memory Results:**
- Before optimization: ~923 MB
- After optimization: Significant reduction through categorical encoding
- Space savings primarily from string → category conversion

#### 6. **Validation Checks**
✅ All assertions passed:
- No NaN values in delay reason columns
- Cancellation codes properly filled
- Data integrity maintained

#### 7. **Data Export**
✅ Saved files in Parquet format (compressed and fast):
- `delayedflights_2008_processed.parquet` - Full processed dataset
- `sample_10k.parquet` - 10,000-row sample for rapid prototyping

---

### 📊 Week 2 Key Metrics

| Metric | Value |
|--------|-------|
| **New Features Created** | 11 features |
| **Missing Values Resolved** | 100% for critical columns |
| **Memory Optimization** | Categorical + downcasting applied |
| **Data Completeness** | >95% overall |
| **Processed Files Saved** | 2 (full + sample) |

---

### 🎯 Features Created Summary

| Feature Name | Type | Description |
|--------------|------|-------------|
| `fl_date` | datetime64 | Flight date |
| `dep_datetime` | datetime64 | Full departure timestamp |
| `arr_datetime` | datetime64 | Full arrival timestamp |
| `month` | Int8 | Month number (1-12) |
| `day_of_week` | category | Day name |
| `dep_hour` | Int8 | Departure hour (0-23) |
| `route` | category | Origin-Destination pair |
| `is_delayed` | int8 | Delay flag (>15 min) |
| `any_delay_reason` | int8 | Has delay reason flag |
| `total_delay_minutes` | float | Sum of all delays |
| `dep_delayed` | int8 | Departure delay flag |
| `scheduled_duration_min` | float | Planned flight time |
| `actual_duration_min` | float | Actual flight time |

---

### ✅ Week 2 Deliverables

- [x] Cleaned dataset with no critical missing values
- [x] 13+ engineered features for analysis
- [x] Datetime columns properly formatted
- [x] Memory-optimized datatypes
- [x] Preprocessed data saved in Parquet format
- [x] Sample dataset for quick testing
- [x] Data validation passed
- [x] Feature dictionary documented

---

### 📅 Next Steps (Week 3 Preview)

1. **Exploratory Data Analysis (EDA)**
   - Delay distribution analysis by carrier, route, time
   - Identify peak delay periods
   - Correlation analysis between features
   - Visualize temporal patterns

2. **Statistical Analysis**
   - Hypothesis testing for delay causes
   - Compare carrier performance
   - Seasonal trend analysis
   - Route-specific insights

3. **Data Integration**
   - Apply same preprocessing to 2019-2023 dataset
   - Apply same preprocessing to 2024 sample dataset
   - Merge datasets with standardized schema
   - Create unified multi-year dataset

4. **Advanced Feature Engineering**
   - Create lag features for time series
   - Engineer weather-related proxies
   - Create airport congestion metrics
   - Holiday/special event indicators

---

### 📂 Project Structure

```
infosys/
├── dataprpocessing.ipynb         # Week 1: Initial exploration
├── data_pro.ipynb                # Week 2: Preprocessing & feature engineering
├── dataset/
│   ├── DelayedFlights.csv        # 2008 data (1.9M rows)
│   ├── flight_delays.csv         # 2019-23 data (1.7M rows)
│   └── flights_sample_3m.csv     # 2024 sample (3M rows)
├── processed/
│   ├── delayedflights_2008_processed.parquet  # Cleaned & engineered
│   └── sample_10k.parquet                      # Quick testing sample
└── README.md                      # Project documentation
```

---

### 🛠️ Technologies Used

- **Python 3.11.13**
- **pandas 2.3.1** - Data manipulation and analysis
- **numpy 2.2.6** - Numerical computing
- **Jupyter Notebook** - Interactive development environment

---

### 👥 Contributors

Project developed as part of Infosys data analytics initiative.

---

### 📝 Notes

- All memory measurements taken on Windows system
- Optimization strategies may need revision for production deployment
- Dataset timeframes have gaps that should be considered in temporal analysis
- Further investigation needed for optimal data storage format

---

**Last Updated:** October 25, 2025  
**Current Week:** Week 2 - Preprocessing & Feature Engineering ✅ Complete
