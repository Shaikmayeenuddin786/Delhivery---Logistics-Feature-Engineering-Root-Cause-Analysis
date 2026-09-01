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




## Key Results (from Analysis)

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

### time_comparison_scatter
### Scatter Plot - od_duration vs start_scan_to_end_scan with y=x line
<img width="1381" height="800" alt="image" src="https://github.com/user-attachments/assets/5bcaea2d-ea26-4fc4-95f7-848292eb2df4" />
   
   **Key Findings**
   - Strong correlation (0.798) - Both measurements generally track each other
   - But significant difference - od_duration is on average 211 minutes LONGER than start_scan_to_end_scan
   - Median difference is only -50 seconds - Meaning half the trips have very close measurements
   - Large standard deviation (24,273 seconds ≈ 404 minutes) - High variability, some trips have huge differences

### Histogram - actual_time and osrm_distance
   <img width="649" height="347" alt="image" src="https://github.com/user-attachments/assets/931a2817-cf37-41fe-82e1-da757abd35ab" />
   <img width="660" height="345" alt="image" src="https://github.com/user-attachments/assets/9188cf0b-14e2-4a82-bf12-b3d232bfc347" />


   <img width="874" height="468" alt="image" src="https://github.com/user-attachments/assets/0c1d6005-acaa-442f-a572-954033a40d96" />

   <img width="881" height="473" alt="image" src="https://github.com/user-attachments/assets/fea4b61b-f6e5-4fca-b932-8caccbb4ea59" />





---

## Top 5 Business Insights 
#### *sorted On priority*

1. **Extreme Outliers distort averages** - Mean difference is -211 minutes but median is only -0.8 minutes
2. **Geographic concentration** - Haryana, Maharashtra, Karnataka account for 47.3% of deliveries
3. **OSRM underestimates 99.2% of trips** - Real-world factors add 15-20% to travel time
4. **Carting vs FTL are very different** - FTL is 50% faster but covers 12x longer distances
5. **Strong correlation (0.798)** but systematic difference between time metrics

---

## Top 5 Recommendations
#### *sorted On priority*

| Priority | Recommendation | Expected Impact |
|----------|---------------|-----------------|
| 1 | Add 20% buffer to OSRM ETAs | Reduce missed promises by 80% |
| 2 | Build real-time outlier detection | Catch severe delays early |
| 3 | Optimize top 3 states | 10-15% faster delivery |
| 4 | Separate models for Carting vs FTL | 15-20% better accuracy |
| 5 | Standardize time definitions | Clearer KPIs |


## Future Upgrades & Scaling Plan

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
