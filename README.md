![logo_ironhack_blue 7](https://user-images.githubusercontent.com/23629340/40541063-a07a0a8a-601a-11e8-91b5-2f13e4e6b441.png)

# Lab | Indexing, Combining and Aggregation in pandas

## Overview

This lab focuses on combining datasets, reshaping tables, and computing grouped summaries in pandas. You will work with a realistic dataset of course enrollments and scores, then use merges, groupby, and pivot operations to build analysis-ready views. The emphasis is on getting the shape right and validating that your results match the underlying data.

## Learning Goals

By the end of the lab, you should be able to merge DataFrames on keys, reshape data between long and wide forms, compute grouped statistics, and validate aggregation results with simple checks.

## Setup and Context

You will use the CSV dataset included in this repository: `data_safe_copy.csv`. Each row represents a student's score in a module assignment. The fields are `student_id`, `cohort`, `module`, `assignment`, and `score`. The dataset is intentionally long-form so you can practice reshaping and aggregation. Work in a notebook named `m1-07-indexing-aggregation-lab.ipynb`.

## Requirements

- Fork this repository to your own GitHub account.
- Clone your fork to your machine.
- Use the included CSV file `data_safe_copy.csv` from the lab repository.
- Make sure you can open and run Jupyter notebooks (for example via Jupyter Lab or VS Code).

## Getting Started

- Create a new notebook and name it `m1-07-indexing-aggregation-lab.ipynb`.
- Confirm you can successfully load `data_safe_copy.csv` before moving on to merges/pivots.
- Before you submit, restart your kernel and run the notebook **top to bottom**.

## Tasks

### Task 1: Load and inspect the dataset

Load `data_safe_copy.csv` into a DataFrame named `scores`. Confirm the row count is at least 300 and print the first five rows. Run `info()` and verify that `score` is numeric.

### Task 2: Build a student roster table and merge

Create a small DataFrame named `roster` with columns `student_id` and `status`, where `status` is either `"active"` or `"inactive"`. Include at least 10 student IDs that are not present in the scores dataset. Merge `scores` with `roster` using a left join so all score rows remain. Confirm that missing statuses exist after the merge and count them.

### Task 3: Aggregate by module and cohort

Compute the average score by `cohort` and `module` using `groupby`. Store the result in a DataFrame named `avg_by_module`. Then compute the overall average score by `cohort` only and compare the values to ensure the module-level averages roll up as expected.

### Task 4: Reshape to a wide report

Create a wide table where rows are `student_id`, columns are `module`, and values are the average score per student per module. Use `pivot_table` with `mean` as the aggregation. Store the result in `student_module_report`.

Validate that the number of rows equals the number of unique students in the original dataset and that the column labels match the set of module names.

### Task 5: Ranking and top performers

For each cohort, identify the top 3 students by overall average score. Use groupby plus sorting or rank logic. Store the results in a DataFrame named `top_students` with columns `student_id`, `cohort`, and `avg_score`.

Add a check that each cohort appears exactly three times in `top_students`.

## Common Pitfalls and Debugging Notes

A common mistake is joining on the wrong key or using the wrong join type. If you see an unexpected drop in rows, re-check the merge settings. Another frequent issue is mixing long and wide formats. Make sure you know when you are working with one row per record versus one row per student.

When reshaping, verify that your pivot table uses the intended aggregation. If you see duplicate rows or unexpected missing values, check whether your index and columns are defined correctly.

## Submission

### What to submit

Submit the following files:
- The notebook file `m1-07-indexing-aggregation-lab.ipynb`

### Definition of done (checklist)

Before you submit, make sure:

- [ ] The notebook runs **top to bottom** without errors after a kernel restart.
- [ ] You validated row counts and dtypes on load (including `score` as numeric).
- [ ] Your merge preserves score rows (left join) and you counted missing statuses.
- [ ] Your grouped summaries and pivot table have the expected shapes/labels and include validation checks.
- [ ] `top_students` contains exactly 3 students per cohort (and you checked it).
- [ ] The notebook is saved and included in your git commit.

### How to submit (Git workflow)

- When you’re done, make sure all changes are saved, then run:

```bash
git add .
git commit -m "Solved m1-07 lab"
git push -u origin HEAD
```

- Make a pull request.
- Paste the link to your pull request in the Student Portal.

## Evaluation Criteria

Your work will be evaluated on correctness, clarity, and structure. Correctness means your merges, reshapes, and aggregations match the intended logic and your validation checks pass. Clarity means your code is readable and variable names are descriptive. Structure means the notebook runs cleanly from top to bottom with each task completed in order and with visible outputs.
