# Faculty Scheduling: Predicting Staffing Preferences

## Overview

This project analyzes historical scheduling data from the University of Texas anesthesiology department to predict faculty staffing preferences. Using machine learning techniques, I developed models to answer three key questions:

1. **Staffing Type Preferences** - Does each faculty member prefer working with CRNAs only, residents only, or mixed teams?
2. **Team Size Preferences** - Do faculty prefer small (1-2), medium (3-4), or large (5+) teams?
3. **Specific Staff Preferences** - Which individual CRNAs does each faculty member prefer to work with?

## Key Findings

- Faculty preferences are **intrinsic and stable** - they don't change based on day of week or other external factors
- Historical faculty patterns are the strongest predictors of future staffing choices
- Staffing type and team size can be predicted with **91% accuracy**
- CRNA pairings can be predicted with **83% sensitivity** using class weighting techniques

## Data

- **2,924** shift records spanning August 2024 - August 2025
- **53** unique faculty members
- **160+** CRNAs and residents
- Features include temporal variables, faculty characteristics, and binary staffing indicators

### Class Imbalance Challenge

The data is highly imbalanced:
- CRNA Only: 57%
- Resident Only: 36%
- Mixed: 7%

This imbalance required special techniques (class weights, threshold tuning) to achieve meaningful predictions.

## Methods

### Exploratory Data Analysis
- Staffing type distribution analysis
- Faculty preference heatmaps
- Temporal pattern analysis
- Correlation analysis (room count vs team size: r = 0.76)

### Hypothesis Testing
- Chi-square test: Staffing type vs weekday (p = 0.779, not significant)
- Chi-square test: Staffing type vs faculty (p < 0.001, significant)
- Pearson correlation: Room count vs team size (r = 0.76, p < 0.001)
- T-test: Holiday vs non-holiday team sizes (p = 0.758, not significant)

### Feature Engineering
- Historical faculty preference rates (CRNA-only rate, mixed rate, resident-only rate)
- Historical average team sizes
- Team size categories (Small, Medium, Large)
- Temporal features (weekday, holiday indicator)

### Models

**Model 1: Staffing Type Classification**
| Model | Accuracy | Kappa |
|-------|----------|-------|
| Logistic Regression | 90.9% | 0.76 |
| LDA | 90.9% | 0.76 |
| SVM | 90.9% | 0.76 |
| Baseline | 74.3% | 0.00 |

**Model 2: Team Size Classification**
| Model | Accuracy | Kappa |
|-------|----------|-------|
| Logistic Regression | 91.9% | 0.80 |
| LDA | 91.9% | 0.80 |
| SVM | 91.9% | 0.80 |
| Baseline | 70.8% | 0.00 |

**Model 3: CRNA Pairing Prediction**
| Model | Accuracy | Sensitivity |
|-------|----------|-------------|
| Ridge Regression (with class weights) | 39.9% | 82.7% |
| SVM (with class weights) | 67.5% | 61.2% |
| Baseline | 95.9% | 0% |

## Recommendations

Based on this analysis, I recommend schedulers:

1. **Use historical preferences as the primary guide** - Past behavior strongly predicts future choices
2. **Identify faculty with strong preferences** - Most faculty clearly prefer either CRNA-only or resident-only teams
3. **Use CRNA pairing predictions as suggestions** - The model identifies likely working relationships to inform assignments

## Limitations

- Rare classes (Mixed staffing at 7%, Large teams at <1%) cannot be reliably predicted
- Some scheduling factors may not be captured in the data (case complexity, patient needs)
- Models may need retraining as staff turnover occurs
