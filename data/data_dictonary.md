# 📘 Data Dictionary: Retail Analytics Project

## 1. Overview
* **Dataset Source:** [Online Retail II UCI Machine Learning Repository](https://archive.ics.uci.edu/ml/datasets/Online+Retail+II)
* **Domain:** E-Commerce / Retail
* **Time Period:** 01/12/2009 - 09/12/2011
* **Description:** This dataset contains all the transactions occurring for a UK-based and registered, non-store online retail. The company mainly sells unique all-occasion gift-ware.

---

## 2. Data Model Schema (Star Schema)
The raw data has been transformed into a Star Schema to optimize performance in Power BI.

### 🟧 Fact Table: `Fact_Sales`
*Contains granular transactional records.*

| Field | Data Type | Description | Example |
| :--- | :--- | :--- | :--- |
| **InvoiceNo** | Text | Unique 6-digit number assigned to each transaction. If it starts with 'C', it indicates a cancellation. | `536365`, `C536379` |
| **StockCode** | Text | Product (item) code. Unique 5-digit number. | `85123A` |
| **CustomerID** | Text | Unique 5-digit integer assigned to each customer. | `17850` |
| **InvoiceDate** | Date/Time | The day and time when a transaction was generated. | `2010-12-01 08:26:00` |
| **Quantity** | Whole Number | The number of products per transaction. | `6`, `12` |
| **UnitPrice** | Decimal | Product price per unit in Sterling (£). | `2.55` |
| **TotalSales** | Decimal | **[Calculated Column]** Revenue generated per line item. Formula: `Quantity * UnitPrice` | `15.30` |

### 🟦 Dimension: `Dim_Customer`
*Contains unique customer attributes.*

| Field | Data Type | Description |
| :--- | :--- | :--- |
| **CustomerID** | Text | Primary Key. Links to `Fact_Sales`. |
| **Country** | Text | The name of the country where the customer resides. |
| **R_Score** | Whole Number | **[Calculated]** Recency Score (1-5) based on days since last purchase. |
| **F_Score** | Whole Number | **[Calculated]** Frequency Score (1-5) based on number of transactions. |
| **M_Score** | Whole Number | **[Calculated]** Monetary Score (1-5) based on total spend. |
| **Segment** | Text | **[Calculated]** Final grouping (e.g., "Champions", "At Risk") based on RFM scores. |

### 🟦 Dimension: `Dim_Product`
*Contains unique product attributes.*

| Field | Data Type | Description |
| :--- | :--- | :--- |
| **StockCode** | Text | Primary Key. Links to `Fact_Sales`. |
| **Description** | Text | Product Name. |
| **ABC_Class** | Text | **[Calculated]** Pareto classification (A=Top 20% Revenue, B=Middle, C=Bottom). |

---

## 3. Data Cleaning & Assumptions (ETL Log)
Before analysis, the following cleaning steps were applied in Power Query:

1.  **Handling Nulls:** Rows with missing `CustomerID` were removed as they cannot be used for customer segmentation.
2.  **Exclusions:**
    * Removed cancelled transactions (where `InvoiceNo` starts with 'C').
    * Removed non-product codes: `POSTAGE`, `D` (Discount), `M` (Manual), `BANK CHARGES`.
3.  **Data Quality:**
    * Filtered out records with `Quantity <= 0` or `UnitPrice <= 0`.
    * Unified description strings (uppercased) to avoid duplication due to case sensitivity.

---

## 4. Business Metrics Definitions

### RFM Analysis
Used to segment customers based on purchasing behavior:
* **Recency:** Days since the last valid purchase.
* **Frequency:** Count of unique `InvoiceNo` per customer.
* **Monetary:** Sum of `TotalSales`.

### ABC Analysis (Pareto Principle)
Used for inventory and sales strategy:
* **Class A:** Products contributing to the top **70%** of cumulative revenue.
* **Class B:** Products contributing to the next **20%** of cumulative revenue.
* **Class C:** Products contributing to the final **10%** of cumulative revenue.