# Assignment 4: Customer Support Ticket Analyzer

## Overview

This assignment focuses on using Python's core data structures to analyze and efficiently access customer support ticket data.

The main goal was to understand when and why to use **lists, sets, and dictionaries**, while also developing an understanding of **time and space complexity**.

The assignment was completed using only core Python. No Pandas, NumPy, Counter, or external libraries were used for the analysis.

## Dataset

**Customer Support Ticket Dataset**

The dataset contains **8,469 customer support tickets** with information such as:

- Ticket ID
- Customer Name
- Customer Email
- Customer Age
- Customer Gender
- Product Purchased
- Date of Purchase
- Ticket Type
- Ticket Subject
- Ticket Description
- Ticket Status
- Resolution
- Ticket Priority
- Ticket Channel
- First Response Time
- Time to Resolution
- Customer Satisfaction Rating

The CSV was loaded using Python's built-in `csv.DictReader`.

## Assignment Objectives

1. Basic dataset exploration
2. Searching through records
3. Frequency counting
4. Duplicate detection
5. Grouping tickets by customer
6. Building a fast ticket lookup
7. Finding top-K ticket types
8. Understanding time and space complexity
9. Choosing appropriate data structures for different operations

## Implementation

### Part 1: Basic Exploration

Implemented functions to find:

- Total number of tickets
- Unique ticket types
- Unique ticket statuses
- Unique priorities
- Unique products

A **set** was used for unique values because it automatically removes duplicates.

**Results:**
- Total tickets: **8,469**
- Unique ticket types: **5**
- Unique statuses: **3**
- Unique priorities: **4**
- Unique products: **42**

### Part 2: Searching

Implemented:

- `find_tickets_by_customer()`
- `find_tickets_by_product()`

These functions traverse the original list and return all matching ticket records.

**Results:**
- Tickets for `Marisa Obrien`: **1**
- Tickets for `GoPro Hero`: **228**
- Nonexistent searches return an empty list.

**Time complexity:** `O(n)`

### Part 3: Frequency Counting

Implemented frequency counting for:

- Ticket types
- Ticket statuses
- Ticket priorities
- Products

Dictionaries were used to maintain a:

```text
category → frequency
```

mapping.

**Ticket Type frequencies:**

| Ticket Type | Count |
|---|---:|
| Refund request | 1752 |
| Technical issue | 1747 |
| Cancellation request | 1695 |
| Product inquiry | 1641 |
| Billing inquiry | 1634 |

**Status frequencies:**

| Status | Count |
|---|---:|
| Pending Customer Response | 2881 |
| Open | 2819 |
| Closed | 2769 |

**Priority frequencies:**

| Priority | Count |
|---|---:|
| Medium | 2192 |
| Critical | 2129 |
| High | 2085 |
| Low | 2063 |

### Part 4: Duplicate Detection

Implemented:

```python
find_duplicate_ticket_ids(rows)
```

A set tracks IDs already encountered, while another set stores IDs that appear more than once.

**Result:** 0 duplicate Ticket IDs.

**Time complexity:** `O(n)` expected

### Part 5: Customer Grouping

Implemented:

```python
group_tickets_by_customer(rows)
```

The data is grouped as:

```text
customer → list of tickets
```

Example:

```python
{
    "Customer A": [ticket1, ticket2],
    "Customer B": [ticket3]
}
```

Also implemented:

```python
find_customers_with_multiple_tickets(customer_tickets)
```

**Results:**
- Unique customers: **8,028**
- Customers with multiple tickets: **372**

**Overall grouping complexity:** `O(n)` expected

### Part 6: Fast Ticket Lookup

Implemented:

```python
build_ticket_lookup(rows)
get_ticket_by_id(ticket_lookup, ticket_id)
```

A dictionary creates a:

```text
Ticket ID → Ticket
```

mapping.

**Building the lookup:** `O(n)`

**Dictionary lookup:** `O(1)` average

This demonstrates how preprocessing can make repeated lookups significantly faster.

### Part 7: Top-K Ticket Types

Implemented:

```python
top_k_ticket_types(rows, k)
```

The function counts ticket types, sorts the frequency pairs, and returns the top `k` results.

For `k = 3`:

```text
Refund request: 1752
Technical issue: 1747
Cancellation request: 1695
```

**Time complexity:** `O(n + k_unique log k_unique)`

where `k_unique` is the number of unique ticket types being sorted.

### Part 8: Complexity Analysis

The assignment also examined how the operations scale with the size of the dataset.

## Data Structure Choices

| Requirement | Data Structure | Reason |
|---|---|---|
| Store all ticket records | List | Sequential collection of records |
| Find unique values | Set | Automatically removes duplicates |
| Count frequencies | Dictionary | Maps category to frequency |
| Detect duplicate IDs | Set | Fast membership checking |
| Group customer → tickets | Dictionary + List | Direct customer lookup with multiple tickets |
| Ticket ID → ticket lookup | Dictionary | Fast average `O(1)` lookup |

## Complexity Summary

| Operation | Complexity |
|---|---|
| Searching original list | `O(n)` |
| Frequency counting | `O(n)` |
| Finding unique values | `O(n)` expected |
| Duplicate detection | `O(n)` expected |
| Customer grouping | `O(n)` expected |
| Building ticket lookup | `O(n)` |
| Ticket dictionary lookup | `O(1)` average |
| Top-K sorting | `O(n + k_unique log k_unique)` |

## Key Learnings

### Data structures should match the operation

```text
Need uniqueness       → Set
Need key → value      → Dictionary
Need ordered records   → List
Need repeated lookup   → Dictionary / Set
```

### Preprocessing can improve repeated operations

Searching the original list for a ticket requires `O(n)` time.

Building a dictionary first costs `O(n)`, but subsequent ticket ID lookups are `O(1)` average.

### Big-O describes scaling

An `O(n)` operation may be reasonable for a small dataset but becomes increasingly expensive as the number of records grows. With millions of records, runtime and memory usage become important considerations.

## Technologies

- Python
- Built-in `csv` module
- Lists
- Sets
- Dictionaries
- Basic algorithmic complexity analysis

## Files

```text
04-Customer-Support-Ticket-Analyzer/
├── a4_CustomerSupportTicketAnalyzer.ipynb
└── README.md
```

The notebook contains the complete implementation, tests, and final results.

## Status

**Assignment 4: Complete**

This assignment is part of the **AI & Data Science Mastery** journey, progressing from Python fundamentals toward NumPy, Pandas, SQL, Statistics, Machine Learning, and Generative AI.
