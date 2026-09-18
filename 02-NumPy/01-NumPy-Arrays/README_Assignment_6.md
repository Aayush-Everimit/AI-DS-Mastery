# Assignment 6 - NumPy Fundamentals: Customer Churn Numerical Analyzer

## Status
**Completed**

This is the first half of the NumPy section. It covers NumPy arrays, indexing, aggregation, Boolean masking, `np.where()`, vectorized operations, and basic broadcasting.

## Dataset
**E-commerce Customer Churn**

File:
`data_ecommerce_customer_churn.csv`

## Folder Structure
```text
02-NumPy/
└── 01-NumPy-Arrays/
    ├── a6_CustomerChurnNumericalAnalyzer.ipynb
    ├── README.md
    └── data/
        └── data_ecommerce_customer_churn.csv
```

## Objective
Build a numerical analysis workflow using NumPy while understanding the operations underneath higher-level data-science libraries.

Core restrictions: no Pandas, scikit-learn, or Seaborn. Python's built-in `csv` module may be used for loading.

## Numerical Features
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

## Topics Completed

### 1. Dataset inspection and preparation
- Load CSV using `csv.DictReader`
- Identify numerical features and target
- Detect missing numerical values
- Exclude rows with missing numerical values before constructing `X`

### 2. NumPy arrays
Created:
```python
X  # numerical feature matrix
y  # churn target
```
Practiced `shape`, `ndim`, `size`, and `dtype`.

### 3. Indexing and slicing
Practiced:
```python
X[0]
X[:5]
X[0][:3]
X[0, :3]
X[:, 0]
X[-5:]
X[0, 0]
```

Important distinction:
```text
X[:, 0] -> all rows, first column
X[:][0] -> first row
```

### 4. Aggregation
Practiced:
```python
np.mean()
np.median()
np.min()
np.max()
np.std()
```
and:
```python
np.mean(X, axis=0)
np.mean(X, axis=1)
```

Key rule:
```text
axis=0 -> reduce rows -> one result per column
axis=1 -> reduce columns -> one result per row
```

### 5. Boolean masking
Practiced conditions and combined masks using:
```python
&
|
~
```
Example:
```python
mask = (satisfaction <= 2) & (complain == 1)
```

### 6. `np.where()`
Practiced:
```python
np.where(condition, value_if_true, value_if_false)
```
for low-satisfaction, inactive, and complaint flags.

Key distinction:
```text
Boolean mask -> select rows
np.where()   -> create/transform values
```

### 7. Vectorized operations
Created numerical features without Python-level loops, including:
```python
engagement_score = tenure + devices + addresses - days_since_order
```
Also practiced conditional calculations such as cashback per tenure.

### 8. Basic broadcasting
Calculated:
```python
feature_means = np.mean(X, axis=0)
X_centered = X - feature_means
```
and verified that centered column means are approximately zero.

## What I Should Be Able to Explain
1. What an `ndarray` is.
2. `shape`, `ndim`, `size`, and `dtype`.
3. The difference between `X[0]`, `X[:, 0]`, and `X[:][0]`.
4. `axis=0` versus `axis=1`.
5. Boolean masks.
6. `and` versus `&` for NumPy conditions.
7. Masking versus `np.where()`.
8. Vectorization.
9. Why vectorized numerical operations are useful.
10. Broadcasting.

# Independent Exam / Task

## Customer Behavior Screening Engine

Build a new NumPy-only analysis from scratch. Do not copy the assignment solution. You may use the same churn dataset.

### 1. High-value customers
Find customers satisfying:
```text
CashbackAmount > 250
AND
Tenure > 10
```
Return the Boolean mask, count, and matching rows.

### 2. At-risk customers
Define at-risk as:
```text
SatisfactionScore <= 2
AND
DaySinceLastOrder > 10
```
Create the Boolean mask, an `np.where()` flag (`1` at-risk, `0` otherwise), and the count.

### 3. Engagement score
Create:
```text
Engagement =
Tenure
+ NumberOfDeviceRegistered
+ NumberOfAddress
- DaySinceLastOrder
```
Use vectorized NumPy operations. Report mean, minimum, maximum, and standard deviation.

### 4. Feature centering
Calculate each feature mean and create `X_centered` using broadcasting. Verify centered column means are approximately zero.

### 5. Business summary
Print:
```text
Total customers analyzed
High-value customers
At-risk customers
Average engagement score
Highest engagement score
Lowest engagement score
```

## Exam Rules
- No Pandas
- No scikit-learn
- No ChatGPT-generated solution
- No loops for numerical calculations
- NumPy should be used wherever appropriate
- Documentation lookup for forgotten syntax is allowed

## Evaluation
Check:
- Correct indexing and slicing
- Correct axis interpretation
- Correct Boolean conditions
- Correct `np.where()`
- Correct vectorization
- Correct broadcasting
- Clean implementation and meaningful variable names
- Ability to explain the implementation

## Completion Standard
Assignment 6 is mastered when the implementation can be reproduced independently and the underlying NumPy concepts can be explained without relying on memorized code.

# Assignment 7 - Remaining NumPy

The next assignment will cover the remaining NumPy topics:

- Feature normalization / standardization
- Churn analysis
- Churned vs non-churned feature comparisons
- Numerical risk scoring
- Risk-group analysis
- NumPy performance benchmarking
- Python loops vs vectorization
- Memory/performance reasoning
- Final analytical report
- NumPy concept exam

Progression:
```text
Assignment 6 -> NumPy fundamentals
Assignment 7  -> NumPy analytical application + performance
Assignment 8+ -> More independent vectorized problem solving
```
