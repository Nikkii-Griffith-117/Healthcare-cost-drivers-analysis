# Healthcare Cost Drivers Analysis (In Progress)

## Project Overview  
This project analyzes healthcare cost drivers using a dataset of 100,000+ patient records to uncover patterns in lifestyle, demographics, and utilization.

---

##  Business Questions  
- Do lifestyle habits (smoking and alcohol use) impact healthcare utilization and total claims?  
- How do health conditions (e.g., hypertension and BMI) influence medical costs?  
- Which lifestyle group (smokers vs non-smokers, alcohol users vs non-users) generates the highest claims?  

---

##  Data Cleaning 
#### Microsoft Excel  
- Reduced dataset from 54 columns to relevant features for analysis 
- Converted raw data into structured table format for easier filtering and manipulation
- Created duplicate sheet to preserve the original dataset before cleaning
   
#### *Data Quality Corrections* 
#### Microsoft Excel
- Corrected *4,441 records* where individuals under 21 were assigned invalid lifestyle behaviors:
    - Updated alcohol frequency to "*None*"
    - Updated smoking status to "*Never*"
- Corrected *2,115 records* where individuals under age 16 were assigned unrealistic values:
    - Set income values to *NULL* (blank)
    - Set dependents to 0
- Addressed invalid or missing age values (e.g., age= 0) to improve dataset consistency
#### BigQuery (SQL)
- Standardized categorical values (e.g., “Never” vs “never”) during SQL analysis using transformation functions (UPPER/INITCAP) to ensure accurate grouping

---
## SQL Analysis (BigQuery)
  - SQL queries were executed in BigQuery to analyze the relationship between lifestyle habits, health conditions, and healthcare utilization and costs.
  
 ___
## SQL Queries (BigQuery)

### -- Q1: Lifestyle impact (smoking + alcohol)

SELECT
  UPPER(smoker) AS smoker,
  UPPER(alcohol_freq) AS alcohol_freq,
  COUNT(*) AS total_people,
  ROUND(AVG(visits_last_year), 2) AS avg_visits,
  ROUND(AVG(claims_count), 2) AS avg_claims,
  ROUND(AVG(total_claims_paid), 2) AS avg_total_cost
FROM `healthcare-cost-drivers.healthcare_cost_drivers.healthcare_cost_drivers_cleaned`
GROUP BY UPPER(smoker), UPPER(alcohol_freq)
ORDER BY avg_total_cost DESC;

### -- Q2: Hypertension impact

SELECT
  hypertension,
  ROUND(AVG(bmi), 2) AS avg_bmi,
  COUNT(*) AS total_people,
  ROUND(AVG(visits_last_year), 2) AS avg_visits,
  ROUND(AVG(claims_count), 2) AS avg_claims,
  ROUND(AVG(total_claims_paid), 2) AS avg_total_cost
FROM `healthcare-cost-drivers.healthcare_cost_drivers.healthcare_cost_drivers_cleaned`
GROUP BY hypertension
ORDER BY avg_total_cost DESC;


### -- Q3: Smoking vs cost
SELECT
  INITCAP(smoker) AS smoker,
  COUNT(*) AS total_people,
  ROUND(AVG(total_claims_paid), 2) AS avg_total_cost
FROM `healthcare-cost-drivers.healthcare_cost_drivers.healthcare_cost_drivers_cleaned`
GROUP BY INITCAP(smoker)
ORDER BY avg_total_cost DESC;

### -- Q3 Extension: Alcohol vs cost
SELECT
  UPPER(alcohol_freq) AS alcohol_freq,
  COUNT(*) AS total_people,
  ROUND(AVG(total_claims_paid), 2) AS avg_total_cost
FROM `healthcare-cost-drivers.healthcare_cost_drivers.healthcare_cost_drivers_cleaned`
GROUP BY UPPER(alcohol_freq)
ORDER BY avg_total_cost DESC;

---

## Insights  
### 1. Lifestyle Impact on Healthcare Utilization (Smoking + Alcohol)
- Current smokers consistently had the highest healthcare costs across all alcohol consumption levels
- The highest-cost group was current smokers who do not consume alcohol, averaging ~$2,102 in total claims
- Alcohol consumption alone showed minimal variation in cost compared to smoking status
- Healthcare utilization (visits and claims) remained relatively similar across alcohol groups but increased with smoking status
#### Key takeaway:
Smoking is a significantly stronger driver of healthcare costs than alcohol consumption.

### 2. Health Conditions (Hypertension & BMI)
- Individuals with hypertension had nearly double the average total healthcare cost (~$2,227 vs ~$1,160)
- They also had:
  - Higher average visits (2.75 vs 1.72)
  - Higher average claims (2.56 vs 1.38)
- BMI differences were minimal, indicating that hypertension itself is a stronger cost indicator than BMI alone
#### Key takeaway:
   Hypertension is a major driver of both healthcare utilization and cost.
  
### 3. Lifestyle Comparison (Smoking vs Alcohol)
- Current smokers had the highest average healthcare costs (~$2,023)

  *Followed by:*
  - Former smokers (~$1,464)
  - Non-smokers (~$1,252)
- Alcohol consumption showed much smaller cost differences:
  - Weekly (~$1,400)
  - Daily (~$1,391)
  - Occasional (~$1,386)
#### Key takeaway:
Smoking has a substantially greater impact on healthcare costs than alcohol consumption.

---
## SQL Analysis Screenshots
###### Question 1:
<img width="1818" height="803" alt="Pasted Graphic 2" src="https://github.com/user-attachments/assets/933a4a52-8fbc-4eda-bb4e-5bf024874f9c" />

###### Question 2:
<img width="2874" height="1340" alt="Pasted Graphic" src="https://github.com/user-attachments/assets/e85e0868-d60b-4b86-938f-a0a324d5399e" />

###### Question 3:
<img width="1722" height="1434" alt="image" src="https://github.com/user-attachments/assets/f9b29af5-6c9d-4fdb-9ce8-bf36e65ad931" />

---
## Tools Used  
- Excel: Used for initial data inspection and preliminary cleaning.
- BigQuery (SQL): Leveraged for complex querying and scalable analysis of the 100k+ record dataset, ensuring greater performance and reliability than traditional spreadsheets.
- Tableau: Selected for developing interactive visualizations and final insights.

---

## Next Steps  
- Develop interactive dashboards in Tableau to visualize key findings
- Translate insights into actionable business recommendations
- Continue refining analysis to support decision-making in healthcare cost management
