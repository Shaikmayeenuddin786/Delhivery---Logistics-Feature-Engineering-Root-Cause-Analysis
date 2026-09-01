# **Logistics Company**
### **Feature Engineering & Root Cause Analysis | Top Business Insights & Strategic Recommendations**

<img width="726" height="422" alt="image" src="https://github.com/user-attachments/assets/12ee2c11-41a9-4838-bf82-7cb477baf2a0" />


---

## **Quick Overview**

| **Section** | **Details** |
| :--- | :--- |
| **Business Problem** | Raw logistics data is messy. One delivery trip is split across multiple rows, making it useless for forecasting. Data scientists need clean, processed data to build better models. |
| **Objectives** | 1. Clean and sanitize raw pipeline data<br>2. Merge multiple rows per trip into single records<br>3. Create useful features (city, state, time parts)<br>4. Compare actual times vs OSRM predictions<br>5. Handle missing values and outliers<br>6. Normalize and encode data for ML |
| **Technical Stack** | Python 3.11, Jupyter Notebook, Pandas, NumPy, Matplotlib, Seaborn, Scikit-learn, SciPy |
| **Project Features** | • 144,867 raw rows → merged into 14,817 unique trips<br>• Created 28 new features<br>• 99.2% of trips took longer than OSRM predicted<br>• Handled missing values and capped outliers<br>• Applied one-hot encoding and normalization |
| **Start-to-End Pipeline** | Data Loading → Data Cleaning → Feature Engineering (city, state, time parts) → Trip Merging (groupby) → Time/Distance Comparison → Outlier Detection & Capping → Missing Value Treatment → Encoding & Normalization → Business Insights |
| **Top Strategic Recommendations** | • Add 20% buffer to OSRM ETAs – reduce missed promises by 80%<br>• Build real-time outlier detection – catch severe delays early<br>• Optimize top 3 states – achieve 10-15% faster delivery<br>• Separate models for Carting vs FTL – get 15-20% better accuracy<br>• Standardize time definitions – create clearer KPIs |
| **Future Upgrades & Scaling Plan** | • Deploy as real-time API – let systems get engineered data on demand<br>• Automate pipeline with Apache Airflow – run daily without manual work<br>• Move to cloud data warehouse – handle larger datasets faster<br>• Real-time outlier detection – flag unusual trip patterns as they happen |


---

## **The Big Picture**

Delhivery is India's largest integrated logistics player. This project cleans and processes raw logistics data for Delhivery, India's largest logistics company. Raw trip data is split across multiple rows—like connecting flights—making it useless for forecasting. I merged 144,867 rows into 14,817 unique trips, created 28 new features, and uncovered that OSRM underestimates 99% of trips. The cleaned data and insights now help data scientists build better forecasting models, while business teams can add realistic buffers to delivery promises.




## Business Problem

Delhivery wants to understand and process data from their engineering pipelines:
- Clean and manipulate data to extract useful features from raw fields
- Make sense of raw data to help the data science team build forecasting models

**Key challenges**
- One delivery trip is split across multiple rows (like connecting flights)
- Need to merge rows intelligently using aggregations
- Compare actual times vs OSRM (routing engine) predictions
- Handle missing values, outliers, and categorical variables



## Objectives

| # | Objective |
|---|-----------|
| 1 | Define problem statement and perform EDA | 
| 2 | Create new features (city, state, time parts) |
| 3 | Merge multiple rows per trip using groupby |
| 4 | Compare time and distance fields (actual vs OSRM) |
| 5 | Detect and cap outliers using IQR method |
| 6 | Handle missing values (median for numbers, mode for categories) |
| 7 | Analyze relationships between aggregated fields |
| 8 | Apply one-hot encoding to categorical variables |
| 9 | Normalize and standardize numerical features |
| 10 | Generate business insights and recommendations |

## Technical Stack

| Tool | Purpose |
|------|---------|
| Python 3.11 | Core programming language |
| Jupyter Notebook 7.2.2 | Interactive development environment |
| Pandas 2.2.3 | Data manipulation and aggregation |
| NumPy 2.2.5 | Numerical operations |
| Matplotlib 3.10.1 | Data visualization |
| Seaborn 0.13.2 | Statistical visualizations |
| Scikit-learn 1.6.1 | Scaling, encoding, preprocessing |
| SciPy 1.5.2 | Statistical tests (t-test) |


## Structural Flowchart

<img width="793" height="571" alt="image" src="https://github.com/user-attachments/assets/76ee09aa-1e34-4e5c-b076-04f172ce84b7" />



