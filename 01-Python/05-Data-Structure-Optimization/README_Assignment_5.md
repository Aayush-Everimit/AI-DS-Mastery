# Assignment 5 - Transaction Data Optimizer

## Overview

This assignment focuses on applying Python data structures and algorithmic thinking to transaction data.

The goal is to efficiently analyze transaction records using core Python structures such as:

- Lists
- Sets
- Dictionaries
- Tuples

The assignment covers grouping, frequency analysis, duplicate detection, aggregation, lookup optimization, and complexity analysis.

## Dataset

The assignment uses the **PaySim Synthetic Financial Dataset**.

The dataset contains transaction records with fields including:

- `step`
- `type`
- `amount`
- `nameOrig`
- `oldbalanceOrg`
- `newbalanceOrig`
- `nameDest`
- `oldbalanceDest`
- `newbalanceDest`
- `isFraud`
- `isFlaggedFraud`

For development and testing, the notebook processes the first **1,000 transactions** rather than the full multi-million-row dataset.

## Objectives

1. Find unique transaction types
2. Group transactions by origin account
3. Find accounts with multiple transactions
4. Count transactions by type
5. Find the most common transaction type
6. Detect duplicate transactions
7. Calculate spending by origin account
8. Find top-K spending accounts
9. Count fraudulent transactions by type
10. Find fraudulent accounts
11. Build a fast account lookup structure
12. Retrieve transactions for a specific account
13. Analyze time and space complexity
14. Test edge cases and validate consistency

## Implementation

### 1. Dataset Loading

The dataset is loaded with Python's built-in `csv` module and `csv.DictReader`.

A 1,000-record limit is used during development to keep experimentation fast.

### 2. Unique Transaction Types

A `set` is used to store transaction types and automatically eliminate duplicates.

Example:

```text
{'PAYMENT', 'TRANSFER', 'CASH_OUT', 'DEBIT', 'CASH_IN'}
```

**Complexity:** `O(n)` average time, `O(k)` space.

### 3. Group Transactions by Origin Account

Transactions are grouped into:

```text
nameOrig -> list of transactions
```

Conceptually:

```text
{
    "C123": [transaction1, transaction2],
    "C456": [transaction3]
}
```

**Complexity:** `O(n)` average time, `O(n)` space.

### 4. Accounts with Multiple Transactions

The grouped transaction lists are checked for length greater than one.

**Complexity:** `O(a)` time, where `a` is the number of unique origin accounts.

### 5. Transaction Frequency by Type

A dictionary maps:

```text
transaction_type -> frequency
```

For the 1,000-record sample:

```text
PAYMENT: 437
TRANSFER: 99
CASH_OUT: 230
DEBIT: 51
CASH_IN: 183
```

The frequencies correctly sum to **1,000**.

**Complexity:** `O(n)` average time, `O(k)` space.

### 6. Most Common Transaction Type

The frequency dictionary is sorted by frequency in descending order.

For the sample:

```text
PAYMENT
```

was the most common transaction type with **437 transactions**.

**Complexity:** `O(n + k log k)`.

### 7. Duplicate Transaction Detection

A composite transaction key is created from:

```text
(step, type, amount, nameOrig, nameDest)
```

The tuple is stored in a set. If the same key appears again, it is recorded as a duplicate.

**Data structures:**

- `tuple` for the composite key
- `set` for tracking previously seen keys

**Complexity:** `O(n)` average time, `O(n)` space.

### 8. Origin Account Spending

Transaction amounts are converted to floating-point values and aggregated by origin account:

```text
nameOrig -> total spending
```

**Complexity:** `O(n)` average time, `O(a)` space.

### 9. Top-K Spending Accounts

The account spending dictionary is sorted by total spending in descending order and the first `k` accounts are returned.

**Complexity:** `O(n + a log a)`.

### 10. Fraud Analysis by Transaction Type

The existing `isFraud` dataset label is used to count fraudulent transactions by transaction type.

This is **label analysis, not a fraud detection model**.

**Complexity:** `O(n)` average time.

### 11. Fraudulent Accounts

A set stores the origin accounts associated with transactions where:

