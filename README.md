# Healthcare Cost Drivers Analysis (In Progress)

## Project Overview  
This project analyzes healthcare cost drivers using a dataset of 100,000+ patient records to uncover patterns in lifestyle, demographics, and utilization.

---

##  Business Questions  
- Do lifestyle habits (smoking and alcohol use) impact healthcare utilization and total claims?  
- How do health conditions (e.g., hypertension and BMI) influence medical costs?  
- Which lifestyle group (smokers vs non-smokers, alcohol users vs non-users) generates the highest claims?  

---

##  Data Cleaning (Excel)  
- Reduced dataset from 54 columns to relevant features for analysis 
- Converted raw data into structured table format for easier filtering and manipulation
- Created duplicate sheet to preserve the original dataset before cleaning

---
## Data Quality Corrections (Excel)
- Corrected *4,441 records* where individuals under 21 were assigned invalid lifestyle behaviors:
    - Updated alcohol frequency to "*None*"
    - Updated smoking status to "*Never*"
- Corrected *2,115 records* where individuals under age 16 were assigned unrealistic values:
    - Set income values to *NULL* (blannk)
    - Set dependents to 0
- Addressed invalid or missing age values (e.g., age= 0) to improve dataset consistency

---

## Initial Insights (Early Findings)  
- Preliminary review suggests smokers tend to have higher total claims  
- Higher BMI appears to correlate with increased healthcare visits  

---

## Tools Used  
- Excel (data cleaning & initial analysis)  
- SQL (planned for deeper analysis)  
- Tableau (planned for visualization)  

---

## Next Steps  
- Perform SQL analysis to validate trends  
- Build Tableau dashboard to visualize key insights  
- Develop business recommendations based on findings  
