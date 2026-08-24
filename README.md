# 📈 Saudi Stock Market Time Series Forecasting

An end-to-end **Time Series Forecasting and Machine Learning project** for forecasting the **Tadawul All Share Index (TASI)** using statistical, machine learning, and deep learning models.

The project compares six forecasting approaches under the same train/test evaluation framework:

- ARIMA
- SARIMA
- Prophet
- Random Forest
- XGBoost
- LSTM

The objective is not only to generate forecasts, but also to systematically compare different modeling families and identify the most effective approach for the available Saudi stock market time-series data.

---

## 🎯 Project Objective

Financial time-series forecasting is challenging because market data can contain:

- Trends
- Seasonal behavior
- Non-linear relationships
- Structural changes
- Temporal dependencies

This project investigates whether traditional statistical models, machine-learning models, or deep-learning architectures provide the best forecasting performance for **TASI**.

---

## 📊 Dataset

The project uses historical Saudi stock market data from the **Tadawul Statistical Bulletin**.

### Target Variable

**Tadawul All Share Index (TASI)**

### Final Modeling Dataset

After preprocessing:

- **44 observations**
- Training observations: **35**
- Testing observations: **9**

### Training Period

**First Half 2015 → Fourth Quarter 2023**

### Testing Period

**First Quarter 2024 → First Quarter 2026**

The final test period was kept separate to evaluate how well each model performs on unseen observations.

---

## 🧹 Data Preparation

The workflow includes:

- Data loading and inspection
- Target-variable identification
- Data cleaning
- Period normalization
- Missing-value handling
- Chronological train/test splitting
- Feature engineering
- Lag generation
- Rolling statistics
- Model-specific preprocessing
- Scaling for deep learning

Engineered time-series features include:

- `Lag_1` to `Lag_6`
- `Rolling_Mean_3`
- `Rolling_Mean_6`
- `Rolling_STD_3`
- `Rolling_STD_6`
- Percentage change
- First difference

---

## 🤖 Forecasting Models

### 1. ARIMA

ARIMA was optimized using a grid-search strategy with `statsmodels`.

**Best configuration:**

**ARIMA Order:** `(0, 2, 1)`

### 2. SARIMA

SARIMA extends ARIMA by incorporating seasonal structure.

**Best configuration:**

**SARIMA Order:** `(0, 1, 2)`  
**Seasonal Order:** `(0, 1, 1, 4)`

The seasonal period of `4` represents quarterly seasonality.

### 3. Prophet

Prophet was used as an additional statistical forecasting approach capable of modeling trend and temporal patterns.

**Test performance:**

**RMSE:** `1248.63`  
**MAE:** `1082.61`  
**MAPE:** `9.42%`

### 4. Random Forest

Random Forest regression was trained using lag-based time-series features to capture non-linear relationships.

**Test performance:**

**RMSE:** `679.33`  
**MAE:** `554.05`  
**MAPE:** `4.68%`

### 5. XGBoost

XGBoost was used as a gradient-boosting forecasting approach using engineered temporal features.

**Test performance:**

**RMSE:** `811.23`  
**MAE:** `681.86`  
**MAPE:** `5.76%`

### 6. LSTM

A multi-layer **Long Short-Term Memory neural network** was implemented to capture sequential dependencies in TASI.

**Architecture:**

**LSTM:** 50 units with `return_sequences=True`  
**Dropout:** 0.2  
**LSTM:** 50 units  
**Dropout:** 0.2  
**Output Layer:** Dense(1)

**Training configuration:**

**Window Length:** `3`  
**Training Epochs:** `100`  
**Total Parameters:** `30,651`  
**Scaling:** `MinMaxScaler`

The scaler was fitted on the training data only to prevent data leakage.

---

## 📈 Model Performance

Models were evaluated using:

- **RMSE — Root Mean Squared Error**
- **MAE — Mean Absolute Error**
- **MAPE — Mean Absolute Percentage Error**