## Repository Structure

delhivery-feature-engineering/

<img width="1073" height="483" alt="image" src="https://github.com/user-attachments/assets/b1f1b96c-09cb-42b0-be3f-b1cf66d72749" />


# INSIGHTS - Exploratory Data analysis (EDA)
---
## DATASET SHAPE & STRUCTURE

| Metric | Value |
|--------|-------|
| Total original rows (segments) | 144,867 |
| Total unique trips (after merging) | 14,817 |
| Features created | 28 |
| Features after one-hot encoding | 17,805 |
| Correlation (od_duration vs start_scan) | 0.7980 |
| Mean time difference | -12,660 seconds (-211 minutes) |
| Median time difference | -50 seconds (-0.8 minutes) |
| Trips where actual > OSRM | 99.2% |
| Data completeness after cleaning | 100% |

## MISSING VALUES ANALYSIS

| Column | Missing Count | % Missing | Action Taken |
| :--- | :---: | :---: | :--- |
| **cutoff_timestamp** | 144,867 | 100% | Dropped |
| **cutoff_factor** | 144,867 | 100% | Dropped |
| **factor** | 144,867 | 100% | Dropped |
| **segment_factor** | 144,867 | 100% | Dropped |
| **is_cutoff** | 144,867 | 100% | Dropped |
| **od_start_time** | 0 | 0% | Converted to datetime |
| **od_end_time** | 0 | 0% | Converted to datetime |
| **start_scan_to_end_scan** | 0 | 0% | Kept as numeric |
| **All other columns** | 0 | 0% | No missing values |


## A. CONTINUOUS VARIABLE DISTRIBUTION ANALYSIS
### COMPARING TIME MEASUREMENTS
### Scatter Plot - od_duration vs start_scan_to_end_scan with y=x line
  <img width="1381" height="800" alt="image" src="https://github.com/user-attachments/assets/5bcaea2d-ea26-4fc4-95f7-848292eb2df4" />
   
   **Key Findings**
   - Strong correlation (0.798) - Both measurements generally track each other
   - But significant difference - od_duration is on average 211 minutes LONGER than start_scan_to_end_scan
   - Median difference is only -50 seconds - Meaning half the trips have very close measurements
   - Large standard deviation (24,273 seconds ≈ 404 minutes) - High variability, some trips have huge differences


#### Time-Based Distributions

| Variable | Skewness | Shape | Key Finding |
| :--- | :--- | :--- | :--- |
| **start_scan_to_end_scan** | Right-Skewed | Moderate tail | Range: 49 to 3,099 minutes |
| **actual_time** | Right-Skewed | Long tail | Many short trips, few very long trips |
| **osrm_time** | Right-Skewed | Similar to actual_time | Tracks actual_time but underestimates |
<img width="687" height="360" alt="image" src="https://github.com/user-attachments/assets/c17e64aa-24bc-4133-84ea-b21cd0dcbdfb" />
<img width="696" height="373" alt="image" src="https://github.com/user-attachments/assets/7677ac9a-721a-43ad-aca1-342e190d66a9" />
<img width="697" height="366" alt="image" src="https://github.com/user-attachments/assets/b4d4fa4e-0e87-4057-94ab-92b774bc50dc" />

#### Distance-Based Distributions

| Variable | Min | Max | Distribution |
| :--- | :---: | :---: | :--- |
| **actual_distance_to_destination** | ~1 km | ~400 km | Right-skewed |
| **osrm_distance** | ~1 km | ~400 km | Similar pattern |
<img width="705" height="369" alt="image" src="https://github.com/user-attachments/assets/e5de504e-b466-4a2b-a070-6bb15b3d5694" />

  
## B. CATEGORICAL VARIABLES DISTRIBUTION ANALYSIS
#### Route Type Distribution
Carting (Short distance, multi-stop):
 • Avg actual time: 70.64 minutes
 • Avg distance: 26.62 km
 - This means trips are short (26.62 km avg), dispatchers can quickly re-route trucks, make multi-stop drops, and handle urgent local delivery shifts with minimal downtime.

FTL (Full Truck Load - Direct):
 • Avg actual time: 574.01 minutes
 • Avg distance: 328.18 km
 - By filling an entire truck for a single direct run (328.18 km avg), you eliminate intermediate handling, reduce cargo damage risks, and secure the lowest possible shipping rate per mile.

<img width="636" height="824" alt="image" src="https://github.com/user-attachments/assets/1f5059b3-465c-472a-8d4c-3d1073266e93" />


