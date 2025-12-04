# DSA2040A_DataMining_Education_Analysis
## Student Performance & Attendance Analysis 

# Project Overview  
This project explores a real-world education dataset containing student attendance behavior, study habits, participation, and academic performance.  
Across 5 weeks, we implemented a full **data-mining pipeline**:

1. ETL (Extract–Transform–Load)  
2. Data Cleaning & Enrichment  
3. Exploratory & Statistical Analysis  
4. Data Mining Techniques  
5. Insights, Dashboarding & Storytelling  

Our goal was to understand what factors influence student performance and uncover patterns that can support educational decision-making.



#  Key Research Questions  
- How do attendance and study habits affect performance?  
- What patterns exist among high, average, and low-performing students?  
- Can we classify students based on performance indicators?  
- What actionable insights can educators use to improve results?



### Team Members
1. Victor - 388  
2. Abdiqalaq - 243  
3. Kendi - 807  
4. Bradley - 346  
5. Sammi Oyabi - 677



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



# **WEEK TWO — Data Cleaning & Enrichment**

## **Overview**
In Week 2, we built a complete ETL process to clean, standardize, and transform the raw dataset into a fully analysis-ready file.  
Key steps included loading the data, removing duplicates, handling missing values, mapping encoded categories, fixing data types, removing outliers, reducing noise, engineering new features, and exporting the final dataset.

---

## **Tasks Completed**

### 1. Loading Raw data
- Loaded dataset: **14,003 rows × 16 columns**  
- Inspected structure using `.shape`, `.head()`, `.info()`


### 2. Basic Cleaning
   - Removed duplicate rows  
   - Handled missing values using sensible defaults (e.g., Gender=0 (Female), Motivation=19(Medium), Internet=1(Yes))  

### 3. Column Mapping*
   - Converted numeric codes into human-readable labels  
     | Column      | Mapping |
     |------------|---------|
     | Gender     | 0 → Female, 1 → Male |
     | Motivation | 0 → Low, 1 → Medium, 2 → High |
     | FinalGrade | 0 → A, 1 → B, 2 → C, 3 → D |
   - Improved interpretability for visualization and modeling  
##  4. Data Type Correction  
Converted columns to correct formats:

### **Numeric → float**  
StudyHours, Attendance, Age, OnlineCourses, AssignmentCompletion, ExamScore

### **Categorical → category**  
Resources, Motivation, Gender, Internet, LearningStyle, StressLevel, Discussions, EduTech, FinalGrade, Extracurricular


### **5. Derived Fields**
   - `ActiveLearner`: Yes if student participates in extracurricular or uses EduTech  
   - `PassStatus`: Pass for grades A/B/C, Fail for D 

### **6. Outlier Handling**
- Used the IQR method for numeric columns.
- Removed 45 outliers from `StudyHours`.
- No outliers detected in: Attendance, Age, OnlineCourses, AssignmentCompletion, ExamScore.


### **7. Noise Reduction**
- Trimmed whitespace from all categorical fields.
- Standardized text casing (Title Case).
- Replaced noisy placeholders (`?`, `N/A`, `--`, `Null`, `0`) with `NaN`.
- Fixed minor typos in labels (e.g., "Femal" → "Female", "Ye" → "Yes").



### **8. Standardization & Formatting**
- Rounded numeric columns to 2 decimal places.
- Reordered columns alphabetically for readability.
- Re-validated categorical vs numerical columns  



### **9. Final Output**
- Final cleaned dataset saved as: **`final_dataset.csv`**
- Final shape: **12,424 rows × 18 columns**
- Updated notebook: `1_extract_transform.ipynb`



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
 
- Visualized via a heatmap
   
 <img width="1051" height="966" alt="image" src="https://github.com/user-attachments/assets/d9eb94c8-576a-469d-9a97-0ef50cae047c" />

- Correlations were generally low, indicating mostly independent features

