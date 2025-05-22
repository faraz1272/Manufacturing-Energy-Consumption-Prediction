# Manufacturing Energy Consumption Prediction

## 📋 Project Overview

This project focuses on predicting energy consumption in manufacturing equipment using sensor data from a multi-zone factory environment. The dataset includes environmental measurements from 9 distinct zones, external weather conditions, and energy consumption metrics to build predictive models for optimizing energy usage.

## 🎯 Objective

Develop machine learning models to predict `equipment_energy_consumption` (measured in Wh) based on:
- Multi-zone temperature and humidity readings
- External weather conditions
- Historical energy consumption patterns
- Temporal features (time of day, day of week, month)

## 📊 Dataset Description

### Target Variable
- **equipment_energy_consumption**: Energy consumption of manufacturing equipment (Wh)
- Range: 10-1080 Wh with right-skewed distribution

### Features Overview
- **Time Information**: Timestamp-based features (hour, day, month, day of week)
- **Zone Measurements**: Temperature and humidity from 9 factory zones
- **Weather Data**: Outdoor temperature, humidity, pressure, wind speed, visibility, dew point
- **Energy Metrics**: Lighting energy consumption
- **Engineered Features**: Statistical aggregations, lag features, rolling statistics

### Factory Zones
1. **Zone 1**: Main Production Area
2. **Zone 2**: Assembly Line
3. **Zone 3**: Quality Control
4. **Zone 4**: Packaging Area
5. **Zone 5**: Raw Material Storage
6. **Zone 6**: Loading Bay
7. **Zone 7**: Office Space
8. **Zone 8**: Control Room
9. **Zone 9**: Staff Area

## 🔧 Data Preprocessing

### Data Cleaning
- ✅ Removed negative values in energy and humidity measurements (sensor errors)
- ✅ Handled missing values using median imputation
- ✅ Converted timestamp to datetime format
- ✅ Removed duplicate entries
- ✅ Statistical significance testing for random variables (removed non-significant features)

### Feature Engineering
- **Temporal Features**: Extracted hour, day, month, day of week from timestamps
- **Aggregated Zone Features**: Mean temperature/humidity, standard deviation, ranges
- **Weather Interactions**: Temperature-humidity interactions
- **Lag Features**: 1-hour lag for energy consumption
- **Rolling Statistics**: 3-hour rolling mean for energy consumption

### Outlier Treatment
- **IQR Method**: Identified outliers using 1.5×IQR rule
- **Clipping**: Applied to features with >10% outliers (lighting_energy, visibility_index)

![image](https://github.com/user-attachments/assets/75af30bd-5c52-4e10-b756-c5109b757d45)

*Figure 1: Distribution of Equipment Energy Consumption*

## 📈 Exploratory Data Analysis

### Key Insights

#### Temporal Patterns
- **Daily**: Energy peaks during afternoon hours (2-4 PM)
- **Weekly**: Higher consumption on weekdays vs weekends
- **Monthly**: Seasonal variations correlate with outdoor temperature

#### Environmental Correlations
- Strong correlation between outdoor temperature and energy consumption
- Zone temperature variations impact overall energy usage
- Humidity patterns show inverse relationship with temperature

![image](https://github.com/user-attachments/assets/5d66ef6a-48d9-4c31-9278-3a808a8b3094)

*Figure 2: Feature Correlation Heatmap*

## 🤖 Model Development

### Models Implemented
1. **Linear Regression** (Baseline)
2. **Ridge Regression** (L2 Regularization)
3. **Polynomial Regression** (Degree 2)
4. **PCA + Linear Regression** (Dimensionality Reduction)
5. **Decision Tree** (Hyperparameter Tuned)
6. **XGBoost** (Gradient Boosting)
7. **Neural Network** (Deep Learning)
8. **Support Vector Regression** (SVR)

### Model Performance Summary

| Model | RMSE | MAE | R² Score |
|-------|------|-----|----------|
| **Linear Regression** | 92.66 | 35.26 | **0.59** |
| **Ridge Regression** | 92.66 | 35.26 | **0.59** |
| **XGBoost (Tuned)** | 94.27 | **34.24** | 0.58 |
| **Neural Network** | 94.47 | 37.12 | 0.58 |
| **SVR** | 98.66 | 35.78 | 0.53 |
| **Decision Tree (Tuned)** | 105.39 | 40.91 | 0.47 |
| **Polynomial Regression** | 103.06 | 43.23 | 0.49 |
| **Linear Regression + PCA** | 120.83 | 47.70 | 0.30 |

![image](https://github.com/user-attachments/assets/0bda2f69-b746-4d6d-994c-a78fe68f964d)

*Figure 5: Model Performance Comparison*

### Best Model: Linear Regression
**Test Set Performance:**
- **RMSE**: 91.68
- **MAE**: 35.72
- **R² Score**: 0.5698

## 🏆 Results & Insights

### Model Selection Rationale
- **Linear Regression** achieved the best balance of performance and interpretability
- **XGBoost** showed the lowest MAE but with higher complexity
- **Neural Network** performed competitively but with longer training time
- **Polynomial features** led to overfitting, reducing generalization

### Feature Importance
Top predictors of energy consumption:
1. Historical energy consumption (lag features)
2. Outdoor temperature
3. Zone temperature variations
4. Time-based features (hour of day)
5. Lighting energy consumption
