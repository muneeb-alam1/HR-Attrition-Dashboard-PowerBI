# 📉 HR Attrition Analysis Dashboard

## 📌 Project Overview
This project showcases an interactive **HR Attrition Analysis Dashboard** built using Microsoft Power BI. 
It transforms raw employee data into meaningful insights to help HR teams understand why employees leave and which groups
are most at risk.

The goal was to go beyond surface-level reporting — instead of just showing *how many* employees left,
this dashboard uncovers **why** they left and **who** is most at risk of leaving next. It combines DAX-powered KPIs, Power Query 
data cleaning, and cross-dimensional visuals into a 3-page interactive dashboard that HR teams can use to make 
data-driven decisions.

---

## 🎯 Project Objectives
- Analyze employee attrition across departments, job roles, salary slabs, and age groups to identify where
turnover is concentrated
- Identify the key behavioral and structural drivers of attrition — including overtime, tenure, job satisfaction, and
business travel frequency
- Uncover demographic patterns by examining gender, marital status, and education field combinations
- Build a fully interactive, multi-page Power BI dashboard using DAX measures and dynamic slicers that allow
HR teams to self-serve their own analysis

---

## 🛠️ What I Built
A **3-page interactive Power BI dashboard**, each page designed to answer one core question:

**Executive Summary** — What is the overall attrition picture?
**Drivers Analysis** — Why are employees leaving?
**Demographic Analysis** — Who is leaving?

### Technical Features
- **Custom DAX Measures:** Attrition Rate, Attrition Count, and filter-context-aware calculations that dynamically
respond to every slicer selection.
- **Power Query Transformations:** Mapped all numeric codes (e.g., satisfaction levels 1–4) to human-readable labels before analysis.
- Attrition breakdowns by department, job role, salary slab, tenure group, and age group.
- Cross-dimensional visuals including **Attrition by Job Role × Satisfaction** and **Attrition Risk by Age & Gender**.
- A clean dark-themed layout with consistent color coding and insight callout cards.
- Custom DAX measures stored in a **dedicated Measures Table** for clean model organisation.
- **Collapsible side filter panel** triggered by a button, keeps the dashboard clean when filters aren't in use.

**Tools & Technologies**

**Power BI Desktop** — Dashboard design and DAX development
**Power Query** — Data cleaning and transformation
**DAX** — Custom measures and calculated columns

---

## ⚠️ Challenges & Solutions
**Challenge 1**
The raw dataset used numbers (1–4) for satisfaction, work-life balance, and job involvement
ratings with no descriptive labels.

**Solution:** 
Used Power Query to map every numeric code to its descriptive equivalent (e.g., 1 → "Low", 4 → "Very High")
before loading data into the model.

**Challenge 2**
Many demographic variables were correlated, making it hard to 
isolate which factor was truly driving attrition.

**Solution:** 
Created cross-dimensional charts to expose compound risk segments (e.g: age 18–25 + overtime = highest-risk group).

**Challenge 3**
No space left on the dashboard canvas for slicers With multiple charts already occupying the canvas

**Solution:** Built a collapsible side filter panel triggered by a button — slicers stay hidden until 
needed, keeping the layout clean

---

## 🧮 DAX Measures
**Total Attrition** — counts only employees where attrition is "Yes" to get the correct attrition headcount:
```dax
Total Attrition = CALCULATE(COUNT('HR Analytics'[Attrition]), 'HR Analytics'[Attrition] = "Yes")
```
 
**Job Satisfaction Text** — converts numeric satisfaction scores into readable labels:
```dax
Job Satisfaction Text = 
SWITCH(
    TRUE(),
    'HR Analytics'[JobSatisfaction] <= 2, "Low",
    'HR Analytics'[JobSatisfaction] = 3, "Medium",
    'HR Analytics'[JobSatisfaction] = 4, "High"
)
```
 
**Working Years Group** — groups total working years into tenure bands for experience-based analysis:
```dax
Working Years Group = 
SWITCH(
    TRUE(),
    'HR Analytics'[TotalWorkingYears] <= 1, "0-1 Year",
    'HR Analytics'[TotalWorkingYears] <= 3, "1-3 Years",
    'HR Analytics'[TotalWorkingYears] <= 5, "3-5 Years",
    'HR Analytics'[TotalWorkingYears] <= 10, "5-10 Years",
    "10+ Years"
)
```
 
---

## 📊 Key Insights
### Executive Summary
- **1,470** Employees | Attrition: **237 (16.1%)** | Avg Age: **37** | Avg Salary: **$6.51K** | Avg Tenure: **7 years**
- **R&D Department** leads attrition at **56.1%**; new hires (0–1 year) exit fastest at **34.9%**
- **Sales Representatives** have the highest attrition rate by job role at **39.8%**
- Employees aged **26–35** account for the highest number of exits (**116 cases**)


### Drivers Analysis
- Overtime is the biggest driver **30.5%** attrition vs **10.4%** for non-overtime employees
- **52% of attrition** comes from frequent business travelers and low job satisfaction adds **19.7%**
- Employees **2–3 years without a promotion** show the highest attrition at **17.1%**


### Demographic Analysis
- **Single employees** leave at **25.5%** nearly double the rate of married employees **12.5%**
- **18–25 age group** carries the highest attrition risk at **64.1%** when working overtime
- Human Resources **22.8%** has the highest attrition by education, followed by Technical Degree **21.3%** and Marketing **19.3%**

---

## 💡 Business Recommendations
- Urgently review **overtime policies** given 30.5% attrition among overtime employees, particularly in Sales and Lab
Technician roles where overtime and attrition are both highest.
- Introduce **retention programs for 0–1 year employees** — including onboarding support and early check-ins — to curb
high early-stage exits.
- Revisit **salary bands below $5K**, as this group carries the highest attrition and likely warrants a pay review.
- Create **promotion roadmaps** for employees in the 2–3 year tenure window to prevent stagnation-driven turnover.
- Prioritize retention efforts on **Sales Representatives** (39.8% attrition) and **Laboratory Technicians** (62 exits).
- Develop **support programs for single employees** and frequent travelers, who show disproportionately high exit rates.

---

## 🖼️ Dashboard Preview
 
**Executive Summary**
<img width="991" height="560" alt="image" src="https://github.com/user-attachments/assets/bc03059b-99f2-40e8-8d88-076d73cd31ad" />


 
**Drivers Analysis**
<img width="1045" height="560" alt="image" src="https://github.com/user-attachments/assets/108d1a87-9f0e-4415-9a68-ab8d5c9990b0" />


 
**Demographic Analysis**
<img width="1044" height="560" alt="image" src="https://github.com/user-attachments/assets/806d5889-3e20-49a3-8b94-7c8cef2f0eb9" />

 
---
 
## 🚀 How to Use
1. Download the `.pbix` file
2. Open in **Power BI Desktop**
3. Use the slicers to filter by Department, Gender, or Job Role etc
4. Use **Ctrl + Click** on navigation buttons to switch between pages

---

## 📈  Future Improvements
- Add a **predictive attrition model** using Python or R integrated into Power BI
- Include a **manager-level drill-through** page for team-specific attrition
- Connect to a **live HR data source** for real-time monitoring
