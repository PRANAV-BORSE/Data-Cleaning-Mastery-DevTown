# Data-Cleaning-Mastery-DevTown

# Data Cleaning Mastery Bootcamp - Final Project

Organized by **DevTown** in collaboration with **Microsoft Student Chapter (MSC)** & **Google Developers Group (GDG)**.

## Project Overview
This project focuses on identifying, handling, and cleaning real-world data quality issues present in an uncleaned e-commerce sales dataset (`Messy_data.csv`). The final objective is to prepare a consistent, reliable dataset ready for exploratory data analysis and downstream machine learning tasks.

---

## Data Quality Issues & Cleaning Strategy

| Data Quality Issue | Observed Examples | Resolution Method |
| :--- | :--- | :--- |
| **Duplicates** | 5 duplicate rows | Identified with `.duplicated()` and dropped with `.drop_duplicates()`. |
| **Extra Whitespace** | Leading/trailing spaces across text columns | Stripped using `.str.strip()`. |
| **Text Standardization** | `delhi`, `DELHI`, `pUnE`, `completed `, `SHIPPED` | Normalized using `.str.title()` for consistent case across `City` and `OrderStatus`. |
| **Data Type Inconsistencies** | `"three"`, `"2 pcs"`, `"18,500"`, `"forty"`, `"29 years"` | Mapped text representations to numeric digits, removed commas, and converted columns using `pd.to_numeric(..., errors='coerce')`. |
| **Invalid & Mixed Dates** | Mixed formats (`YYYY-MM-DD`, `DD/MM/YYYY`) and string `'not a date'` | Converted with `pd.to_datetime(format='mixed', errors='coerce')` and imputed missing timestamps via forward fill. |
| **Outliers & Anomalies** | Negative quantity (`-3.0`), extreme bulk values (`500.0`), unrealistic ages | Replaced values outside valid domains with `NaN` and imputed with median values. |
| **Missing Values** | Nulls in `CustomerName`, `City`, `UnitPrice`, `Quantity`, `CustomerAge` | Numeric values imputed with median (or group-level median); text columns filled with mode or sensible defaults (`Unknown Customer`). |
| **Feature Engineering** | Missing derived sales value | Created `TotalAmount = Quantity * UnitPrice` rounded to 2 decimal places. |

---

## Repository Structure
```text
├── Messy_data.csv                       # Raw source dataset
├── cleaned_sales_dataset.csv            # Cleaned, standardized export
├── Data_Cleaning_Mastery_Project.ipynb  # End-to-end Python cleaning pipeline in Google Colab
└── README.md                            # Project documentation and summary
