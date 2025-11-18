# DSA2040A_DataMining_Education_Analysis
<<<<<<< HEAD

## WEEK ONE WORK

### Project Overview
This project analyses student performance and attendance data from a real-world dataset in the education domain.  
Through a structured data-mining workflow, we aim to:

- Clean and transform the raw data  
- Identify trends and patterns in student performance  
- Prepare the dataset for advanced analytics and modelling  

### Dataset Description
**Source:** A dataset from Kaggle containing student records covering attendance behaviour and academic performance.  

**Content:** Each record corresponds to a student and includes features such as:
- Weekly self-study hours  
- Attendance percentage  
- Class participation  
- Total score  
- Letter grade  

**Challenges:**  
The dataset contains inconsistent values and missing data, requiring a strong **ETL (Extract–Transform–Load)** approach before modelling.

### Team Members
1. Victor388  
2. Abdiqalaq243  
3. Kendi807  
4. Bradley346  

---
## WEEK TWO WORK

### Advanced Data Cleaning and Standardization (Kendi)
The Week 2 task focused on advanced transformation and ensuring data readiness for analysis.  

#### Key Steps Performed:
- **Handled outliers** using the IQR method to reduce skew and improve accuracy.  
- **Reduced noise** by smoothing categorical inconsistencies and removing irrelevant data.  
- **Standardized formats** across numerical and categorical columns to maintain consistency.  
- **Exported cleaned dataset** (`final_dataset.csv`) ready for analytical modelling.  

#### Output Files:
- `data/raw.csv` — Original merged dataset  
- `data/transformed.csv` — After Week 1 transformations  
- `data/final_dataset.csv` — Fully cleaned dataset after Week 2  

---

### Tools Used
- Python (Pandas, NumPy)
- Jupyter Notebook
- Git / GitHub for version control
=======
The Student Performance and Attendance dataset from Kaggle contains real-world student records with missing and inconsistent values. It includes attendance behavior and academic scores, allowing analysis of how absenteeism affects performance. It is ideal for ETL cleaning, feature engineering, and education data mining tasks.
>>>>>>> 2893197 (Initial commit)

# **WEEK TWO — Data Cleaning & Transformation**

## **Overview**
Week 2 focused on preparing the dataset for analysis by removing outliers, reducing noise, standardizing formats, and exporting the final cleaned file.

---

## **Tasks Completed**

### **1. Outlier Handling**
- Used the IQR method for numeric columns.
- Removed 45 outliers from `StudyHours`.
- No outliers detected in: Attendance, Age, OnlineCourses, AssignmentCompletion, ExamScore.

---

### **2. Noise Reduction**
- Trimmed whitespace from all categorical fields.
- Standardized text casing (Title Case).
- Replaced noisy placeholders (`?`, `N/A`, `--`, `Null`, `0`) with `NaN`.
- Fixed minor typos in labels (e.g., "Femal" → "Female", "Ye" → "Yes").

---

### **3. Standardization**
- Rounded numeric columns to 2 decimal places.
- Reordered columns alphabetically for clarity.

---

### **4. Final Output**
- Final cleaned dataset saved as: **`final_dataset.csv`**
- Final shape: **12,424 rows × 18 columns**
- Updated notebook: `extract_transform.ipynb`

---

