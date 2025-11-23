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

## � Week 3 Report – Exploratory Data Analysis (EDA)

**Report Date:** October 30, 2025  
**Status:** ✅ Completed

### 🎯 Week 3 Goals
- Perform comprehensive univariate analysis on all key variables
- Conduct bivariate analysis to understand relationships between features
- Visualize temporal patterns in flight operations and delays
- Analyze delay distributions and identify key insights
- Create enhanced correlation analysis with interpretable insights

---

### 📈 EDA Analysis Completed

#### 1. **Temporal Flight Patterns**

✅ **Monthly Flight Distribution**
- Analyzed seasonal patterns in flight volume across 12 months
- Visualization: Count plot showing flight distribution by month
- Purpose: Identify peak travel seasons and capacity planning insights

✅ **Day of Week Analysis**
- Examined flight patterns across weekdays vs. weekends
- Visualization: Count plot with ordered days (Monday-Sunday)
- Purpose: Understanding business vs. leisure travel patterns

✅ **Hourly Departure Patterns**
- Analyzed flight distribution across 24 hours of the day
- Visualization: Histogram with KDE overlay showing departure hour preferences
- Purpose: Identify peak departure times and airport congestion periods

#### 2. **Airline Performance Analysis**

✅ **Top Airlines by Flight Volume**
- Identified top 10 airlines by total flight count
- Visualization: Horizontal bar plot ranking carriers by volume
- Purpose: Market share analysis and operational scale comparison

✅ **Airline Delay Performance**
- Analyzed average delay times by carrier
- Visualization: Horizontal bar plot showing top 10 airlines by average delay
- Purpose: Carrier reliability comparison and performance benchmarking

#### 3. **Delay Pattern Analysis**

✅ **Total Delay Distribution**
- Examined overall delay distribution across all flights
- Visualization: Histogram showing delay minute distribution
- Purpose: Understanding delay severity and frequency patterns

✅ **Temporal Delay Patterns**
- **Monthly Delay Trends**: Line plot showing average delay by month
- **Hourly Delay Patterns**: Line plot showing average delay by departure hour
- **Daily Delay Patterns**: Box plot showing delay distribution by day of week
- Purpose: Identify peak delay periods and operational bottlenecks

#### 4. **Enhanced Correlation Analysis**

✅ **Comprehensive Correlation Matrix**
- Created lower-triangle correlation heatmap to avoid redundancy
- Enhanced visualization with:
  - Red-Blue diverging colormap for better interpretation
  - Proper centering at zero correlation
  - Improved annotations and styling
  - Larger figure size for better readability

✅ **Automated Correlation Insights**
- **Top 5 Strongest Positive Correlations**: Identified variables that move together
- **Top 5 Strongest Negative Correlations**: Identified inversely related variables
- **Delay-Specific Analysis**: Focused analysis on variables most correlated with total delay

✅ **Statistical Summary Export**
- Generated comprehensive statistical summary of all variables
- Exported to CSV format for external analysis and reporting

---

### 📊 Key EDA Insights Generated

#### Temporal Insights:
1. **Seasonal Patterns**: Flight volume variation across months
2. **Weekly Patterns**: Business vs. leisure travel distribution
3. **Daily Patterns**: Peak departure hours and airport utilization
4. **Delay Timing**: When delays are most likely to occur

#### Operational Insights:
1. **Carrier Performance**: Ranking airlines by reliability and volume
2. **Delay Severity**: Distribution and magnitude of delays
3. **Route Efficiency**: Understanding delay patterns by time and carrier

#### Statistical Insights:
1. **Variable Relationships**: Which factors are most strongly correlated
2. **Delay Predictors**: Key variables that correlate with delays
3. **Data Quality**: Comprehensive statistical overview of all variables

---

### 🎨 Visualization Techniques Used

| Analysis Type | Visualization | Purpose |
|---------------|---------------|---------|
| **Categorical Counts** | Count plots | Flight distribution patterns |
| **Continuous Distributions** | Histograms with KDE | Delay and time distributions |
| **Temporal Trends** | Line plots | Trends over time periods |
| **Comparative Analysis** | Horizontal bar plots | Ranking and comparison |
| **Distribution Comparison** | Box plots | Delay patterns by categories |
| **Correlation Analysis** | Enhanced heatmap | Variable relationships |

---

