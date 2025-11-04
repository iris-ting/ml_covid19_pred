## Project Overview  
This project investigates whether vaccine uptake and COVID-19 positivity rates can be predicted from behavioral and attitudinal data.  
By combining data preprocessing, modeling, and clustering, we aim to support targeted public health strategies and policy recommendations.

---

## Repository Structure  
```
data/
│
├── covidcast_new.csv          # Original raw dataset
├── covid_data_x_filled.csv    # Dataset after KNN imputation for independent variables
└── covid_fill_x_y.csv         # Dataset after completing proxy-labeled target variables

code/
│
├── 01_EDA.ipynb                      # Exploratory data analysis and validation
├── 02_Knn with missing data.ipynb    # KNN-based imputation for missing features
├── 03_Proxy Model for target variables.ipynb  # Random Forest proxy model for missing targets
├── 04_Model_vaccine_uptake.ipynb     # Modeling vaccine uptake (Ridge, Lasso, NN, XGBoost)
├── 05_Model with covid positive.ipynb# Modeling COVID-19 positivity rates
└── 06_Clustering.ipynb               # Behavioral clustering and policy recommendations
```

---

## Analysis Structure  

### 1. Data Analysis  
- **Data Understanding:** County-level COVID-related behaviors and attitudes (25,626 rows, 19 columns).  
- **Validation:** Range checks and outlier detection using IQR.  
- **Correlation Analysis:** Removal or combination of highly correlated variables.  
- **Missing Values:**  
  - Independent variables imputed via **KNN (k=3)**.  
  - Target variables imputed via **Random Forest proxy model**.  
  - Final cleaned datasets saved in `data/` for reuse.  

### 2. Modeling  
- **Targets:**  
  - Vaccine Uptake (`smoothed_wcovid_vaccinated`)  
  - COVID Positivity (`smoothed_wtested_positive_14d`)  
- **Models Compared:** Ridge, Lasso, Neural Network, XGBoost  
- **Feature Engineering:**  
  - Temporal features (time, phase indicators)  
  - Log transformation for skewed variables  
- **Best Models:**  
  - Vaccine Uptake → Neural Network (R² = 0.80)  
  - COVID Positivity → XGBoost (R² = 0.92)

### 3. Clustering and Policy Insights  
- **Clustering Method:** K-Means (k=3)  
- **Cluster Profiles:**  
  - Cluster 0: Balanced behavior, average vaccination  
  - Cluster 1: Skeptical, low trust, moderate vaccination  
  - Cluster 2: Cautious, high trust, low vaccination  
- **Policy Recommendations:**  
  - Maintain current messaging for Cluster 0  
  - Peer-based trust campaigns for Cluster 1  
  - Improve accessibility for Cluster 2  

