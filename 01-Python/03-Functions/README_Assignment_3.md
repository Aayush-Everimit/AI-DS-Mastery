# Assignment 3: Student Performance Analyzer

## Overview

A Python-based student performance analysis system designed to practice
function design, reusable logic, validation, data cleaning, statistical
calculations, filtering, grading, and function composition.

The assignment was completed using core Python without Pandas or NumPy.

## Problem

Given a collection of student records containing:

- Name
- Age
- Marks

the system validates and cleans student data, performs statistical analysis,
filters students based on marks, assigns grades, and generates an overall
performance summary.

## Concepts Practiced

- Python functions
- Function parameters and return values
- Function composition
- Input validation
- Type checking with `type()` and `isinstance()`
- Type conversion
- Lists and dictionaries
- Conditional logic
- Iteration
- Data cleaning
- Statistical calculations
- Sorting
- Edge-case handling
- Reusable function design

## Implemented Functions

### Validation

```python
validate_name(name)
validate_age(age)
validate_marks(marks)
```

These functions validate student attributes based on their expected types
and value ranges.

### Data Cleaning

```python
clean_student(student)
```

Responsible for validating and converting student information into the
expected representation.

The cleaning process handles:

- Empty values
- Type conversion
- Name normalization
- Age validation
- Marks validation

### Statistical Analysis

```python
calculate_average(students)
find_highest_marks(students)
find_lowest_marks(students)
calculate_median(students)
```

The statistical functions calculate:

- Average marks
- Highest marks
- Lowest marks
- Median marks

The median is implemented manually by extracting and sorting the marks
rather than using a statistics library.

### Filtering

```python
filter_students(students, min_marks)
```

Returns students whose marks meet or exceed a specified minimum threshold.

### Grade Assignment

```python
assign_grade(marks)
```

Assigns a grade based on the student's marks.

The grading scheme used is:

| Marks | Grade |
|---:|:---|
| 90–100 | A |
| 80–89 | B |
| 70–79 | C |
| 60–69 | D |
| Below 60 | E |

### Summary Generation

```python
summary(students, passing_marks=40)
```

Combines the previously implemented functions to produce an overall
student-performance summary.

The summary includes:

- Number of students
- Average marks
- Highest marks
- Lowest marks
- Median marks
- Number passed
- Number failed
- Grade distribution

## Example Input

```python
students = [
    {"name": "Aman", "age": 20, "marks": 78},
    {"name": "Riya", "age": 19, "marks": 91},
    {"name": "Karan", "age": 21, "marks": 64},
    {"name": "Neha", "age": 20, "marks": 85},
]
```

## Complexity

### Average, Highest, Lowest, and Filtering

Each uses a single pass through the student records.

**Time:** `O(n)`

### Median

The marks are extracted in `O(n)` and then sorted.

**Time:** `O(n log n)`

**Space:** `O(n)` for the marks list.

## Key Learnings

- Functions should have a clear responsibility.
- Parameters allow reusable logic to operate on different inputs.
- Return values allow functions to be composed into larger workflows.
- Validation and data cleaning are related but distinct responsibilities.
- Type checking can be performed using `type()` and `isinstance()`.
- Statistical calculations can be implemented directly using core Python.
- Edge cases such as empty input should be considered.
- Function design includes deciding what a function should return, not just
  what it should calculate.

## Areas Identified for Improvement

During review, the following areas were identified for future improvement:

- Use consistent return types from functions.
- Separate validation and cleaning more clearly.
- Handle failed type conversions with explicit exception handling.
- Avoid mutating the original student dictionary when cleaning data.
- Improve validation of empty or whitespace-only names.
- Simplify the return value of `assign_grade()` to return only the grade.

These limitations are documented as part of the learning process.

## Constraints

The assignment was implemented using core Python.

### Not used

- Pandas
- NumPy
- `statistics`
- `collections.Counter`

## Status

**Completed**

### Skills Demonstrated

- [x] Function definition
- [x] Parameters and return values
- [x] Function composition
- [x] Input validation
- [x] Type checking
- [x] Type conversion
- [x] Data cleaning
- [x] List and dictionary manipulation
- [x] Statistical calculations
- [x] Filtering
- [x] Sorting
- [x] Grade assignment
- [x] Summary generation
- [x] Basic complexity analysis
