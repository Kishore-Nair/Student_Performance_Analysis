
# Multidimensional Student Performance Analytics

## A Predictive Framework for Burnout Risk & Academic Trajectories

---

## Executive Summary

This repository presents a dual-engine machine learning framework designed to model academic performance trajectories while simultaneously detecting burnout risk in higher-education students.

The system integrates:

* **Predictive Performance Engine** for continuous regression modeling of a synthesized performance index
* **Risk Stratification Engine** for multi-class classification of burnout risk and early intervention

The models are trained on a multi-factor behavioural dataset of more than 550 students, combining academic, behavioural, and psychological attributes.

This work unifies predictive analytics, explainable AI, and unsupervised learning to deliver actionable and interpretable educational intelligence.

# System Overview

```
Raw Survey Data
      ↓
Data Engineering and Feature Synthesis
      ↓
Regression Engine → Performance Score
Classification Engine → Burnout Risk
      ↓
Interpretability + Clustering + Visualization
      ↓
Actionable Student Archetypes and Feedback
```

---

# Data Engineering Deep Dive

The dataset integrates behavioural, academic, and psychometric signals.

| Category      | Features                                   |
| ------------- | ------------------------------------------ |
| Academic      | Marks, Study Hours, Attendance             |
| Behavioural   | Consistency, Late Submissions              |
| Psychological | Stress, Motivation, Sleep, Physical Health |

## Missing Value Recovery — KNN Imputation (n = 5)

A KNNImputer with five neighbors was used to reconstruct missing values while preserving feature relationships. This approach avoids the bias introduced by mean or median imputation and maintains the local structure of the feature space.

## Stochastic Continuous Mapping (Gaussian Noise Injection)

Several survey variables were discretized into ordinal levels. To improve generalization, Gaussian noise was injected into engineered features:

x_prime = clip(x + Normal(0, 0.05), 0, 1)

This stochastic mapping transforms ordinal bins into quasi-continuous variables, improving model generalization and reducing discretization artifacts.

## Feature Synthesis — Performance Score

A composite academic wellness index was engineered:

Performance_Score = Sleep_Hours + Physical_Health + Study_Hours + Motivation + Attendance - Stress

The score lies within the range [0, 5] and captures both positive and negative contributors to academic outcomes.

---

# Model Architecture and Benchmarking

## Regression Engine — Performance Prediction

| Model                    | RMSE       | R²         |
| ------------------------ | ---------- | ---------- |
| Linear Regression (Best) | **0.2646** | **0.8707** |
| Random Forest Regressor  | 0.3385     | 0.7885     |
| Support Vector Regressor | 0.2908     | 0.8664     |
| Decision Tree Regressor  | 0.4412     | 0.6407     |

The results indicate strong linear structure in the feature space, allowing a parametric model to outperform ensemble methods.

## Classification Engine — Burnout Risk Detection

Pipeline:

* Stratified train/test split
* SMOTE resampling to correct class imbalance
* Hyperparameter-tuned Random Forest classifier

| Metric             | Value    |
| ------------------ | -------- |
| Accuracy           | 0.85     |
| Weighted F1 Score  | **0.86** |
| Recall (High Risk) | 0.75     |

The classifier reliably identifies vulnerable students and minimizes false negatives in high-risk populations.

---

# Interpretability and Visualization

## t-SNE Manifold Learning

High-dimensional student behaviour was projected into two dimensions using t-SNE, revealing distinct behavioural regions and fuzzy class boundaries.

## SHAP Explainability

SHAP analysis provided model transparency and feature attribution.

Key predictors of performance:

* Sleep Hours
* Physical Health
* Attendance
* Motivation

Key predictors of burnout:

* Motivation
* Sleep Hours
* Teacher Support

## Unsupervised Student Archetypes

K-Means clustering revealed three latent student profiles:

| Cluster   | Archetype                 | Description                            |
| --------- | ------------------------- | -------------------------------------- |
| Cluster 0 | Motivated but Stressed    | High effort with elevated burnout risk |
| Cluster 1 | Low Motivation, High Risk | Critical intervention group            |
| Cluster 2 | Balanced and Stable       | Healthy academic behaviour             |

---

# Visual Analytics

The system includes:

* Correlation heatmaps
* Confusion matrices
* SHAP summary plots
* t-SNE embeddings
* Radar profile comparisons

These visual tools transform predictions into human-interpretable insights.

---

# Technology Stack

| Category           | Tools                    |
| ------------------ | ------------------------ |
| Language           | Python                   |
| Machine Learning   | Scikit-Learn             |
| Imbalance Handling | Imbalanced-Learn (SMOTE) |
| Explainability     | SHAP                     |
| Visualization      | Matplotlib, Seaborn      |
| Manifold Learning  | t-SNE                    |
| Clustering         | K-Means, PCA             |

---

# Future Directions

* Integration with LLM-based academic coaching systems
* Real-time burnout monitoring dashboards
* Cross-institution validation and scaling
* Adaptive recommendation engines

---

# Research Impact

This project demonstrates how interpretable machine learning can evolve from prediction into proactive academic intervention, forming a foundation for AI-driven student success platforms.
