<<<<<<< HEAD
# 🗄️ OLAP System with SQLite + Pandas

## 📌 Project Overview

This project demonstrates the design and implementation of a **mini OLAP (Online Analytical Processing) system** using:

* **SQLite** → for relational storage and queries (ROLAP)
* **Pandas (Python)** → for data cube creation and multidimensional aggregation (MOLAP)
* **Hybrid (ROLAP + MOLAP)** → combining relational queries and cube-based aggregation (HOLAP)
* **Seaborn/Matplotlib** → for visualizations

The project applies OLAP techniques on **sales data** structured in a **star schema**. It highlights how businesses can analyze sales trends across multiple dimensions (product, category, date, revenue, quantity).

---

## 🏗️ Schema Design: Star Schema

A **Star Schema** was used, where the **fact table (sales)** connects to **dimension tables (products, dates)**.

### **1. Dimension Tables**

#### `products`

Contains details about products.

| Column     | Type         | Description                                    |
| ---------- | ------------ | ---------------------------------------------- |
| product_id | INTEGER (PK) | Unique identifier for each product             |
| category   | TEXT         | Product category (e.g., Electronics, Clothing) |
| name       | TEXT         | Name of the product                            |
| price      | DECIMAL      | Unit price                                     |

#### `dates`

Stores the date hierarchy for OLAP time analysis.

| Column     | Type      | Description                |
| ---------- | --------- | -------------------------- |
| date       | DATE (PK) | Transaction date           |
| year       | INTEGER   | Year                       |
| quarter    | INTEGER   | Quarter of the year (1–4)  |
| month      | INTEGER   | Month number               |
| month_name | TEXT      | Month name (e.g., January) |

---

### **2. Fact Table**

#### `sales`

Stores measurable facts:

| Column     | Type         | Description                      |
| ---------- | ------------ | -------------------------------- |
| sale_id    | INTEGER (PK) | Unique identifier for each sale  |
| date       | DATE (FK)    | Foreign key to `dates`           |
| product_id | INTEGER (FK) | Foreign key to `products`        |
| quantity   | INTEGER      | Quantity sold                    |
| revenue    | DECIMAL      | Total revenue (quantity × price) |

---

## 🔍 OLAP Architectures Implemented

### **1. ROLAP (Relational OLAP)**

ROLAP queries are executed **directly on SQLite** using SQL queries.

✔️ Examples:

* Average revenue by **product category**
* Total sales by **year**
* Best-selling products in **each category**

---

### **2. MOLAP (Multidimensional OLAP)**

MOLAP was implemented by creating **data cubes using Pandas pivot tables**.

✔️ Examples:

* Revenue cube (**Category × Year**)
* Quantity cube (**Category × Year**)

This allows slicing/dicing quickly without hitting the database again.

---

### **3. HOLAP (Hybrid OLAP)**

HOLAP combines ROLAP + MOLAP:

1. Use **SQL (ROLAP)** to fetch detailed records (e.g., sales for year 2024).
2. Use **Pandas pivot (MOLAP)** to summarize revenue by **Category × Month**.

This gives the efficiency of MOLAP with the flexibility of ROLAP.

---

## 🔄 OLAP Operations Demonstrated

1. **Slice** – Selecting a single dimension value

   * Example: Sales in **2023** only.

2. **Dice** – Filtering by multiple dimensions

   * Example: Sales in **2023** for **Electronics** only.

3. **Roll-Up** – Aggregating data into higher levels of hierarchy

   * Example: From **Product → Category → Year**.

4. **Drill-Down** – Breaking down data into finer levels of detail

   * Example: From **Year → Quarter → Month**.

---

## 📊 Visualizations

To complement the analysis, Seaborn/Matplotlib were used to generate:

1. **Bar Plot** → Average revenue by product category
   <img width="859" height="547" alt="image" src="https://github.com/user-attachments/assets/6b3146c0-93c4-4587-81c2-7bf4cf5bb53d" />

2. **Heatmap** → Revenue cube (**Category × Year**)
   <img width="675" height="547" alt="image" src="https://github.com/user-attachments/assets/a5cce025-2a6c-49b6-a41b-9c70a58228ca" />

3. **Line Plot** → Total revenue trends by year
   <img width="876" height="547" alt="image" src="https://github.com/user-attachments/assets/ccfbd494-6387-40aa-8f87-228cba83b067" />


These visualizations help to quickly identify:

* Which categories generate the most revenue
* Seasonal/yearly revenue trends
* Category-level comparisons

---

## 🚀 How to Run the Project

### **1. Clone the Repository**

