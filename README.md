# DSA2040A_DataMining_Education_Analysis
## Student Performance & Attendance Analysis 

# Project Overview  
This project explores a real-world education dataset containing student attendance behaviour, study habits, participation, and academic performance.  
Across 5 weeks, we implemented a full **data-mining pipeline**:

1. ETL (Extract–Transform–Load)  
2. Data Cleaning & Enrichment  
3. Exploratory & Statistical Analysis  
4. Data Mining Techniques  
5. Insights, Dashboarding & Storytelling  

Our goal was to understand what factors influence student performance and uncover patterns that can support educational decision-making.

---

#  Key Research Questions  
- How do attendance and study habits affect performance?  
- What patterns exist among high-, average-, and low-performing students?  
- Can we classify students based on performance indicators?  
- What actionable insights can educators use to improve results?

---

### Team Members
1. Victor - 388  
2. Abdiqalaq - 243  
3. Kendi - 807  
4. Bradley - 346  
5. Sammi Oyabi 

---

# **WEEK 1 — Project Kickoff & Dataset Selection**

### **Overview**  
Week 1 focused on establishing the project structure and performing an initial assessment of the raw dataset.

### **Tasks Completed**

1. **Topic Selection & Role Assignment**  
   - Domain chosen: **Education**  
   - Roles: ETL Lead, Analyst, Visualizer, Documenter  

2. **Dataset Review**  
   - Source: Kaggle education performance dataset  
   - 12+ features including: StudyHours, Attendance, Participation, TotalScore, Grade  

3. **Issue Identification**  
   - Missing values  
   - Inconsistent formatting  
   - Mixed data types  
   - Noisy categorical entries  

4. **Output**  
   - Initial README draft  
   - Raw dataset summary  

---

# **WEEK TWO — Data Cleaning & Enrichment**

## **Overview**
Week 2 focused on preparing the dataset for analysis by removing outliers, reducing noise, standardizing formats, and exporting the final cleaned file.


## **Tasks Completed**

### 1. Basic Cleaning
   - Removed duplicate rows  
   - Handled missing values using sensible defaults (e.g., Gender=0 (Female), Motivation=19(Medium), Internet=1(Yes))  

### 2. Column Mapping*
   - Converted numeric codes into human-readable labels  
     | Column      | Mapping |
     |------------|---------|
     | Gender     | 0 → Female, 1 → Male |
     | Motivation | 0 → Low, 1 → Medium, 2 → High |
     | FinalGrade | 0 → A, 1 → B, 2 → C, 3 → D |
   - Improved interpretability for visualization and modeling  
##  3. Data Type Correction  
Converted columns to correct formats:

### **Numeric → float**  
StudyHours, Attendance, Age, OnlineCourses, AssignmentCompletion, ExamScore

### **Categorical → category**  
Resources, Motivation, Gender, Internet, LearningStyle, StressLevel, Discussions, EduTech, FinalGrade, Extracurricular

---
### **4. Derived Fields**
   - `ActiveLearner`: Yes if student participates in extracurricular or uses EduTech  
   - `PassStatus`: Pass for grades A/B/C, Fail for D 

### **5. Outlier Handling**
- Used the IQR method for numeric columns.
- Removed 45 outliers from `StudyHours`.
- No outliers detected in: Attendance, Age, OnlineCourses, AssignmentCompletion, ExamScore.


### **6. Noise Reduction**
- Trimmed whitespace from all categorical fields.
- Standardized text casing (Title Case).
- Replaced noisy placeholders (`?`, `N/A`, `--`, `Null`, `0`) with `NaN`.
- Fixed minor typos in labels (e.g., "Femal" → "Female", "Ye" → "Yes").

---

### **7. Standardization & Formatting**
- Rounded numeric columns to 2 decimal places.
- Reordered columns alphabetically for readability.
- Re-validated categorical vs numerical columns  

---

### **8. Final Output**
- Final cleaned dataset saved as: **`final_dataset.csv`**
- Final shape: **12,424 rows × 18 columns**
- Updated notebook: `1_extract_transform.ipynb`

---

# **WEEK 3 — Exploratory Data Analysis**

### **Overview**  
Week 3 focused on gaining insights through visual and statistical EDA using Pandas, Seaborn and Matplotlib.

### **Tasks Completed**