#### **3. Distributions**  
- Histograms for :
  
   - study hours
     
    <img width="695" height="391" alt="image" src="https://github.com/user-attachments/assets/e299c1de-eceb-4437-a627-fc398dcfd094" />

   -  Online courses,
     
    <img width="695" height="391" alt="image" src="https://github.com/user-attachments/assets/2cda81e8-4780-46f6-9b37-2f25827cab5c" />

   - ExamScore
     
    <img width="695" height="391" alt="image" src="https://github.com/user-attachments/assets/7ef09a26-22f3-4888-ae1c-73e2d7c493f8" />

   - Age
    
    <img width="704" height="391" alt="image" src="https://github.com/user-attachments/assets/fda068e0-a595-4fb1-b960-1fa99c38af9d" />

   - AssignmentCompletion
    
  <img width="695" height="391" alt="image" src="https://github.com/user-attachments/assets/0a916442-8b9c-4a4c-98a9-30c03a06a16b" />

- Noted uniform distribution in StudyHours

#### **4. Group Comparisons**
- **Gender:** Average exam scores compared using pie charts
  
  <img width="636" height="656" alt="image" src="https://github.com/user-attachments/assets/06fdc546-b4cc-4c9f-aece-a593463f45f0" />

- **Age groups:** Exam scores binned and visualized with bar plots
  
  <img width="687" height="545" alt="image" src="https://github.com/user-attachments/assets/d77401f4-63f8-49a4-a5af-a9e11460fec3" />

- **Stress Level
  
  <img width="636" height="656" alt="image" src="https://github.com/user-attachments/assets/c97799f0-ba9c-4e08-a5f9-3475a9643aab" />

-   EduTech usage
  
  <img width="850" height="545" alt="image" src="https://github.com/user-attachments/assets/4f0bc44d-1005-468d-941a-22c3677ea26d" />

-  Learning Styles:
  
  <img width="850" height="545" alt="image" src="https://github.com/user-attachments/assets/41ef37f7-9d74-4885-a016-fa7e664c38d2" />


-  ** Compared via pie chart, violin plot and boxplots to identify trends  


#### **Output**  
- Notebook: **2_exploratory_analysis.ipynb**


 
# **WEEK 4 - Data Mining **

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
  
<img width="990" height="559" alt="image" src="https://github.com/user-attachments/assets/9ef95bf5-45ae-4305-85e2-c0ad027f5aeb" />

<img width="990" height="559" alt="image" src="https://github.com/user-attachments/assets/3983e097-2f6c-453a-8a69-b09b88703d94" />

<img width="990" height="558" alt="image" src="https://github.com/user-attachments/assets/d066570d-4c3a-4414-b634-f8430f1b98b4" />


#### **Output**  
- Notebook: **3_data_mining.ipynb**



# **WEEK 5 - Insights & Storytelling **

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

## **Power BI Dashboard**

Below are the exported Power BI dashboard views: 

1. Overview Dashboard

2. Analytics

3. Behavior & Demographics

4. Resources & Technology

5. Mining Results & Insights



lead_integration_victor.png

performance_analytics_abdi.png

behaviour_demo_kendi.png

resource_tech_bradley.png

mining_result_sammi.png

### Key Insights

Low study hours + poor attendance → highest failure risk

ExamScore, StudyHours, and Attendance are strongest performance indicators

High performers consistently have high internet access + good study routines

#### Recommendations

Provide targeted support for at-risk clusters

Monitor students with <70% attendance

Promote 15+ hours of weekly study

Guarantee internet + learning resources availability



## 6. Tools & Techniques
**Languages & Libraries:**  
- Python (Pandas, Numpy, Seaborn, Matplotlib, Scikit-learn)  

**Techniques Used:**  
- ETL: cleaning, transformations, derived columns  
- Statistical Analysis: correlations, distributions, group comparisons  
- Data Mining: K-Means clustering, Decision Tree classification, Association Analysis  



## 7. Team Contributions
| Member          | Contributions                                       |
|-----------------|-----------------------------------------------------|
| Victor-388      |     data exctration & dashboard                     |
| Abdiqalaq-243   |data extraction & ReadMe                             |
| Kendi-807       |   data cleaning,data manipulation,ReadMe & dashboard|
| Bradley-346     |  data cleaning,EDA analysis,ReadMe & dashboard      |
| Sammi Oyabi-677 |     data mining,ReadMe & dashboard                  |



## 8. How to Run
1. Clone repository  
2. Ensure Python 3.x with required packages installed  
3. Run notebooks sequentially:  
   - `1_extract_transform.ipynb` → `2_exploratory_analysis.ipynb` → `3_data_mining.ipynb` → `4_insights_dashboard.ipynb`  
4. Final datasets saved in `../data/final/`  