Key Finding: Carting (short-distance, multi-stop) represents nearly 70% of all delivery segments.
<img width="644" height="831" alt="image" src="https://github.com/user-attachments/assets/ace39599-4ebc-4967-bb94-f48ca58f026c" />



### Histogram - actual_time and osrm_distance
<img width="649" height="347" alt="image" src="https://github.com/user-attachments/assets/931a2817-cf37-41fe-82e1-da757abd35ab" />
<img width="660" height="345" alt="image" src="https://github.com/user-attachments/assets/9188cf0b-14e2-4a82-bf12-b3d232bfc347" />


   <img width="874" height="468" alt="image" src="https://github.com/user-attachments/assets/0c1d6005-acaa-442f-a572-954033a40d96" />

   <img width="881" height="473" alt="image" src="https://github.com/user-attachments/assets/fea4b61b-f6e5-4fca-b932-8caccbb4ea59" />




---

## **Top 5 Business Insights**
#### *sorted On priority*


### INSIGHT 1: Extreme Outliers Hide the Real Picture

- **Average trip difference:** 211 minutes
- **Median trip difference:** Only 0.8 minutes (50 seconds)
- **What this means:** Most trips are fine, but a few severely delayed trips (4-10+ hours) are making the average look bad
- **Business Impact:** Don't trust averages – they hide the fact that most trips are running well


### INSIGHT 2: Business is Concentrated in 3 States ( Geographic Distribution)

  | Source State | Delivery Count | Percentage |
  | :--- | :---: | :---: |
  | **Haryana** | 27,499 | 19.0% |
  | **Maharashtra** | 21,401 | 14.8% |
  | **Karnataka** | 19,578 | 13.5% |
  | **Tamil Nadu** | 7,494 | 5.2% |
  | **Gujarat** | 7,202 | 5.0% |
  | **Others** | 61,693 | 42.5% |
  
  | Destination State | Delivery Count | Percentage |
  | :--- | :---: | :---: |
  | **Karnataka** | 21,065 | 14.5% |
  | **Haryana** | 20,622 | 14.2% |
  | **Maharashtra** | 18,196 | 12.6% |
  | **West Bengal** | 8,499 | 5.9% |
  | **Telangana** | 8,205 | 5.7% |

*Finding: Top 3 source states account for 47.3% of all deliveries.*
- **47% of all deliveries** come from just 3 states: **Haryana, Maharashtra, and Karnataka**
- **What this means:** Your business is heavily dependent on this corridor
- **Business Impact:** Any disruption in these states affects half your operations


### INSIGHT 3: OSRM Almost Always Underestimates Time

- **99.2%** of trips take longer than OSRM predicts
- **Typical overage:** 15-20% above OSRM estimate
- **What this means:** The routing engine never accounts for real-world delays (traffic, loading, breaks)
- **Business Impact:** Customer ETAs based on OSRM are almost always wrong (too optimistic)


### INSIGHT 4: Carting and FTL are Two Different Businesses

| Metric | Carting | FTL |
|:-------|:--------|:----|
| Avg Time | 71 min | 574 min (9.6 hours) |
| Avg Distance | 27 km | 328 km |
| Speed | 23 km/hr | 34 km/hr |

- **What this means:** FTL is 50% faster but covers 12x longer distances
- **Business Impact:** One-size-fits-all forecasting and pricing will fail – you need separate strategies


### INSIGHT 5: Strong Correlation but Systematic Difference

- **Correlation:** 0.798 (strong positive)
- **What this means:** Both metrics measure trip duration well, but `od_duration` includes more waiting/idle time than `start_scan`
- **Business Impact:** Use `start_scan` for customer promises (tighter), `od_duration` for internal efficiency monitoring


## Much Simpler Summary (non Tech)

| # | Insight | One-Liner |
|:--|:--------|:----------|
| 1 | Outliers | A few bad trips are hiding the fact that most trips are running fine |
| 2 | Geography | 47% of deliveries come from just 3 states – focus optimization there |
| 3 | OSRM | It underestimates 99% of trips – add a 20% buffer to ETAs |
| 4 | Carting vs FTL | They're completely different – build separate models for each |
| 5 | Time Metrics | `start_scan` for customers, `od_duration` for internal tracking |


---

## Top 5 Recommendations
#### *sorted On priority*

### PRIORITY 1: Add 20% Buffer to OSRM ETAs

| What | Details |
|:-----|:---------|
| **Problem** | OSRM underestimates 99% of trips |
| **Solution** | Multiply all ETAs by 1.2 before showing customers |
| **Impact** | Reduce missed delivery promises by ~80% |
| **Effort** | 1-2 days, near zero cost |
| **ROI** | Very High (happy customers) |

