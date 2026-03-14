# 🛒 Zepto E-Commerce SQL Data Analysis Project--(LEARNING PROJECT)

A complete, real-world **data analyst portfolio project** built on an e-commerce inventory dataset scraped from [Zepto](https://www.zeptonow.com/) — one of India's fastest-growing quick-commerce startups. This project simulates end-to-end analyst workflows: from raw data ingestion and exploratory analysis to business-driven SQL insights.

> 💼 Perfect for data analyst aspirants building a strong portfolio 

---

## 📌 Table of Contents

- [Project Overview](#-project-overview)
- [Dataset Overview](#-dataset-overview)
- [Project Workflow](#-project-workflow)
- [Business Insights](#-business-insights)
- [Tech Stack](#-tech-stack)
- [How to Use](#-how-to-use)
- [License](#-license)

---

## 📊 Project Overview

This project simulates how real data analysts work behind the scenes in e-commerce and retail. Using SQL on a PostgreSQL database, we:

- ✅ Set up a messy, real-world e-commerce inventory database
- ✅ Perform **Exploratory Data Analysis (EDA)** to understand product categories, availability, and pricing inconsistencies
- ✅ Implement **Data Cleaning** to handle null values, remove invalid entries, and convert pricing from paise to rupees
- ✅ Write **business-driven SQL queries** to derive insights around pricing, inventory, stock availability, revenue, and more

---

## 📁 Dataset Overview

The dataset was sourced from **Kaggle** and originally scraped from Zepto's official product listings — it closely mirrors what you'd encounter in a real-world e-commerce inventory system.

Each row represents a unique **SKU (Stock Keeping Unit)**. Duplicate product names exist intentionally, since the same product may appear multiple times across different package sizes, weights, discounts, or categories — exactly how real catalog data looks.

### 🧾 Columns

| Column | Description |
|---|---|
| `sku_id` | Unique identifier for each product entry (Synthetic Primary Key) |
| `name` | Product name as it appears on the app |
| `category` | Product category (e.g. Fruits, Snacks, Beverages) |
| `mrp` | Maximum Retail Price — originally in paise, converted to ₹ |
| `discountPercent` | Discount applied on MRP |
| `discountedSellingPrice` | Final price after discount — also converted to ₹ |
| `availableQuantity` | Units available in inventory |
| `weightInGms` | Product weight in grams |
| `outOfStock` | Boolean flag indicating stock availability |
| `quantity` | Number of units per package (mixed with grams for loose produce) |

---

## 🔧 Project Workflow

### 1. Database & Table Creation

```sql
CREATE TABLE zepto (
  sku_id                SERIAL PRIMARY KEY,
  category              VARCHAR(120),
  name                  VARCHAR(150) NOT NULL,
  mrp                   NUMERIC(8,2),
  discountPercent       NUMERIC(5,2),
  availableQuantity     INTEGER,
  discountedSellingPrice NUMERIC(8,2),
  weightInGms           INTEGER,
  outOfStock            BOOLEAN,
  quantity              INTEGER
);
```

### 2. Data Import

Loaded via pgAdmin's import feature. If unavailable, use:

```sql
\copy zepto(category, name, mrp, discountPercent, availableQuantity,
            discountedSellingPrice, weightInGms, outOfStock, quantity)
FROM 'data/zepto_v2.csv'
WITH (FORMAT csv, HEADER true, DELIMITER ',', QUOTE '"', ENCODING 'UTF8');
```

> ⚠️ If you encounter UTF-8 encoding errors, re-save the CSV as **CSV UTF-8** format before importing.

### 3. 🔍 Exploratory Data Analysis

- Counted total records in the dataset
- Viewed sample data to understand structure and content
- Checked for null values across all columns
- Identified distinct product categories
- Compared in-stock vs. out-of-stock product counts
- Detected products with multiple SKUs (different sizes, packaging, etc.)

### 4. 🧹 Data Cleaning

- Identified and removed rows where MRP or discounted selling price was zero
- Converted `mrp` and `discountedSellingPrice` from **paise → rupees** for consistency

---

## 📈 Business Insights

| # | Analysis |
|---|---|
| 1 | Top 10 best-value products by discount percentage |
| 2 | High-MRP products currently out of stock |
| 3 | Estimated potential revenue per product category |
| 4 | Expensive products (MRP > ₹500) with minimal discount |
| 5 | Top 5 categories offering highest average discounts |
| 6 | Price per gram to identify value-for-money products |
| 7 | Product segmentation by weight (Low / Medium / Bulk) |
| 8 | Total inventory weight per product category |

---

## 🛠️ Tech Stack

- **PostgreSQL** — Relational database
- **pgAdmin** — GUI client for database management
- **SQL** — Querying, cleaning, and analysis

---

## 🚀 How to Use

1. **Clone the repository**
   ```bash
   git clone https://github.com/amlanmohanty/zepto-SQL-data-analysis-project.git
   cd zepto-SQL-data-analysis-project
   ```

2. **Open `zepto_SQL_data_analysis.sql`**  
   This single file contains table creation, data exploration, data cleaning, and all business analysis queries.

3. **Load the dataset into pgAdmin** (or any PostgreSQL client)
   - Create a new database
   - Run the SQL file
   - Import `zepto_v2.csv` (convert to UTF-8 encoding if necessary)

---

## 📜 License

[MIT](LICENSE) — free to fork, star ⭐, and use in your own portfolio.

---

*Built to simulate real analyst workflows in e-commerce — from messy raw data to actionable business insights.*