### 📁 EDA Deliverables

✅ **Comprehensive Visualizations**
- 9 different chart types covering all major analysis dimensions
- Professional styling with consistent color palettes
- Clear titles, labels, and legends for interpretability

✅ **Statistical Analysis**
- Enhanced correlation matrix with automated insights
- Top correlation identification (positive and negative)
- Delay-specific correlation analysis

✅ **Data Export**
- `summary/EDA_summary.csv` - Complete statistical summary
- Ready for further analysis and reporting

✅ **Documentation**
- Detailed markdown cells explaining each analysis section
- Clear objectives and interpretations for each visualization

---

### 🔍 Analysis Methodology

#### Univariate Analysis:
- Distribution analysis for continuous variables
- Frequency analysis for categorical variables
- Statistical summaries and outlier identification

#### Bivariate Analysis:
- Temporal relationship exploration
- Categorical vs. continuous variable analysis
- Correlation analysis between numerical variables

#### Visualization Standards:
- Consistent color schemes and styling
- Appropriate chart types for data types
- Clear annotations and professional formatting

---

### 📈 Week 3 Key Metrics

| Metric | Value |
|--------|-------|
| **Visualizations Created** | 9+ comprehensive charts |
| **Analysis Dimensions** | Temporal, Categorical, Correlation |
| **Statistical Insights** | Top 5 positive/negative correlations |
| **Export Files** | 1 (EDA summary CSV) |
| **Notebook Cells** | 22+ analysis cells |

---

### ✅ Week 3 Deliverables

- [x] Complete temporal pattern analysis (monthly, daily, hourly)
- [x] Comprehensive airline performance analysis
- [x] Delay distribution and pattern analysis
- [x] Enhanced correlation analysis with automated insights
- [x] Professional visualizations with consistent styling
- [x] Statistical summary export for further analysis
- [x] Well-documented analysis with clear objectives
- [x] Interpretable insights for business decision-making

---

---

## ✈️ Week 4 Report – Advanced Delay Analysis & Insights

**Report Date:** November 3, 2025  
**Status:** ✅ Completed

### 🎯 Week 4 Goals
- Compare delay causes by airline (carrier, weather, NAS, security, late aircraft delays)
- Explore total and average delays by carrier and airport
- Identify peak delay times and delay-prone airports
- Analyze weather vs carrier delay correlations
- Visualize temporal delay patterns and summarize actionable insights

---

### 📈 Advanced Delay Analysis Completed

#### 1. **Comprehensive Delay Statistics**

✅ **Delay Types Analysis**
- Analyzed 6 key delay categories: Carrier, Weather, NAS, Security, Late Aircraft, and Total Arrival delays
- Generated statistical summaries for all delay types
- Identified delay distribution patterns and outliers

✅ **Airline Performance Benchmarking**
- Created carrier-specific delay summaries aggregated by total delay minutes
- Ranked airlines by total delay impact and average delay performance
- Established baseline metrics for airline reliability comparison

#### 2. **Airline Delay Performance Analysis**

✅ **Total Delay Rankings**
- Identified top 10 airlines by cumulative arrival delay minutes
- Visualization: Horizontal bar chart showing total delay burden by carrier
- Purpose: Understand which airlines contribute most to system-wide delays

✅ **Delay Cause Breakdown by Airline**
- Analyzed proportional contribution of different delay causes for top airlines
- Visualization: Stacked bar chart showing percentage breakdown of delay types
- Key Insights: Identified which airlines are affected more by weather vs operational issues

✅ **Average Delay Performance**
- Ranked airlines by average delay per flight
- Visualization: Bar chart showing average delay minutes by carrier
- Purpose: Identify airlines with consistently poor on-time performance

#### 3. **Weather vs Operational Delay Analysis**

✅ **Correlation Analysis**
- Scatter plot analysis of weather delay vs carrier delay (20,000 sample flights)
- Calculated correlation matrix between weather, carrier, NAS, and arrival delays
- Purpose: Understand relationships between different delay causes

✅ **Statistical Relationships**
- Quantified correlation coefficients between delay types
- Identified patterns in how different delay causes interact
- Established baseline for predictive modeling

#### 4. **Airport Performance Analysis**

