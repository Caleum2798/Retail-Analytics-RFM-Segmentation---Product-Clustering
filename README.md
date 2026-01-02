# Retail Analytics: RFM Segmentation & Product Clustering

![Status](https://img.shields.io/badge/Status-Completed-success)
![Tools](https://img.shields.io/badge/Tools-PowerBI%20|%20DAX%20|%20PowerQuery-blue)

## 📊 Project Overview
This project involves an end-to-end analysis of online retail transaction data to identify customer segments and optimize product strategy. By implementing **RFM Analysis** (Recency, Frequency, Monetary) and **Pareto Analysis (ABC)**, this dashboard provides actionable insights to improve customer retention and maximize revenue.

> **Live Demo:** [Link to NovyPro or PDF Report Here]

## 🎯 Business Problems Solved
The dashboard addresses critical business questions:
1.  **Customer Segmentation:** Who are the VIP clients, and which ones are at risk of churning?
2.  **Product Performance:** Which products contribute to 80% of the revenue (Pareto Principle)?
3.  **Sales Trends:** How are sales performing over time across different regions?

## 🛠️ Tech Stack & Methodology
* **Data Cleaning (ETL):** Used Power Query to clean raw transactional data (handling missing values, negative quantities, and data typing).
* **Data Modeling:** Designed a **Star Schema** connecting a central Fact table (Transactions) with Dimension tables (Customers, Products, Calendar).
* **Advanced DAX:**
    * **RFM Segmentation:** Calculated R, F, and M scores dynamically to categorize customers into segments like "Champions", "Loyal", and "At Risk".
    * **ABC Analysis:** Implemented dynamic ranking to classify products into Class A (Top 20%), B, and C based on revenue contribution.

## 📈 Key Insights & Visuals

### 1. Customer RFM Segmentation
*Analyzed customer behavior to target marketing efforts.*
*(Place a screenshot of your RFM page here)*
* **Insight:** "Champions" account for X% of total revenue despite being only Y% of the customer base.

### 2. Product ABC Analysis
*Applied the 80/20 rule to inventory and sales.*
*(Place a screenshot of your Product Analysis page here)*
* **Insight:** Top 15 products generate 50% of the total revenue.

## 📂 Project Structure
```text
├── assets/
│   ├── dashboard_overview.png
│   └── rfm_logic.png
├── data/
│   └── data_dictionary.md
├── docs/
│   └── specific_insights.pdf
├── README.md
└── Retail_Analytics_Dashboard.pbix (or link to download)