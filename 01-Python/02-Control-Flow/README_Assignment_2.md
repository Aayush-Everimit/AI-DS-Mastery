# Assignment 2: Transaction Monitoring System

## Overview

A Python-based transaction monitoring exercise using the PaySim-style financial transaction dataset.

The assignment focused on applying Python control flow, loops, conditions, sets, dictionaries, validation, aggregation, and rule-based analysis to transaction data without using Pandas or NumPy.

The dataset contains more than 6 million transaction records and includes transaction types such as `PAYMENT`, `TRANSFER`, `CASH_OUT`, `DEBIT`, and `CASH_IN`.

## Dataset

The dataset used in this assignment contains the following fields:

```text
step
type
amount
nameOrig
oldbalanceOrg
newbalanceOrig
nameDest
oldbalanceDest
newbalanceDest
isFraud
isFlaggedFraud
```

During inspection, the dataset was found to contain:

- Approximately 6 million transaction records
- Multiple transaction types
- Missing/`None`-like values in at least one malformed record

## Workflow

The assignment followed a basic data-processing workflow:

```text
Load
  ↓
Inspect
  ↓
Validate
  ↓
Clean
  ↓
Detect duplicates
  ↓
Detect suspicious transactions
  ↓
Calculate user statistics
  ↓
Generate report
```

## Implemented Components

### 1. Dataset Loading

Implemented:

```python
load_dataset(filename)
```

Uses `csv.DictReader` to load CSV records into a list of dictionaries.

### 2. Dataset Inspection

Implemented:

```python
inspect_transactions(transactions)
```

The inspection includes:

- Number of transactions
- First and last records
- Column names
- First five records
- Unique transaction types

### 3. Transaction Validation

Implemented:

```python
validate_transactions(transaction)
```

Validation checks include:

- Transaction type
- Origin account
- Destination account
- Valid transaction types
- Valid step value
- Valid transaction amount
- Valid origin balances
- Valid destination balances
- Numeric conversion failures

Exceptions such as `ValueError`, `TypeError`, and `KeyError` are handled instead of allowing malformed input to immediately terminate validation.

### 4. Data Cleaning

Implemented:

```python
clean_transaction(transactions)
```

The intended workflow separates valid and invalid transactions and records the reason for invalid records.

Numeric fields are converted to appropriate Python types, while string fields are stripped.

### 5. Duplicate Detection

Implemented:

```python
find_duplicates(transactions)
```

A `set` is used to track previously encountered transaction keys.

The transaction key is based on:

```text
step
type
amount
nameOrig
nameDest
```

This provides expected O(n) average-time duplicate detection.

### 6. Rule-Based Suspicious Transaction Detection

Implemented:

```python
detect_suspicious_transactions(transactions)
```

Rules include:

- Very high transaction amount
- Origin balance inconsistency
- Origin balance being emptied during `TRANSFER` or `CASH_OUT`
- Destination balance inconsistency for relevant transaction types
- A transaction is considered suspicious when multiple conditions are triggered

The dataset's `isFraud` label is not used to generate the suspicious-transaction rules.

### 7. User-Level Statistics

Implemented:

```python
calculate_user_statistics(transactions)
```

Calculates per-origin-account:

- Transaction count
- Total transaction amount
- Average transaction amount

Suspicious transaction counts are added separately using:

```python
add_suspicious_counts(...)
```

### 8. Report Generation

Implemented:

```python
generate_report(...)
```

The report is intended to provide:

- Total records
- Valid records
- Invalid records
- Duplicate transactions
- Total transaction amount
- Average transaction amount
- Highest transaction
- Suspicious transactions
- Suspicious percentage
- Actual fraud count from the dataset
- Flagged fraud count
- Top users by transaction value

## Python Concepts Practiced

- Functions
- `for` loops
- Conditional logic
- `continue`
- Lists
- Dictionaries
- Sets
- Tuples
- Exception handling
- Type conversion
- Aggregation
- Rule-based decision logic
- Basic algorithmic complexity

## Complexity

Most transaction-processing operations are designed around a single pass through the dataset:

```text
Loading                  → O(n)
Validation               → O(n)
Duplicate detection      → O(n) average
Suspicious detection     → O(n)
User aggregation         → O(n) average
```

The overall intended processing complexity is approximately:

```text
O(n)
```

Set/dictionary operations provide expected O(1) average lookup and insertion.

## Important Learning

The assignment highlighted the distinction between two skills:

1. **Implementation:** being able to write the required Python logic when a requirement is given.
2. **Problem decomposition:** independently deciding what should be analyzed and what functions should exist.

This assignment primarily targeted the first skill while beginning to introduce the second.

## Known Limitations

This notebook is a learning exercise rather than production code.

Areas identified for future improvement include:

- More consistent function return types
- Stronger separation between validation and cleaning
- More robust handling of malformed rows
- Streaming/chunked processing for very large CSV files
- More carefully calibrated business thresholds
- More rigorous evaluation of rule-based detection against the fraud label

The dataset contains over 6 million rows, so retaining every record in a Python list is useful for learning but is not the most memory-efficient production approach.

## Status

**Completed**

### Skills Demonstrated

- [x] Load structured CSV data
- [x] Inspect dataset structure
- [x] Validate records
- [x] Handle invalid input
- [x] Apply conditional rules
- [x] Detect duplicates with sets
- [x] Aggregate using dictionaries
- [x] Calculate user-level statistics
- [x] Generate a transaction analysis report
- [x] Reason about O(n) processing