```text
isFraud == 1
```

Using a set ensures that each account is represented only once.

**Complexity:** `O(n)` average time, `O(f)` space.

### 12. Fast Account Lookup

A dictionary index is built:

```text
nameOrig -> list of transactions
```

This allows repeated account queries without scanning the entire transaction list.

```python
account_lookup.get(account_id, [])
```

**Complexity:**

- Building lookup: `O(n)`
- Average account lookup: `O(1)`
- Processing `k` returned transactions: `O(k)`

## Testing

A complete testing section was added to the notebook.

Tests cover:

- Dataset loading
- Expected transaction types
- Grouping
- Multiple-transaction accounts
- Frequency totals
- Most common transaction type
- Duplicate detection
- Spending aggregation
- Top-K ordering
- Fraud analysis
- Account lookup
- Non-existent account lookup
- Lookup consistency
- Empty inputs
- `k = 0`
- `k = 1`
- Large `k`

### Testing Results

Using the first 1,000 transactions:

```text
Transactions: 1000
Unique transaction types: 5
Unique origin accounts: 1000
Accounts with multiple transactions: 0
Duplicate transaction keys: 0
Fraudulent accounts: 0
Lookup accounts: 1000
```

The transaction frequency total matched the dataset size:

```text
1000
```

The account lookup was also verified against the grouped account structure.

## Data Structure Decisions

| Requirement | Data Structure | Reason |
|---|---|---|
| Unique transaction types | Set | Removes duplicates |
| Transaction frequency | Dictionary | Fast key-based counting |
| Group by account | Dictionary + List | One account can have many transactions |
| Duplicate detection | Set | Fast membership checking |
| Composite transaction identity | Tuple | Natural immutable composite key |
| Account spending | Dictionary | Maps account to accumulated value |
| Fraudulent accounts | Set | Stores each account once |
| Account lookup | Dictionary + List | Fast repeated account retrieval |

## Complexity Summary

| Operation | Time Complexity |
|---|---:|
| Unique transaction types | `O(n)` average |
| Group by origin account | `O(n)` average |
| Find multiple-transaction accounts | `O(a)` |
| Count by transaction type | `O(n)` average |
| Most common type | `O(n + k log k)` |
| Duplicate detection | `O(n)` average |
| Calculate account spending | `O(n)` average |
| Top-K spending accounts | `O(n + a log a)` |
| Fraud count by type | `O(n)` average |
| Fraudulent accounts | `O(n)` average |
| Build account lookup | `O(n)` average |
| Account lookup | `O(1)` average |

Where:

- `n` = number of transactions
- `a` = number of unique origin accounts
- `k` = number of unique transaction types

## Scaling to Millions of Transactions

The original PaySim dataset contains millions of records, while this assignment uses only 1,000 records during development.

Precomputed dictionaries such as:

```text
nameOrig -> transactions
```

make repeated account queries much faster than repeatedly scanning the full dataset.

However, storing millions of Python dictionaries and lists in memory can be expensive. At larger scale, alternatives include:

- Database indexing
- SQL aggregation
- Chunked processing
- Streaming
- Distributed processing
- Columnar storage
- Analytical databases

The main lesson is that both **runtime efficiency and memory usage** matter as data volume increases.

## Key Learnings

This assignment strengthened practical understanding of:

- Python sets and dictionaries
- Nested data structures
- Composite keys
- Frequency counting
- Grouping
- Aggregation
- Duplicate detection
- Lookup optimization
- Preprocessing versus repeated scanning
- Time complexity
- Space complexity
- Edge-case testing
- Working with large datasets

The central takeaway is that choosing the right data structure can substantially improve repeated operations.

## Files

```text
05-Transaction-Data-Optimizer/
├── a5_TransactionDataOptimizer.ipynb
├── README.md
└── data/
    └── Synthetic_Financial_datasets_log.csv
```

> Note: The full PaySim dataset is large. The notebook currently processes only a limited sample for development and testing.

## Status

**Assignment 5: Complete** ✅

Implementation, testing, edge-case checks, data-structure analysis, and complexity analysis have been completed.
