# Assignment 7 — NumPy Customer Churn Analysis & Performance

## Overview

This assignment extends the NumPy fundamentals from Assignment 6 into practical numerical analysis and performance testing.

The goal was to use **NumPy to analyze customer churn, create a rule-based customer risk score, compare churn behavior across risk groups, and understand the performance benefits of vectorized operations over Python loops.**

This assignment was completed as a guided learning/revision exercise before moving toward fully independent implementations.

---

## Folder Structure

```text
02-NumPy/
└── 02-NumPy-Analysis-Performance/
    ├── a7_CustomerChurnAnalysisPerformance.ipynb
    ├── README.md
    └── data/
        └── data_ecommerce_customer_churn.csv
```

## Dataset

**Dataset:** E-commerce Customer Churn

The dataset contains customer-level information from an e-commerce business, including:

- Tenure
- WarehouseToHome
- NumberOfDeviceRegistered
- PreferedOrderCat
- SatisfactionScore
- MaritalStatus
- NumberOfAddress
- Complain
- DaySinceLastOrder
- CashbackAmount
- Churn

The numerical analysis uses:

```text
Tenure
WarehouseToHome
NumberOfDeviceRegistered
SatisfactionScore
NumberOfAddress
Complain
DaySinceLastOrder
CashbackAmount
```

Target:

```text
Churn
```

## Objectives

1. Feature standardization
2. Churn analysis
3. Comparing churned vs non-churned customers
4. Rule-based customer risk scoring
5. Risk-group analysis
6. NumPy vectorization
7. Python loop vs NumPy performance comparison
8. Interpreting numerical results
9. Reinforcing important NumPy concepts

## Feature Standardization

Standardized the numerical feature matrix using:

```python
X_scaled = (X - feature_means) / feature_std
```

with feature-wise means and standard deviations calculated using NumPy.

The standardized data was checked to verify that each feature had approximately:

```text
Mean ≈ 0
Standard deviation ≈ 1
```

This demonstrated NumPy broadcasting without explicit Python loops.

## Churn Analysis

Calculated:

- Total customers
- Churned customers
- Non-churned customers
- Overall churn rate
- Feature means for churned customers
- Feature means for non-churned customers
- Difference between the two groups

The churn rate was calculated using:

```python
churn_rate = np.mean(y == 1)
```

These comparisons were treated as descriptive analysis, not causal conclusions.

## Rule-Based Risk Scoring

A customer risk score was created using:

| Condition | Score |
|---|---:|
| SatisfactionScore ≤ 2 | +2 |
| Complain = 1 | +2 |
| DaySinceLastOrder > 10 | +2 |
| Tenure < 5 | +1 |
| NumberOfAddress ≤ 1 | +1 |

The maximum possible score is 8.

The score was calculated using NumPy operations and `np.where()`.

## Risk Groups

Customers were categorized as:

```text
0–2  → Low
3–4  → Medium
5+   → High
```

For each group, the analysis calculated:

- Customer count
- Churned customer count
- Churn rate

This demonstrated how NumPy Boolean masks can be combined for business analysis.

## Performance Comparison

A performance experiment used **1,000,000 random values**.

The same calculation was implemented with:

### Python loop

```python
x**2 + 2*x + 5
```

### NumPy vectorization

```python
values**2 + 2*values + 5
```

Execution time was measured for both implementations and the speedup was calculated:

```python
speedup = loop_time / numpy_time
```

The results were also validated using:

```python
np.allclose(result_loop, result_numpy)
```

This demonstrated the practical performance advantage of vectorized numerical operations.

## Key NumPy Concepts Practiced

### Standardization

```python
(X - mean) / std
```

### Axis-based aggregation

```python
np.mean(X, axis=0)
```

### Boolean masking

```python
X[y == 1]
```

### Conditional transformation

```python
np.where(condition, value_if_true, value_if_false)
```

### Broadcasting

Applying a 1D feature vector across all rows of a 2D matrix.

### Vectorization

Performing operations over entire arrays without explicit Python iteration.

### Performance validation

```python
np.allclose(...)
```

## Learning Outcomes

After completing this assignment, I can:

- Standardize numerical features using NumPy
- Calculate churn rates using Boolean arrays
- Compare numerical characteristics of customer groups
- Build rule-based scoring systems
- Create categorical groups from numerical scores
- Perform grouped analysis using Boolean masks
- Use NumPy vectorized arithmetic
- Measure Python vs NumPy execution time
- Explain why vectorized operations are generally faster
- Understand broadcasting in practical numerical operations
- Validate equivalent numerical implementations

## Learning Note

This notebook is intentionally a **learning/revision notebook**, rather than a polished production implementation.

Assignments 1–5 established Python fundamentals and data-structure problem solving. Assignment 6 introduced NumPy arrays, indexing, aggregation, masking, `np.where()`, vectorization, and broadcasting. Assignment 7 extends those concepts into numerical analysis and performance.

The following assignments will increasingly require independent implementation rather than guided reconstruction.

## Technologies

- Python
- NumPy
- CSV
- Jupyter Notebook
- `time`

No Pandas or Scikit-learn was used for the core NumPy exercises.

## Status

**Completed**

Assignment 7 — NumPy Customer Churn Analysis & Performance
