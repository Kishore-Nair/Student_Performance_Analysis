# Advanced Multidimensional Student Performance Analytics

### *Predictive Modeling, Burnout Risk Stratification, and Behavioral Clustering*

## Project Overview

This project engineering a comprehensive analytical framework to evaluate and predict student academic trajectories. By leveraging a dataset of **550+ students**, the system moves beyond simple grade tracking to analyze the symbiotic relationship between physiological factors (sleep, health), psychological indicators (stress, motivation), and academic outcomes.

The architecture features a dual-engine approach: a **High-Precision Regressor** for performance forecasting and a **Robust Classifier** for proactive burnout detection.

---

## Technical Architecture & Methodology

### 1. Advanced Data Engineering Pipeline

* 
**KNN-Based Imputation**: Implemented `KNNImputer` (n=5) for sophisticated missing value recovery, ensuring the integrity of the 'Age' feature space compared to simple mean/median methods.


* 
**Feature Synthesis & Normalization**: Engineered a composite `Performance_Score` by aggregating multi-source signals (Marks, Attendance, Sleep, Health, and Motivation) through `MinMaxScaler` and `StandardScaler` transformations .


* 
**Stochastic Continuous Mapping**: Added Gaussian noise to discrete health and motivation scores to enhance model generalization and prevent overfitting on sparse distributions .



### 2. High-Dimensional Visualization & EDA

* 
**Manifold Learning**: Utilized **t-SNE (t-distributed Stochastic Neighbor Embedding)** to project high-dimensional student data into 2D space, revealing distinct clusters and "fuzzy" boundaries between performance labels .


* 
**Feature Interconnectivity**: Executed a detailed Pearson Correlation analysis, identifying a strong negative correlation between **Stress Score** and **Performance Score**.



---

## Performance Metrics & Model Benchmarking

The project utilizes a multi-model ensemble to ensure predictive reliability.

### Performance Prediction (Regression)

We benchmarked several architectures, with **Random Forest** emerging as the superior model due to its ability to capture non-linear student behaviors.

| Model | RMSE (Lower is Better) |  Score | Key Parameters |
| --- | --- | --- | --- |
| **Random Forest (Optimized)** | <br>**0.1029** 

 | <br>**0.8101** 

 | <br>`max_depth: 10`, `n_estimators: 200` 

 |
| **Support Vector Regressor** | 0.3175 

 | 0.8408 

 | <br>`kernel: rbf`, `C: 100` 

 |
| **Linear Regression** | 0.3246 

 | 0.8336 

 | Baseline |

### Burnout Risk Detection (Classification)

To address class imbalance in student burnout, we integrated **SMOTE (Synthetic Minority Over-sampling Technique)**.

* 
**Accuracy**: **85.11%** 


* 
**Macro F1-Score**: **0.81** (SVC implementation) 


* 
**Feature Importance**: `Motivation` and `Late_submissions` were identified via **SHAP (SHapley Additive exPlanations)** as the primary drivers of burnout risk.



---

## Unsupervised Behavioral Clustering

Using **K-Means Clustering** coupled with **Principal Component Analysis (PCA)**, students were segmented into three distinct behavioral archetypes:

1. 
**Motivated but Stressed**: High engagement but rising burnout signals.


2. 
**Low Motivation, High Risk**: Critical intervention required.


3. 
**Balanced and Stable**: Optimal performance-wellbeing equilibrium.



---

## 💻 Tech Stack

* **Core**: Python, Pandas, NumPy
* **ML Frameworks**: Scikit-Learn, Imbalanced-learn (SMOTE)
* **Explainable AI (XAI)**: SHAP
* **Visualization**: Seaborn, Matplotlib, Plotly (Radar/Spider Charts)
* **Deployment**: Joblib (Model Serialization)

---
