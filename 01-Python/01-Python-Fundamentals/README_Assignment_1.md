# Assignment 1: Python Data Processing

## Overview

A hands-on Python assignment focused on loading and processing structured CSV data using core Python, without Pandas or NumPy.

The assignment was designed to build the foundation for later data-science workflows by working directly with Python lists, dictionaries, CSV files, data cleaning, and type conversion.

## Concepts Practiced

- Python functions
- Lists and dictionaries
- CSV file handling
- `csv.DictReader`
- `csv.reader`
- Data cleaning
- Type conversion
- String normalization
- Dictionary-based record representation
- Basic dataset inspection
- Date parsing

## Part 1: Student Record Processing

A student performance CSV dataset was loaded and converted into Python dictionaries.

### Implemented

- Loaded CSV data using `csv.DictReader`
- Converted CSV rows into Python dictionaries
- Inspected dataset records, keys, and values
- Cleaned selected fields
- Converted numerical fields from strings to integers
- Normalized string fields

### Fields Processed

```text
school
sex
age
address
studytime
failures
absences
passed
```

### Example transformation

Raw CSV values:

```python
{
    "age": "18",
    "studytime": "2",
    "failures": "0",
    "absences": "6"
}
```

After cleaning:

```python
{
    "age": 18,
    "studytime": 2,
    "failures": 0,
    "absences": 6
}
```

String fields were stripped, while `passed` was normalized to lowercase.

## Part 2: Order Data Processing

A second CSV structure was used to practice the same concepts on a different dataset.

### Implemented

- CSV loading
- Dictionary/list based record processing
- Numerical type conversion
- Date parsing
- String cleaning and normalization

### Fields Processed

```text
id
order_date
ship_mode
customer_id
sales
```

### Type conversions

```text
id           → int
order_date   → datetime.date
ship_mode    → normalized string
customer_id  → cleaned string
sales        → float
```

## Constraints

The assignment was completed using core Python and did not use:

- Pandas
- NumPy
- Polars

The purpose was to understand the underlying mechanics of structured-data processing before moving to specialized data-science libraries.

## Key Learnings

- CSV values are initially read as strings.
- `csv.DictReader` provides convenient column-name based access.
- Real-world datasets may differ from an expected toy schema.
- Data cleaning involves both string normalization and type conversion.
- Lists and dictionaries are sufficient for basic structured-data processing.
- Understanding the underlying operations makes later Pandas workflows easier to reason about.

## Status

**Completed**

### Skills Demonstrated

- [x] CSV loading
- [x] `csv.DictReader`
- [x] Lists and dictionaries
- [x] Data cleaning
- [x] Type conversion
- [x] Date parsing
- [x] String normalization
- [x] Basic dataset inspection
- [x] Processing structured data without Pandas