✅ **Enhanced Airport Delay Visualization**
- Analyzed top 15 airports by average arrival delay
- **Professional Visualization Features:**
  - Gradient color scheme (red intensity based on delay severity)
  - Value labels on each bar showing exact delay minutes
  - Rotated airport codes for better readability
  - Grid lines and professional styling
  - Ranking system with medal emojis for top performers

✅ **Airport Delay Insights**
- **CMX (Houghton County Memorial)**: Highest average delay at 122.6 minutes
- **PLN (Pellston Regional)**: Second highest at 94.7 minutes  
- **SPI (Abraham Lincoln Capital)**: Third highest at 87.2 minutes
- Identified systematic issues at smaller regional airports

#### 5. **Temporal Delay Pattern Analysis**

✅ **Hourly Delay Patterns**
- Analyzed average arrival delay by departure hour (0-23)
- Visualization: Line plot showing delay trends throughout the day
- Purpose: Identify peak delay periods and optimal departure times

✅ **Seasonal Delay Analysis**
- Examined average arrival delay by month (1-12)
- Visualization: Line plot showing seasonal delay patterns
- Purpose: Understand weather and holiday impacts on delays

---

### 📊 Key Week 4 Insights Generated

#### Airline Performance Insights:
1. **Delay Distribution Patterns**: Clear identification of worst-performing carriers
2. **Operational vs Weather Impact**: Understanding which airlines are more susceptible to different delay types
3. **Performance Benchmarking**: Established relative performance metrics across carriers

#### Airport Operational Insights:
1. **Problem Airports**: Identified airports with systematic delay issues
2. **Regional vs Hub Performance**: Understanding delay patterns by airport type
3. **Capacity Constraints**: Airports showing consistent delay patterns

#### Temporal Operation Insights:
1. **Peak Delay Hours**: Identified times of day with highest delay risk
2. **Seasonal Patterns**: Understanding how delays vary throughout the year
3. **Operational Planning**: Data for optimizing flight schedules

#### Statistical Insights:
1. **Delay Correlations**: Quantified relationships between different delay causes
2. **Predictive Indicators**: Identified variables that could predict delays
3. **Risk Assessment**: Understanding delay risk factors

---

### 🎨 Advanced Visualization Techniques

| Analysis Type | Visualization Method | Enhancement Features |
|---------------|---------------------|---------------------|
| **Total Delays** | Horizontal bar charts | Color-coded by severity, clear ranking |
| **Delay Proportions** | Stacked bar charts | Percentage breakdown, legend positioning |
| **Average Performance** | Comparative bar charts | Gradient coloring, value annotations |
| **Correlations** | Scatter plots | Transparency, sample sizing, trend analysis |
| **Airport Rankings** | Enhanced bar charts | Gradient colors, rotated labels, value labels |
| **Temporal Patterns** | Line plots | Markers, grid lines, seasonal highlighting |

---

### 📁 Week 4 Deliverables

✅ **Comprehensive Delay Analysis**
- 8 different analysis dimensions covering all major delay factors
- Professional visualizations with enhanced styling and readability
- Statistical correlation analysis between delay types

✅ **Actionable Business Insights**
- Airport performance rankings with specific delay minutes
- Airline reliability benchmarking with cause breakdown
- Temporal optimization recommendations for flight scheduling

✅ **Advanced Data Visualization**
- Enhanced plotting with gradient colors and professional styling
- Value annotations and improved label positioning
- Consistent color schemes and standardized formatting

✅ **Statistical Documentation**
- Correlation matrices for delay relationships
- Performance rankings with quantified metrics
- Temporal pattern analysis with seasonal trends

---

### 🔍 Week 4 Methodology

#### Delay Cause Analysis:
- Categorical breakdown of delay types by airline
- Proportional analysis showing relative impact of different causes
- Correlation analysis between weather and operational delays

#### Performance Benchmarking:
- Total delay aggregation for system impact assessment
- Average delay calculation for per-flight performance
- Ranking systems for comparative analysis

#### Temporal Analysis:
- Hourly pattern recognition for operational optimization
- Seasonal trend analysis for capacity planning
- Peak period identification for resource allocation

#### Visualization Excellence:
- Professional styling with consistent color schemes
- Enhanced readability through proper label positioning
- Value annotations for precise data communication

---

### 📈 Week 4 Key Metrics

