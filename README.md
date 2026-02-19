

## 🛒 Zepto HSR Layout – Pricing & Demand Analysis Dataset (6454 Products)

##  Project Overview

This repository contains a **primary dataset and end-to-end data pipeline** designed for analyzing pricing strategy, discount behavior, demand intensity, and competitive signals in the quick-commerce industry.

The dataset was collected from a Zepto dark store serving **HSR Layout, Bangalore** — a high-footfall and digitally mature urban locality that serves as a strong proxy for urban Bangalore consumption patterns.

 **Data Collection Date:** February 17 (Tuesday) 2026
 **Context:** Non-festival, regular weekday
 **Objective:** Build a modeling-ready dataset for pricing, demand, and competitive analysis.

---

#  Repository Structure

```
 zepto-hsr-analysis
│
├── zepto_scraper.py                 # API-based data collection script
├── DDA_Zepto_cleaning.ipynb         # Data cleaning & feature engineering notebook
├── zepto_HSR_cleaned_dataset.xlsx   # Final cleaned dataset
└── README.md
```

---

#  Data Collection

Data was collected using a structured API scraping strategy implemented in:

📄 `zepto_scraper.py` 

###  Key Features of Scraper

* Uses Zepto search API endpoint
* Systematic category-based search queries
* Pagination handling
* Deduplication using `Product Variant ID`
* Structured Excel export
* Store-specific extraction (HSR Layout)

Each row represents a **product variant** available at the dark store at the time of scraping.

---

#  Data Cleaning & Preprocessing

Cleaning and feature engineering were performed in:

 `DDA_Zepto_cleaning.ipynb`

###  Key Cleaning Steps

### 1️⃣ Duplicate Detection

* Rows 6457 onward were exact duplicates of rows 1–6455.
* The second half of the dataset was removed.

### 2️⃣ Image URL Correction

Original paths:

```
cms/product_variant/xxxx.jpeg
```

Converted to:

```
https://cdn.zeptonow.com/cms/product_variant/xxxx.jpeg
```

### 3️⃣ Data Type Standardization

| Column Type | Final Type |
| ----------- | ---------- |
| Pricing     | float64    |
| Quantities  | int64      |
| Ratings     | float64    |
| Flags       | bool       |
| Text        | object     |

### 4️⃣ Missing Value Handling

* `Average Rating` → Filled with 0 (no rating)
* `Total Ratings` → Filled with 0
* `L3 Category` → Dropped (90.76% missing)
* Other text columns retained (realistic retail missingness)

### 5️⃣ Discount Validation

Recalculated:

```
Discount % = ((MRP - Selling Price) / MRP) * 100
```

Validated with ±1% tolerance.
No significant mismatches detected.

### 6️⃣ Consistency Checks

* No duplicate Product Variant IDs
* No stock mismatch (0 quantity with in-stock flag)
* Pricing consistency verified

---

#  Feature Engineering

Two binary classification labels were created.

---

##  High Discount Flag

```
High_Discount_Flag = True if Discount % >= 20
```

Purpose:

* Model promotional intensity
* Identify aggressive discounting

---

##  High Demand Flag

Defined as:

```
Total Ratings > 5000 AND Average Rating >= 4.5
```

Purpose:

* Identify highly popular products
* Model demand intensity

---

#  Dataset Description

Final cleaned dataset:
📄 `zepto_HSR_cleaned_dataset.xlsx`

### Key Features

* Product Name
* Brand
* MRP (₹)
* Selling Price (₹)
* Discount %
* Available Quantity
* Out of Stock
* Average Rating
* Total Ratings
* Primary Category
* Is Sponsored
* Country of Origin
* Manufacturer
* High_Discount_Flag
* High_Demand_Flag

Each row represents one product variant.

---

#  Analytical Use Cases

This dataset supports:

### 1️⃣ Pricing Strategy Analysis

* Category-level discount comparison
* Sponsored vs non-sponsored pricing

### 2️⃣ Demand Modelling

* High-demand classification
* Rating-driven popularity analysis

### 3️⃣ Inventory Risk Assessment

* Stock-out risk modelling
* Demand vs availability patterns

### 4️⃣ Competitive Quick-Commerce Analysis

Competing platforms can use this dataset for:

* Price benchmarking
* Urban demand estimation
* Discount intensity comparison
* Assortment depth evaluation
* Bangalore market intelligence

HSR Layout serves as a strong representative urban consumption zone.

---

#  Tech Stack

* Python
* pandas
* requests
* openpyxl
* NumPy
* Jupyter Notebook

---

#  Ethical & Usage Disclaimer

* Data collected for academic and research purposes.
* No authentication bypass or private endpoints used.
* Scraping conducted with controlled request frequency.
* Intended strictly for analytical and educational use.

---

#  Future Enhancements

* Train/test split modelling pipeline
* Category-level elasticity modelling
* Discount impact regression analysis
* Time-series monitoring across multiple days
* Multi-store comparative benchmarking

---

#  Project Highlights

* Real-world primary dataset
* API-based structured extraction
* Robust cleaning and validation
* Feature engineering for classification
* Business-aligned analytical framing
* Competitive intelligence angle

---