**Action:** Update  ETA API to add a 20% buffer.


### PRIORITY 2: Build Real-Time Outlier Detection

| What | Details |
|:-----|:---------|
| **Problem** | Extreme delays (211 min avg) hide normal performance |
| **Solution** | Flag trips that are >1.5x slower than normal |
| **Impact** | Catch severe delays within 30 minutes |
| **Effort** | 2-3 weeks, low cost |
| **ROI** | High (proactive problem solving) |

**Action:** Alert operations team when a trip becomes an outlier.



### PRIORITY 3: Optimize Top 3 States

| What | Details |
|:-----|:---------|
| **Problem** | 47% of deliveries from just 3 states |
| **Solution** | Add warehouses and fleet in Haryana, Maharashtra, Karnataka |
| **Impact** | 10-15% faster delivery in high-volume corridors |
| **Effort** | 3-6 months, medium cost |
| **ROI** | High (scaling efficiency) |

**Action:** Audit capacity in top 3 states. Add resources where utilization >80%.



### PRIORITY 4: Separate Models for Carting vs FTL

| What | Details |
|:-----|:---------|
| **Problem** | Carting (71 min, 27 km) and FTL (574 min, 328 km) are very different |
| **Solution** | Build two separate forecasting models |
| **Impact** | 15-20% better ETA accuracy |
| **Effort** | 4-6 weeks, low cost |
| **ROI** | Medium-High (better predictions) |

**Action:** Split training data by `route_type`. Train separate models.



### PRIORITY 5: Standardize Time Definitions

| What | Details |
|:-----|:---------|
| **Problem** | `od_duration` and `start_scan` measure the same thing but differ systematically |
| **Solution** | Document definitions. Use `start_scan` for customer metrics. |
| **Impact** | Clearer KPIs, less confusion |
| **Effort** | 1 week, near zero cost |
| **ROI** | Low-Medium (organizational clarity) |

**Action:** Create a data dictionary defining each time field and its use.



##  Quick Overall Summary (non tech audiance)


| Priority | Recommendation | Time | ROI | Business Impact |
| :---: | :--- | :---: | :---: | :--- |
| **1** | Add 20% buffer to OSRM ETAs | 2 days | Very High | Reduce missed promises by 80% |
| **2** | Real-time outlier detection | 3 weeks | High | Catch severe delays early |
| **3** | Optimize top 3 states | 6 months | High | 10-15% faster delivery |
| **4** | Separate Carting vs FTL models | 6 weeks | Medium-High | 15-20% better accuracy |
| **5** | Standardize time definitions | 1 week | Low-Medium | Clearer KPIs |




## **Future Upgrades & Scaling Plan**


Deploy as a Real-Time API
- Currently, the feature engineering is done in a Jupyter notebook. Building a FastAPI endpoint would let other systems (like routing engines or operations dashboards) get cleaned, engineered data on demand, enabling real-time decision-making.

Automate the Pipeline with Apache Airflow
- Schedule the entire data cleaning, merging, and feature engineering process to run daily without manual intervention. This ensures data scientists always have fresh, processed data to build better forecasting models.

Integrate with a Cloud Data Warehouse
- Move from local CSV files to a cloud database (like Snowflake or BigQuery). This would allow handling of much larger datasets, enable faster queries, and make it easier to share data across teams.

Build a Real-Time Outlier Detection System
- Instead of detecting outliers after the fact, build a system that flags unusual trip patterns (like extreme delays or unexpected routes) as they happen. Operations teams can then intervene immediately to resolve issues.



## Environment Setup
### How to Run

1. Clone this repository
2. Install required libraries:
   ```
   pip install -r requirements.txt
   ```
   pip install pandas numpy matplotlib seaborn scikit-learn scipy
3. Open the Jupyter notebook:
   ```
   Jupyter_Delhivery_Feature_Engineering.ipynb
   [Delhivery_Feature Engineering.ipynb](https://github.com/user-attachments/files/28537543/Delhivery_Feature.Engineering.ipynb)
4. Run the cells sequentially to reproduce the analysis.

**Note:** The dataset is not included in this repository due to size/confidentiality. Please place your data file in the `data/raw/` folder and update the file path in the notebook.




## 👤 **Author**

### **Shaik Mayeenuddin**

#### Business Analyst | Data Analytics & AI/ML | Optimizing Processes to Drive Revenue & Retention

🔗https://www.linkedin.com/in/shaikmayeenuddin