| Metric | Value |
|--------|-------|
| **Analysis Dimensions** | 8 comprehensive delay analyses |
| **Visualization Types** | 6 different chart types with enhancements |
| **Airlines Analyzed** | Top 10+ carriers with detailed breakdowns |
| **Airports Ranked** | Top 15 by average delay performance |
| **Temporal Periods** | 24-hour and 12-month pattern analysis |
| **Statistical Correlations** | 4x4 delay type correlation matrix |

---

### ✅ Week 4 Deliverables

- [x] Complete airline delay cause analysis with proportional breakdowns
- [x] Airport performance ranking with enhanced visualizations
- [x] Weather vs operational delay correlation analysis
- [x] Temporal delay pattern identification (hourly and seasonal)
- [x] Professional visualization enhancements with gradient colors
- [x] Statistical correlation analysis between delay types
- [x] Actionable insights for operational optimization
- [x] Business intelligence ready performance benchmarks

---

---

## 🗺️ Week 5 Report – Geographic Analysis & Route Intelligence

**Report Date:** November 23, 2025  
**Status:** ✅ Completed

### 🎯 Week 5 Goals
- Perform comprehensive route-level analysis with origin-destination pairs
- Create delay heatmaps by airport and temporal patterns
- Integrate geographic coordinate data for spatial analysis
- Develop interactive geographic visualizations of airport performance
- Generate actionable insights for route optimization and capacity planning

---

### 📊 Geographic Analysis Completed

#### 1. **Route Performance Analysis**

✅ **Top Route Identification**
- Analyzed all origin-destination pairs to identify busiest flight routes
- Generated comprehensive route statistics including flight volume, delays, and cancellation rates
- **Key Metrics per Route:**
  - Total flight count
  - Average departure delay
  - Average arrival delay  
  - Cancellation rate
- Visualization: Bar chart showing top 10 routes by flight volume

✅ **Route-Level Insights**
- Identified highest volume routes for capacity planning
- Analyzed delay patterns specific to route combinations
- Established baseline performance metrics for route optimization

#### 2. **Geographic Data Integration**

✅ **Airport Coordinates Database**
- Successfully downloaded and processed airport coordinates from GitHub dataset
- **Data Source:** `https://raw.githubusercontent.com/datasets/airport-codes/master/data/airport-codes.csv`
- **Processing Achievements:**
  - Parsed coordinate strings (longitude, latitude format)
  - Filtered for airports with valid IATA codes and coordinates
  - Created clean reference table with 📍 latitude/longitude data
  - Achieved geographic coordinate coverage for major airports

✅ **Data Enrichment**
- Enhanced flight data with geographic information
- Created comprehensive airport reference table including:
  - IATA codes
  - Airport names
  - Country information
  - Precise latitude/longitude coordinates
- **Output:** `processed/airport_stats_with_coords.csv`

#### 3. **Advanced Heatmap Visualizations**

✅ **Temporal-Airport Delay Heatmap**
- Created matrix visualization showing average arrival delays by:
  - **Y-axis:** Top 20 airports by flight volume
  - **X-axis:** Months (1-12)
  - **Color Intensity:** Average delay minutes
- **Enhanced Features:**
  - Red color gradient for intuitive delay interpretation
  - Proper axis labeling and colorbar
  - Focus on busiest airports for actionable insights

✅ **Route-Level Delay Heatmap**
- Advanced origin-destination delay matrix for top 15 airports
- **Professional Visualization Features:**
  - Seaborn styling with `RdYlBu_r` colormap
  - Annotated cells showing exact delay values (formatted to 1 decimal place)
  - Centered colormap around overall mean delay
  - Square cells with gridlines for better readability
  - Enhanced titles and axis labels with professional formatting

#### 4. **Geographic Performance Mapping**

✅ **Airport Statistics Integration**
- Successfully merged flight performance data with geographic coordinates
- **Combined Metrics:**
  - Total flights per airport
  - Average arrival delays
  - Average departure delays
  - Total delay minutes
  - Cancellation rates
  - Geographic coordinates (lat/lon)

✅ **Interactive Mapping Solution**
- **Challenge Resolution:** Overcame Plotly dependency issues (nbformat compatibility)
- **Robust Fallback Implementation:** Created professional matplotlib-based world map
- **Geographic Visualization Features:**
  - 🌍 World map with airport locations plotted by coordinates
  - 📊 Bubble sizes representing flight volume (scaled appropriately)
  - 🎨 Color coding by average delay (Red-Yellow-Blue gradient)
  - 🏷️ Top 10 airports labeled with IATA codes
  - 📈 Professional styling with grid references and colorbar

