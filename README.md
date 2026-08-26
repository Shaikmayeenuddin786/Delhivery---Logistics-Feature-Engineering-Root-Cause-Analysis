# **Logistics Company**
### **Feature Engineering & Root Cause Analysis | Top Business Insights & Strategic Recommendations**

<img width="726" height="422" alt="image" src="https://github.com/user-attachments/assets/12ee2c11-41a9-4838-bf82-7cb477baf2a0" />


---

# **Quick Overview**

| **Section** | **Details** |
| :--- | :--- |
| **Business Problem** | Delhivery's raw logistics data is messy. One delivery trip is split across multiple rows, making it hard to use for forecasting. Data scientists need clean, processed data to build better models. |
| **Objectives** | 1. Clean and sanitize raw pipeline data<br>2. Merge multiple rows per trip into single records<br>3. Create useful features (city, state, time parts)<br>4. Compare actual times vs OSRM (routing engine) predictions<br>5. Handle missing values and outliers<br>6. Normalize and encode data for machine learning |
| **Technical Stack** | **Language:** Python 3.11<br>**Environment:** Jupyter Notebook<br>**Libraries:** Pandas, NumPy, Matplotlib, Seaborn, Scikit-learn, SciPy |


---

## **The Big Picture**

Delhivery is India's largest integrated logistics player. This project cleans and processes raw logistics data for Delhivery, India's largest logistics company. Raw trip data is split across multiple rows—like connecting flights—making it useless for forecasting. I merged 144,867 rows into 14,817 unique trips, created 28 new features, and uncovered that OSRM underestimates 99% of trips. The cleaned data and insights now help data scientists build better forecasting models, while business teams can add realistic buffers to delivery promises.


---

## Business Problem

Delhivery wants to understand and process data from their engineering pipelines:
- Clean and manipulate data to extract useful features from raw fields
- Make sense of raw data to help the data science team build forecasting models

**Key challenges:**
- One delivery trip is split across multiple rows (like connecting flights)
- Need to merge rows intelligently using aggregations
- Compare actual times vs OSRM (routing engine) predictions
- Handle missing values, outliers, and categorical variables

---

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

---

## Structural Flowchart

<img width="793" height="571" alt="image" src="https://github.com/user-attachments/assets/76ee09aa-1e34-4e5c-b076-04f172ce84b7" />

---

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

---

## Repository Structure

delhivery-feature-engineering/

<img width="1073" height="483" alt="image" src="https://github.com/user-attachments/assets/b1f1b96c-09cb-42b0-be3f-b1cf66d72749" />


---

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

---

## Top 5 Business Insights (sorted On priority)

1. **Extreme Outliers distort averages** - Mean difference is -211 minutes but median is only -0.8 minutes
2. **Geographic concentration** - Haryana, Maharashtra, Karnataka account for 47.3% of deliveries
3. **OSRM underestimates 99.2% of trips** - Real-world factors add 15-20% to travel time
4. **Carting vs FTL are very different** - FTL is 50% faster but covers 12x longer distances
5. **Strong correlation (0.798)** but systematic difference between time metrics

---

## Top 5 Recommendations (sorted On priority)

| Priority | Recommendation | Expected Impact |
|----------|---------------|-----------------|
| 1 | Add 20% buffer to OSRM ETAs | Reduce missed promises by 80% |
| 2 | Build real-time outlier detection | Catch severe delays early |
| 3 | Optimize top 3 states | 10-15% faster delivery |
| 4 | Separate models for Carting vs FTL | 15-20% better accuracy |
| 5 | Standardize time definitions | Clearer KPIs |

---

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

---


# 👤 **Author**

### **Shaik Mayeenuddin**

#### Business Analyst | Data Analytics & AI/ML | Optimizing Processes to Drive Revenue & Retention

🔗https://www.linkedin.com/in/shaikmayeenuddin