#### **1. Distribution Analysis**  
- Histograms created for:  
  - StudyHours  
  - Attendance  
  - TotalScore  
- Identified right-skewed distribution in StudyHours.

#### **2. Correlation Analysis**  
- Explored relationships among numeric features 
  -(`Age`, `StudyHours`, `Attendance`, `ExamScore`, `AssignmentCompletion`, `OnlineCourses`)  
- Correlations were generally low, indicating mostly independent features 
- Visualized via a heatmap 

#### **3. Distributions**  
- Histograms for :
   - study hours, Online courses, ExamScore, Attendance, Age and AssignmentCompletion
- Noted right-skew in StudyHours

### **4. Group Comparisons
- **Gender:** Average exam scores compared using pie charts  
- **Age groups:** Exam scores binned and visualized with bar plots  
- **Stress Level, EduTech usage, Learning Styles:** Compared via pie chart, violin plot and boxplots to identify trends  


#### **Output**  
- Notebook: **2_exploratory_analysis.ipynb**

---
 
 # **WEEK 4 — Data Mining & Modelling **

### **Overview**  
Week 4 implemented multiple data-mining models to extract deeper structural patterns from the dataset.

### **Techniques Used**

#### **1. Clustering — K-Means**  
- Used standardized numeric features for clustering  
- Optimal clusters: 4 (determined via Elbow and Silhouette methods)  
- Cluster analysis revealed distinct student groups with varying study habits and exam scores  
- Visualizations: scatter plots for StudyHours vs ExamScore, Attendance vs ExamScore, etc.  

#### **2. Classification (Decision Tree)**  
- Target: `Pass/Fail` (grades A/B/C = Pass)  
- Features: numeric + categorical (Motivation, Internet, Resources, etc.)  
- Train/test split: 70/30  
- Model accuracy: 100% on both train and test  
- Key predictors: ExamScore, StudyHours, Attendance  
- Confusion matrix and feature importance visualizations included  

#### **3. Association Analysis**  
- Focused on high-performing students (grade A)  
- Converted numeric features into categorical bins: StudyHours, Attendance, ExamScore  
- Observed patterns:  
  | Feature       | Mode   | % of A students |
  |---------------|--------|----------------|
  | StudyHours    | High   | 48.5%          |
  | Attendance    | High   | 37.5%          |
  | Motivation    | Medium | 50.0%          |
  | Internet      | Yes    | 91.9%          |
  | Resources     | Medium | 48.2%          |
  | ExamScore     | High   | 100%           |
- Visualized patterns with stacked bar charts  

#### **Output**  
- Notebook: **3_data_mining.ipynb**

---

# **WEEK 5 — Insights & Storytelling **

### **Expected Deliverables**
- Dashboard (Power BI)  
- Performance distribution summary  
- Cluster visualizations  
- Attendance vs Score insights  

### **Insights**
1. Students in clusters with low study hours and low attendance are at risk of failing  
2. ExamScore, StudyHours, and Attendance are the strongest predictors of success  
3. High-performing students typically have access to internet and study consistently  

**Recommendations:**  
- Provide targeted support for low-performing clusters  
- Monitor attendance below 70% closely  
- Ensure equitable access to educational resources  
- Encourage 15+ hours of weekly study  

**Notebook:** `4_insights_dashboard.ipynb`  

---

## 6. Tools & Techniques
**Languages & Libraries:**  
- Python (Pandas, Numpy, Seaborn, Matplotlib, Scikit-learn)  

**Techniques Used:**  
- ETL: cleaning, transformations, derived columns  
- Statistical Analysis: correlations, distributions, group comparisons  
- Data Mining: K-Means clustering, Decision Tree classification, Association Analysis  

---

## 7. Team Contributions
| Member          | Contributions |
|-----------------|---------------|
| Victor-388      |               |
| Abdiqalaq-243   |               |
| Kendi-807       |               |
| Bradley-346     |               |
| Sammi Oyabi-677 |               |

---

## 8. How to Run
1. Clone repository  
2. Ensure Python 3.x with required packages installed  
3. Run notebooks sequentially:  
   - `1_extract_transform.ipynb` → `2_exploratory_analysis.ipynb` → `3_data_mining.ipynb` → `4_insights_dashboard.ipynb`  
4. Final datasets saved in `../data/final/`  

---