#### 5. **Airport Performance Intelligence**

✅ **Comprehensive Airport Rankings**
- **Top 10 Busiest Airports by Flight Volume:**
  1. **ATL (Atlanta)**: 131,613 flights, 40.7min avg delay
  2. **ORD (Chicago O'Hare)**: 125,979 flights, 50.8min avg delay  
  3. **DFW (Dallas-Fort Worth)**: 95,414 flights, 37.7min avg delay
  4. **DEN (Denver)**: 74,323 flights, 36.1min avg delay
  5. **LAX (Los Angeles)**: 58,772 flights, 33.8min avg delay

✅ **Performance Insights Generated**
- **🔴 Largest Operations Hub:** ATL with 131K+ flights
- **🟡 Highest Delay Airport:** JFK with 53.5 minutes average delay
- **🟢 Best Performance:** OAK (Oakland) with 26.3 minutes average delay
- **📍 Geographic Coverage:** Successfully mapped 50 busiest airports

---

### 🎨 Advanced Visualization Techniques

| Analysis Type | Visualization Method | Technical Enhancements |
|---------------|---------------------|------------------------|
| **Route Performance** | Enhanced bar charts | Rotated labels, professional styling |
| **Temporal Heatmaps** | Matrix visualizations | Color gradients, proper scaling |
| **Route Delay Matrix** | Seaborn heatmaps | Annotated values, centered colormaps |
| **Geographic Mapping** | Matplotlib scatter plots | Bubble sizing, color encoding, world coordinates |
| **Airport Rankings** | Professional scatter plots | Gradient coloring, annotation systems |

---

### 📁 Week 5 Deliverables

✅ **Geographic Data Infrastructure**
- `processed/airport_codes.csv` - Complete airport coordinates database
- `processed/airport_stats_with_coords.csv` - Flight performance data with geographic coordinates
- Integrated coordinate parsing and validation system

✅ **Advanced Visualizations**
- Route performance bar charts with professional styling
- Temporal-airport delay heatmaps with color coding
- Enhanced route-level delay matrices using seaborn
- Professional geographic scatter plot world map
- Airport performance rankings with statistical summaries

✅ **Intelligence & Analytics**
- Comprehensive route statistics for top flight paths
- Geographic performance analysis of major airports
- Temporal delay patterns by airport and month
- Route-specific delay correlation analysis
- Performance benchmarking with geographic context

✅ **Technical Solutions**
- Robust geographic data processing pipeline
- Dependency issue resolution with matplotlib fallback
- Professional visualization standards with consistent styling
- Automated coordinate parsing and validation
- Memory-efficient data processing for large datasets

---

### 🔍 Week 5 Methodology

#### Geographic Integration:
- **Data Acquisition:** Automated download of airport coordinates from authoritative source
- **Data Processing:** Robust coordinate parsing with error handling
- **Data Validation:** IATA code matching and coordinate verification
- **Data Enhancement:** Merging operational metrics with geographic data

#### Visualization Excellence:
- **Professional Styling:** Consistent color schemes and formatting
- **Information Density:** Optimal use of bubble sizes, colors, and annotations  
- **Readability:** Clear axis labels, legends, and title formatting
- **Technical Robustness:** Fallback solutions for dependency issues

#### Performance Analysis:
- **Multi-dimensional Analysis:** Route, temporal, and geographic perspectives
- **Statistical Rigor:** Proper aggregation methods and correlation analysis
- **Business Intelligence:** Actionable insights for operational decision-making
- **Scalable Architecture:** Efficient processing for large-scale airport data

---

### 📈 Week 5 Key Metrics

| Metric | Value |
|--------|-------|
| **Routes Analyzed** | All origin-destination pairs in dataset |
| **Airports Mapped** | 50+ busiest airports with coordinates |
| **Geographic Coverage** | Major airports across continental regions |
| **Visualization Types** | 5 different chart types with professional enhancements |
| **Data Files Generated** | 2 (airport coordinates + merged statistics) |
| **Performance Rankings** | Top 10 busiest + delay performance analysis |
| **Temporal Dimensions** | 12 months × 20+ airports heatmap analysis |

---

### 🏆 Week 5 Key Insights

#### Route Intelligence:
1. **Volume Leaders:** Identified highest traffic routes for capacity optimization
2. **Delay Hotspots:** Route-specific delay patterns for operational improvements
3. **Performance Benchmarking:** Established route-level performance baselines

#### Geographic Intelligence:  
1. **Hub Performance:** ATL leads in volume but ORD shows highest delays
2. **Regional Patterns:** Geographic distribution of delay performance
3. **Operational Optimization:** Identified best and worst performing airports by location

#### Temporal Intelligence:
1. **Seasonal Patterns:** Month-by-month delay variations by airport
2. **Airport-Specific Trends:** Individual airport delay profiles throughout year
3. **Capacity Planning:** Peak period identification for resource allocation

---

### ✅ Week 5 Deliverables

- [x] Complete route-level analysis with top 10 origin-destination pairs
- [x] Geographic coordinate integration with automated data processing
- [x] Advanced heatmap visualizations for temporal-airport delay patterns
- [x] Professional route-level delay matrix with enhanced seaborn styling
- [x] Robust geographic mapping solution with matplotlib fallback
- [x] Comprehensive airport performance rankings with geographic context
- [x] Statistical intelligence summaries for operational decision-making
- [x] Technical infrastructure for scalable geographic analysis

---

## ❄️ Week 6 Report – Seasonal & Cancellation Analysis

**Report Date:** November 23, 2025  
**Status:** ✅ Completed

### 🎯 Week 6 Goals
- Analyze monthly cancellation trends and seasonal patterns
- Break down cancellation types (Carrier, Weather, NAS, Security)
- Assess impact of holidays and winter months on flight operations
- Create seasonal visualizations for operational insights
- Investigate route congestion effects on cancellation rates

---

### 📊 Seasonal & Cancellation Analysis Completed

#### 1. **Monthly Cancellation Trends**

✅ **Seasonal Cancellation Patterns**
- Analyzed cancellation rates across all 12 months of 2008
- **Key Finding:** Dramatic seasonal variation with winter concentration
- **Pattern Identified:**
  - **Jan-Sep**: Virtually zero cancellations (~0.00%)
  - **October**: 0.05% cancellation rate
  - **November**: 0.09% cancellation rate  
  - **December**: 0.25% cancellation rate (peak)

✅ **Cancellation Volume Analysis**
- **Total Cancellations:** 633 out of 1,936,758 flights (0.03% overall rate)
- **Seasonal Distribution:**
  - Q4 (Oct-Dec): 633 cancellations (100% of total)
  - Q1-Q3: 0 cancellations
  - December alone: 480 cancellations (75.8% of annual total)

#### 2. **Cancellation Type Breakdown**

✅ **Root Cause Analysis**
- Successfully mapped cancellation codes to meaningful categories
- **Cancellation Type Distribution:**
  - **🌦️ Weather**: 307 cancellations (48.5%) - Dominant cause
  - **✈️ Carrier**: 246 cancellations (38.9%) - Operational issues  
  - **🏢 NAS**: 80 cancellations (12.6%) - Air traffic control/system
  - **🔒 Security**: 0 cancellations (0.0%) - No security-related cancellations

✅ **Monthly Type Progression**
- **October**: 59 total (Carrier 33, Weather 17, NAS 9)
- **November**: 94 total (Carrier 41, Weather 40, NAS 13)
- **December**: 480 total (Carrier 172, Weather 250, NAS 58)
- **Clear Pattern:** Weather becomes increasingly dominant in winter months

#### 3. **Winter vs Non-Winter Impact Analysis**

✅ **Seasonal Comparison**
- **Winter Months** (Dec, Jan, Feb): 0.083% cancellation rate
- **Non-Winter Months** (Mar-Nov): 0.011% cancellation rate
- **Impact Factor:** **7.4x higher** cancellation rate in winter
- **Statistical Significance:** 480 winter cancellations vs 153 non-winter

✅ **Winter Weather Dominance**
- Weather-related cancellations concentrate heavily in winter period
- Confirms expected seasonal airline operational challenges
- Provides baseline for winter operational planning

#### 4. **Holiday Impact Assessment**

✅ **Holiday vs Normal Day Analysis**
- **Holiday Dates Analyzed:** Dec 24, Dec 25, Dec 31, Jan 1, Nov 27 (Thanksgiving)
- **Holiday Cancellation Rate:** 0.089% 
- **Normal Day Rate:** 0.032%
- **Holiday Impact:** **2.8x higher** cancellation rate on holidays
- **Volume:** 25 holiday cancellations out of 28,017 holiday flights

✅ **Holiday Pattern Insights**
- Holidays show elevated but moderate impact compared to general winter effect
- Winter weather remains primary driver rather than holiday-specific issues
- Holiday effect compounds with winter seasonal challenges

#### 5. **Route Congestion & Cancellation Correlation**

✅ **Route Traffic Classification**
- **Total Routes Analyzed:** 5,205 unique origin-destination pairs
- **Congestion Categories:**
  - **High Congestion:** 1,766 routes (33.9%) - Top traffic routes
  - **Medium Congestion:** 1,721 routes (33.1%) - Moderate traffic
  - **Low Congestion:** 1,718 routes (33.0%) - Light traffic routes

✅ **Congestion Impact Results**
- **High Congestion Routes:** 0.031% average cancellation rate
- **Medium Congestion Routes:** 0.037% average cancellation rate  
- **Low Congestion Routes:** 0.035% average cancellation rate
- **Key Finding:** Medium-traffic routes show slightly higher cancellation vulnerability

✅ **Top Route Examples**
- **LAX-SFO:** 4,739 flights, 0 cancellations (0.000%)
- **ORD-LGA:** 4,396 flights, 2 cancellations (0.045%)
- **ATL-LGA:** 4,058 flights, 1 cancellation (0.025%)
- High-volume routes generally maintain good reliability

---

### 📈 Advanced Statistical Insights

#### Seasonal Intelligence:
1. **Winter Concentration:** 75.8% of annual cancellations occur in December alone
2. **Weather Dominance:** Weather causes nearly half of all cancellations (48.5%)
3. **Operational Resilience:** 99.97% overall completion rate demonstrates robust operations

#### Holiday Intelligence:
1. **Moderate Holiday Effect:** 2.8x increase over normal days
2. **Compounding Factors:** Holiday impact amplifies existing winter challenges
3. **Peak Period Planning:** December holidays require enhanced operational preparation

#### Route Intelligence:
1. **Traffic Paradox:** Medium-congestion routes show highest cancellation rates
2. **High-Volume Reliability:** Busiest routes maintain excellent performance
3. **Route Optimization:** Some route classifications may benefit from capacity adjustments

---

### 🎨 Comprehensive Visualization Portfolio

| Analysis Type | Visualization Method | Key Insights Revealed |
|---------------|---------------------|----------------------|
| **Monthly Trends** | Line plots with markers | Dramatic Q4 concentration |
| **Cancellation Types** | Stacked bar charts | Weather dominance in winter |
| **Seasonal Comparison** | Comparative bar charts | 7.4x winter impact factor |
| **Holiday Analysis** | Binary comparison charts | 2.8x holiday effect |
| **Route Congestion** | Category-based bar charts | Medium-route vulnerability |

---

### 📁 Week 6 Deliverables

✅ **Seasonal Intelligence Framework**
- Comprehensive monthly cancellation trend analysis
- Winter vs non-winter statistical comparison
- Holiday impact quantification and assessment
- Route congestion correlation analysis

✅ **Operational Decision Support**
- **Winter Preparation Metrics:** 7.4x impact factor for resource planning
- **Holiday Staffing Guidance:** 2.8x impact factor for peak periods
- **Route Optimization Data:** Medium-congestion route performance insights
- **Cancellation Type Priorities:** Weather (48.5%) and Carrier (38.9%) focus areas

✅ **Advanced Analytics Implementation**
- Robust data mapping and validation (fixed cancellation code handling)
- Multi-dimensional analysis across temporal, seasonal, and operational dimensions
- Statistical significance testing and impact factor calculations
- Comprehensive verification and data integrity checks

✅ **Business Intelligence Ready Insights**
- Actionable seasonal planning recommendations
- Quantified impact factors for operational scaling
- Route-specific performance benchmarking
- Weather vs operational cancellation prioritization framework

---

### 🔍 Week 6 Methodology

#### Data Quality Assurance:
- **Critical Fix:** Corrected cancellation code mapping (added "N" = None mapping)
- **Validation:** Verified total cancellation counts match across all analyses
- **Integrity Checks:** Confirmed percentage breakdowns sum to 100%

#### Statistical Rigor:
- **Impact Factors:** Calculated precise multiplier effects (7.4x winter, 2.8x holiday)
- **Segmentation Analysis:** Proper categorization of seasonal, holiday, and congestion factors  
- **Trend Analysis:** Month-by-month progression tracking
- **Correlation Assessment:** Route congestion vs cancellation rate relationships

#### Visualization Excellence:
- **Trend Clarity:** Clear seasonal patterns with appropriate scaling
- **Comparative Analysis:** Side-by-side winter/holiday comparisons
- **Category Breakdown:** Stacked visualizations showing type distributions
- **Professional Styling:** Consistent formatting and meaningful color coding

---

### 📈 Week 6 Key Metrics

| Metric | Value |
|--------|-------|
| **Total Cancellations Analyzed** | 633 across 1.9M flights |
| **Seasonal Periods Compared** | Winter vs Non-Winter (9 months each) |
| **Holiday Dates Assessed** | 5 major holidays |
| **Routes Categorized** | 5,205 unique routes by congestion level |
| **Cancellation Types Identified** | 4 primary categories (Weather, Carrier, NAS, Security) |
| **Peak Impact Factor** | 7.4x (Winter vs Non-Winter) |
| **Time Series Analysis** | 12 months of detailed progression |

---

### 🏆 Week 6 Key Findings

#### Critical Seasonal Insights:
1. **Q4 Concentration:** 100% of 2008 cancellations occurred in Oct-Dec
2. **December Dominance:** 75.8% of annual cancellations in single month
3. **Weather Leadership:** Nearly half of all cancellations weather-related
4. **Operational Excellence:** 99.97% overall flight completion rate

#### Actionable Business Intelligence:
1. **Winter Scaling:** Operations need 7.4x cancellation management capacity
2. **Weather Priority:** Weather-related contingency planning most critical
3. **Holiday Preparation:** 2.8x resource scaling for holiday periods
4. **Route Optimization:** Medium-congestion routes may need capacity review

#### Strategic Planning Framework:
1. **Seasonal Resource Allocation:** Data-driven winter staffing models
2. **Weather Contingency Planning:** Evidence-based weather response protocols
3. **Holiday Operations Management:** Quantified holiday impact planning
4. **Route Performance Optimization:** Congestion-based route efficiency improvements

---

### ✅ Week 6 Deliverables

- [x] Complete monthly cancellation trend analysis with seasonal patterns
- [x] Comprehensive cancellation type breakdown with weather dominance insights
- [x] Winter vs non-winter statistical comparison (7.4x impact factor)
- [x] Holiday vs normal day analysis (2.8x impact factor)  
- [x] Route congestion correlation analysis across 5,205+ routes
- [x] Advanced data quality fixes and validation framework
- [x] Business intelligence ready seasonal planning metrics
- [x] Statistical significance testing and impact factor quantification

---

### 📂 Project Structure

```
Mohammed_Shaaz/
├── data_1.ipynb                   # Week 1: Initial exploration & data loading
├── data_2.ipynb                   # Week 2: Preprocessing & feature engineering
├── data_3.ipynb                   # Week 3: Exploratory Data Analysis (EDA)
├── data_4.ipynb                   # Week 4: Advanced delay analysis & insights
├── data_5.ipynb                   # Week 5: Geographic analysis & route intelligence
├── data_6.ipynb                   # Week 6: Seasonal & cancellation analysis
├── dataset/
│   ├── DelayedFlights.csv        # 2008 data (1.9M rows)
│   ├── flight_delays.csv         # 2019-23 data (1.7M rows)
│   └── flights_sample_3m.csv     # 2024 sample (3M rows)
├── processed/
│   ├── delayedflights_2008_processed.parquet  # Cleaned & engineered
│   ├── sample_10k.parquet                      # Quick testing sample
│   ├── airport_codes.csv                       # Airport coordinates database
│   └── airport_stats_with_coords.csv           # Flight performance + coordinates
├── summary/
│   └── EDA_summary.csv           # Statistical summary from Week 3 EDA
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

**Last Updated:** November 23, 2025  
**Current Week:** Week 6 - Seasonal & Cancellation Analysis ✅ Complete