| Model | RMSE | MAE | MAPE |
|---|---:|---:|---:|
| ARIMA | 1595.29 | 1304.24 | 11.61% |
| SARIMA | 1883.77 | 1579.01 | 14.03% |
| Prophet | 1248.63 | 1082.61 | 9.42% |
| Random Forest | 679.33 | 554.05 | 4.68% |
| XGBoost | 811.23 | 681.86 | 5.76% |
| **LSTM** | **587.50** | **424.52** | **3.70%** |

---

## 🏆 Best Model

The **LSTM model achieved the best overall forecasting performance**.

**LSTM Results:**

**RMSE:** `587.50`  
**MAE:** `424.52`  
**MAPE:** `3.70%`

Random Forest achieved the second-best result with a MAPE of approximately **4.68%**.

### Performance Ranking by MAPE

1. **LSTM** — 3.68%
2. **Random Forest** — 4.68%
3. **XGBoost** — 5.76%
4. **Prophet** — 9.42%
5. **ARIMA** — 11.61%
6. **SARIMA** — 14.03%

The results indicate that, on this dataset and evaluation split, the non-linear machine-learning and deep-learning approaches outperformed the classical statistical forecasting models.

---

## 🧠 Key Findings

### Deep Learning

LSTM produced the lowest forecasting error and demonstrated the strongest predictive performance on the test period.

### Machine Learning

Random Forest and XGBoost significantly outperformed ARIMA, SARIMA, and Prophet.

Random Forest was particularly competitive, achieving a MAPE below 5%.

### Statistical Forecasting

ARIMA and SARIMA provided useful statistical baselines but produced higher forecasting errors than the machine-learning approaches.

### Model Comparison

Using several model families provides a more reliable evaluation than relying on a single forecasting technique.

---

## 🛠️ Technologies Used

### Programming

- Python

### Data Processing

- Pandas
- NumPy

### Statistical Modeling

- Statsmodels
- Prophet

### Machine Learning

- Scikit-learn
- Random Forest
- XGBoost

### Deep Learning

- TensorFlow
- Keras

### Visualization

- Matplotlib

### Development Environment

- Jupyter Notebook
- Anaconda

---

## 📂 Project Workflow

**1. Raw Saudi Stock Market Data**  
↓  
**2. Data Loading & Inspection**  
↓  
**3. Data Cleaning**  
↓  
**4. Time-Series Preparation**  
↓  
**5. Chronological Train/Test Split**  
↓  
**6. Statistical Modeling — ARIMA, SARIMA, Prophet**  
↓  
**7. Feature Engineering**  
↓  
**8. Machine Learning — Random Forest, XGBoost**  
↓  
**9. Deep Learning — LSTM**  
↓  
**10. Model Evaluation**  
↓  
**11. Performance Comparison**  
↓  
**12. Best Model Selection — LSTM**

---

## ⚠️ Important Notes

This project is intended for **educational, analytical, and portfolio purposes**.

The forecasting results should not be interpreted as financial or investment advice.

Financial markets are affected by many external variables that are not represented in a univariate historical-index forecasting workflow.

Additionally, the available dataset is relatively small, so model results should be interpreted within the scope of this experiment rather than as evidence of production-level forecasting performance.

---

## 🚀 Future Improvements

Potential extensions include:

- Expanding the historical dataset
- Incorporating daily market observations
- Adding trading volume and market indicators
- Including macroeconomic variables
- Hyperparameter optimization
- Walk-forward validation
- Transformer-based forecasting
- Ensemble forecasting
- Model explainability
- Automated forecasting pipelines
- Interactive forecasting dashboard

---

## 👤 Author

**Talal Oudah Alshammari**  
Data Science

[LinkedIn](https://www.linkedin.com/in/talalalasfour)  
[GitHub](https://github.com/talalalasfour)

---

## 🔗 Project Repository

[Saudi Stock Market Time Series Forecasting](https://github.com/talalalasfour/Time-series-forcasting)

---

## ⭐ About This Project

This project demonstrates an end-to-end forecasting workflow combining **statistical modeling, machine learning, and deep learning** for Saudi stock market time-series analysis.

It highlights practical skills in data preprocessing, feature engineering, forecasting, model evaluation, model comparison, and communicating analytical results.
