# Delhi Air Quality Pollution Trends and Next-Day AQI Prediction

This repository contains the complete implementation of a data mining and machine learning project focused on analyzing long-term air pollution trends in Delhi and building a **next-day AQI category prediction system** using historical pollutant data.

The project combines:
- Exploratory Data Analysis (EDA)
- Feature Engineering on time-series data
- Baseline and advanced Machine Learning models
- Realistic forecasting without information leakage
- A fully documented IEEE-format research report

---

## Project Objectives

- Analyze **pollution trends** in Delhi from 2021 to 2024
- Study **seasonal variation, correlations, and WHO exceedance**
- Build a **next-day AQI category prediction model**
- Compare a **baseline PCA + KNN model** with an improved **Random Forest forecasting model**
- Deliver a **leakage-free, deployable prediction system**

---

## Dataset Description

- **City:** Delhi, India
- **Time Span:** January 1, 2021 – December 31, 2024
- **Frequency:** Daily
- **Total Records:** 1460

### Features:
- **Pollutants:**
  - PM2.5
  - PM10
  - NO2
  - SO2
  - CO
  - Ozone

- **Temporal Attributes:**
  - Date, Month, Year, Day
  - Holidays_Count

- **Derived Feature:**
  - AQI (Air Quality Index)

### Target Variable:
- **AQI_Category:**
  - Good
  - Satisfactory
  - Moderate
  - Poor
  - Very Poor
  - Severe

---

## Exploratory Data Analysis (EDA)

The EDA revealed:

- **Strong seasonality**:
  - Worst pollution during **winter (Oct–Jan)**
  - Cleanest air during **monsoon months**

- **Pollutant dominance**:
  - PM2.5 and PM10 are the **primary AQI drivers**
  - SO2 shows gradual upward trend
  - Ozone increases due to photochemical activity

- **Correlation structure**:
  - PM2.5 and PM10 have the strongest correlation with AQI
  - Gaseous pollutants show moderate influence

- **WHO Guideline Exceedance**:
  - PM2.5 and PM10 exceed WHO limits on **most days**
  - Indicates chronic air quality risk in Delhi

---

## Feature Engineering

To model temporal behavior, the following features were engineered:

### Lag Features (for all pollutants):
- 1-day lag
- 2-day lag
- 7-day lag

### Rolling Statistics:
- 3-day rolling mean
- 7-day rolling mean

### Seasonality Encoding:
- Seasonal category (Winter, Summer, Monsoon, Post-monsoon)
- Sine and Cosine encoding of Month
- Weekend indicator

**Note:** All **AQI-derived features were removed** during final training to prevent **data leakage**.

---

## Machine Learning Models

### 1. Baseline Model: PCA + KNN
- PCA for dimensionality reduction
- KNN for multi-class classification
- Best configuration:
  - PCA Components = 11
  - Neighbors (k) = 11
- **Accuracy:** ~68%

### 2. Final Forecasting Model: Random Forest (Leakage-Free)
- Uses **only historical pollutant features**
- Handles:
  - Nonlinear relationships
  - Feature interactions
  - Class imbalance
- Hyperparameters tuned using validation year (2023)
- **True Forecasting Accuracy (2024): ~79%**

---

## Final Model Performance (2024 Test Set)

- **Overall Accuracy:** ~78.96%
- Performs well on:
  - Moderate
  - Poor
  - Satisfactory
- Lower recall for:
  - Very Poor
  - Severe
  (due to rarity and missing weather data)

Evaluation includes:
- Confusion Matrix
- Precision
- Recall
- F1-score

---

## Next-Day Prediction

The trained Random Forest model is used to predict:
- **AQI category for the next day**
- Based solely on:
  - Past pollutant behavior
  - Temporal patterns
  - Seasonal effects

This ensures **real-world deployability**.

---

## How to Run the Project

### 1. Clone the Repository
```bash
git clone https://github.com/Shreyas-Sarkar/Delhi-Air-Quality-Pollution-Trends.git
cd Delhi-Air-Quality-Pollution-Trends
```

### 2. Create a Virtual Environment (Recommended)
```bash
python -m venv venv
source venv/bin/activate    # For Linux/Mac
venv\Scripts\activate       # For Windows
```

### 3. Install Required Dependencies
```bash
pip install -r requirements.txt
```

### 4. Run the Notebooks in Order
Open Jupyter Notebook or VS Code and execute the notebooks sequentially:

- **`notebooks/Delhi_AIir_Quality_General_Analysis.ipynb`**
  Performs exploratory data analysis and visualization.

- **`notebooks/Next_Day_AQI_Category_KNN_PCA.ipynb`**
  Builds the baseline PCA + KNN classifier.

- **`notebooks/Next_Day_AQI_Category_RandomForest_Without_AQI.ipynb`**
  Trains the final Random Forest model (Leakage-Free) and performs next-day prediction.

- **`notebooks/Next_Day_AQI_Category_RandomForest_With_AQI.ipynb`**
  Trains a Random Forest model including AQI features for comparison.

---

## Research Report
The complete IEEE-format research paper is available at:

`reports/A_Data_Mining_Project_Title_in_IEEE_Double_Column_Format.pdf`

This paper documents:
- Dataset description
- EDA findings
- Feature engineering
- Model architecture
- Evaluation
- Final conclusions

---

## Project Limitations
- Meteorological factors such as wind speed, rainfall, and temperature are not included
- Extreme AQI categories (Severe) are harder to predict due to class imbalance
- The model is trained only on Delhi data
- Prediction horizon is limited to one day ahead

---

## Future Enhancements
- Integrate real-time weather data APIs
- Apply boosting algorithms such as XGBoost or LightGBM
- Extend forecasting to multi-day prediction
- Deploy the model as a web-based AQI forecasting system

---

## Authors
- Priyank Gaur
- Dhruv Sareen
- Shreyas Sarkar

**Team Name:** Teen
