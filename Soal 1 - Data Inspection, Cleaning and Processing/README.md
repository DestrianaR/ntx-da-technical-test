# Soal 1 – Data Inspection, Cleaning and Processing

---

## Background

**PT Sinar Niaga Nusantara** is a fictional Indonesian retailer selling electronics and office supplies (laptops, smartphones, accessories, networking gear, printers, and office equipment) through two channels: **offline stores** handled by sales representatives, and an **online** channel handled by the system.

Ahead of the upcoming management sales review, the Sales Operations team exported the raw order-line transactions from the transaction system into a single CSV file. The export has not been reviewed by anyone. You have just joined the analytics team, and you are asked to make this data **trustworthy and analysis-ready** before the analysis team uses it for revenue, margin, and performance reporting.

You are not expected to know how the data was produced. Inspect it, decide what is wrong, decide how to treat it, and **explain your reasoning** as you would to a colleague who inherits your work.

## Objective

This challenge assesses your ability to:

- **Inspect** an unfamiliar dataset and find quality problems systematically
- **Clean** the data with justified, reproducible decisions
- **Process** the data into a form that is ready for analysis
- **Communicate** assumptions, trade-offs, and open questions

## Dataset Overview

| Item     | Detail                       |
| -------- | ---------------------------- |
| File     | `sales_transactions_raw.csv` |
| Grain    | One row = one order line     |
| Size     | ~7,300 rows × 15 columns     |
| Period   | September 2024 – August 2026 |
| Currency | Indonesian Rupiah (IDR)      |

### Data Dictionary

| Column          | Description                                        | Expected Type                                      |
| --------------- | -------------------------------------------------- | -------------------------------------------------- |
| `order_id`      | Order identifier                                   | string                                             |
| `order_date`    | Date the order was placed                          | date                                               |
| `region`        | Region of the sale                                 | string                                             |
| `channel`       | Sales channel (Online / Offline)                   | string                                             |
| `customer_id`   | Customer identifier                                | string                                             |
| `customer_type` | Customer segment (Retail, UMKM, Korporat)          | string                                             |
| `sales_rep`     | Sales representative code                          | string                                             |
| `category`      | Product category                                   | string                                             |
| `product`       | Product name                                       | string                                             |
| `qty`           | Quantity ordered                                   | integer                                            |
| `discount`      | Discount applied to the line                       | float, fraction between 0 and 1 (e.g. `0.05` = 5%) |
| `status`        | Order status: `Completed`, `Cancelled`, `Returned` | string                                             |
| `unit_price`    | List price per unit (IDR)                          | float                                              |
| `revenue`       | Line revenue after discount (IDR)                  | float                                              |
| `cost`          | Cost of goods sold for the line (IDR)              | float                                              |

### Business Rules You May Assume

- `revenue = qty × unit_price × (1 − discount)`
- `gross profit = revenue − cost`
- Each product has a single list price for the whole period.
- `Cancelled` orders never generated sales.
- `Returned` lines are recorded as separate return records that offset an earlier sale.
- Online orders are processed by the system, not by an individual sales representative.
- Any other assumption you make must be **stated explicitly** in your notebook.

> The dataset comes straight from the source system. Do not assume it is clean.

## Tasks

Complete all tasks in a single Python notebook (`pandas` is expected; other libraries are welcome).

### Task 1 – Data Inspection

1. Give an overview of the dataset: shape, data types, missing values, memory footprint, and basic statistics.
2. Check each column for problems in format, consistency, validity, and plausibility. Include the checks that involve more than one column (e.g. consistency between fields, business rules above).
3. Check for duplicated records and for records that should not be part of a real sales analysis.

### Task 2 – Data Cleaning

1. Apply a treatment for each issue listed in Task 1: standardise, fix, impute, flag, or remove.
2. Justify each decision: why fix vs. drop vs. flag? What assumption did you rely on? What is the risk if that assumption is wrong?
3. Keep an **audit trail**: the number of rows and the total revenue before and after each cleaning step, so every change is traceable (You can use log or just simple print statemnt)
4. Do not silently delete data. Anything removed or altered in a non-trivial way must be reported (and, where sensible, kept in a separate reject/quarantine table).
5. The notebook must be re-runnable from top to bottom, starting from the raw file, without manual edits.

### Task 3 – Data Processing

1. Create analysis-ready fields, for example:
   - Date parts (year, month, quarter, year-month)
   - Net revenue and gross profit that correctly handle returns
   - Gross margin (%)
2. Produce the following summary tables from the cleaned data:
   - Monthly net revenue, gross profit, and margin %
   - Net revenue and margin by `region` × `category`
   - Top 10 customers by net revenue

## Deliverables

You will present your work in a **Jupyter Notebook** (or an equivalent environment). Ensure your submission includes the following:

- **Detailed Documentation**
  - Explain your thought process at each stage.

- **Data Processing & Analysis**
  - Show data preprocessing steps (cleaning, transformation, aggregation).
  - Implement anomaly detection and discuss findings.

- **Final Insights & Recommendations**
  - Summarize key findings on top products, anomalies, and profitable locations.
  - Provide recommendations for the client based on the analysis.

## Evaluation Criteria

We evaluate your submission on the following aspects :

| Criteria                               | What we look for                                                                              |
| -------------------------------------- | --------------------------------------------------------------------------------------------- |
| Inspection thoroughness                | Systematic checks, including cross-column and business-rule checks; issues backed by evidence |
| Cleaning correctness and justification | Right treatment for each issue, explicit assumptions, no unjustified data loss                |
| Processing and feature quality         | Correct metrics (especially returns), useful summaries                                        |
| Code quality and reproducibility       | Readable, modular, re-runnable, sensible use of pandas                                        |
| Communication                          | Clear narrative, concise documentation, honest about uncertainty                              |

### What makes a strong submission

- Finds a wide range of data quality issues, including subtle ones that only show up when checking several columns together or against the business rules.
- Backs every issue with evidence (counts, examples) instead of just stating it.
- Chooses a treatment for each issue (fix, flag, or remove) and explains why, including the assumption behind it and the risk if that assumption is wrong.
- Keeps an audit trail of rows and revenue before and after each step, and reports what was removed or changed.
- Handles returns and cancelled orders correctly in revenue and profit.
- Uses a notebook that runs top to bottom from the raw file, with clean, commented code.
- Explains the thought process clearly, states assumptions, and raises open questions honestly.
- Ends with insights and recommendations that are grounded in the cleaned data.