```bash
git clone https://github.com/your-username/DSA2040A_OLAP_Assignment.git
cd DSA2040A_OLAP_Assignment
```

### **2. Install Dependencies**

```bash
pip install pandas numpy matplotlib seaborn
```

> **Note:** `sqlite3` is part of Python’s standard library, no extra installation needed.

### **3. Run the Script**

```bash
python olap_system.py
```

### **4. Expected Output**

* Console will display ROLAP, MOLAP, HOLAP results.
* Visualizations will pop up showing bar charts, line plots, and heatmaps.

---

## ✨ Key Learnings

* **ROLAP** is best for large-scale relational queries but slower for aggregations.
* **MOLAP** provides fast multidimensional analysis with pre-aggregated cubes.
* **HOLAP** combines the strengths of both, making it a flexible hybrid solution.
* OLAP operations (Slice, Dice, Roll-up, Drill-down) help businesses analyze sales across multiple perspectives.
=======
# 🧠 DSA 2040A – ETL Pipeline Project  
---

## 1️⃣ Project Overview  

This project demonstrates the **ETL (Extract, Transform, Load)** process using a synthetic student exam dataset.  
The main goal was to design a working data pipeline that takes raw exam records and processes them into clean, validated, and enriched data ready for storage or analysis.  

The project is split into two main Jupyter notebooks:
- `etl_extract.ipynb` – Generates and validates raw data  
- `etl_transform.ipynb` – Cleans, enriches, and standardizes the data  

By the end of the workflow, two clean CSV files (`transformed_full.csv` and `transformed_incremental.csv`) are produced — representing ready-to-analyze student performance data.

---

## 2️⃣ Data Source  

**Dataset:** Synthetic student exam records generated using Python’s [`Faker`](https://faker.readthedocs.io/en/master/) library.  

**Description:**  
The dataset simulates real-world student exam data, containing details such as:
- Student demographics (ID, gender, age, region)  
- Academic info (subject, grade level, school)  
- Performance metrics (exam score, date, and pass/fail outcome)  

**Files generated:**  
| File | Description |
|------|--------------|
| `raw_data.csv` | Main dataset containing 8,000 records |
| `incremental_data.csv` | Additional 1,000 records simulating new incoming data |
| `validated_full.csv` | Cleaned + validated merged dataset |
| `validated_incremental.csv` | Cleaned incremental data for testing transformations |

📁 **Location:** `/data` folder inside the main project directory.  

---

## 3️⃣ ET Phases  

### **🔹 Extract Phase**
Notebook: `etl_extract.ipynb`  
**Goal:** Generate, validate, and prepare raw exam data for transformation.  

**Key Steps:**
1. Generated random but realistic data using the `Faker` library.  
2. Created separate `raw` and `incremental` datasets.  
3. Validated data structure — checked column data types, missing values, and duplicates.  
4. Saved validated data into the `/data` folder.  

**Outputs:**
- `validated_full.csv`  
- `validated_incremental.csv`

---

### **🔹 Transform Phase**
Notebook: `etl_transform.ipynb`  
**Goal:** Clean, standardize, and enrich the validated data for analytics.  

**Key Transformations:**
| Step | Transformation | Description |
|------|----------------|-------------|
| 1 | Handle Missing Values | Filled missing regions/schools with "Unknown". |
| 2 | Standardize Text | Converted text fields (gender, subject, region) to Title Case. |
| 3 | Data Type Conversion | Changed `exam_date` to a proper datetime format. |
| 4 | Derived Column | Added `score_status` = Pass/Fail based on score threshold (≥ 50). |
| 5 | Categorization | Binned `exam_score` into Low, Average, Good, Excellent. |
| 6 | Drop Irrelevant Columns | Removed `name` for privacy and minimalism. |

**Outputs:**
- `/transformed/transformed_full.csv`  
- `/transformed/transformed_incremental.csv`

---

## 4️⃣ Tools Used  

| Tool / Library | Purpose |
|----------------|----------|
| **Python 3.13** | Programming language used for data pipeline |
| **Pandas** | Data manipulation and cleaning |
| **NumPy** | Numerical operations |
| **Faker** | Synthetic data generation |
| **Jupyter Notebook** | Interactive environment for coding and documentation |


---

## 5️⃣ Steps to Run the Project  

### **Prerequisites**
Ensure you have the following installed:
- Python 3.10 or later  
- Jupyter Notebook or VS Code with Jupyter extension  
- Required libraries:
  ```bash
  pip install pandas numpy faker matplotlib
>>>>>>> 91f466ff8a06d7a4ce2dc030c55288e4562352a9
