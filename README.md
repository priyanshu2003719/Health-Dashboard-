# 🏥 Global Health Intelligence Dashboard
### Power BI | Multi-Dataset Analytics | Infectious Disease & Patient Risk Profiling

---

![Power BI](https://img.shields.io/badge/Power%20BI-F2C811?style=for-the-badge&logo=powerbi&logoColor=black)
![DAX](https://img.shields.io/badge/DAX-Advanced-blue?style=for-the-badge)
![Data Model](https://img.shields.io/badge/Data%20Model-Star%20Schema-green?style=for-the-badge)
![Status](https://img.shields.io/badge/Status-Complete-success?style=for-the-badge)

---

## 📌 Project Overview

The **Global Health Intelligence Dashboard** is a comprehensive, multi-page Power BI report that unifies six datasets into a single interactive analytics platform. It enables healthcare professionals, researchers, and policy-makers to explore infectious disease trends across **15+ countries** (2015–2025) and simultaneously assess individual patient organ health and risk profiles.

This project demonstrates end-to-end BI development: data modelling, advanced DAX engineering, dynamic image integration, and storytelling through visuals.

---

## 🎯 Business Problem Solved

Global and clinical health data is often siloed across departments, countries, and systems. This dashboard addresses that by:

- Consolidating **10 years of infectious disease surveillance data** (HIV/AIDS, Hepatitis B, HPV, Syphilis) across Africa, Asia, the Americas, Europe, and Oceania
- Providing **real-time patient-level risk profiling** — organ condition, BMI, blood pressure, smoking, alcohol, and family history — all in one view
- Enabling **comparative benchmarking** of treatment coverage, vaccination rates, and incidence trends across nations
- Surfacing actionable insights that support **resource allocation, intervention planning, and population health management**

---

## 📂 Data Architecture

The project integrates six source files into a clean relational model:

| File | Description |
|---|---|
| `Health_Dataset.csv` | 820+ rows of global disease surveillance data (2015–2025): cases, deaths, prevalence, vaccination & treatment coverage |
| `health_dataset.csv` | Patient-level clinical data: age, gender, smoking, BMI, organ, cholesterol, BP risk, alcohol, family history |
| `condition.csv` | Lookup table: `Healthy` / `Damaged` organ condition values |
| `Organs.csv` | Organ-to-image URL mapping (Google Drive thumbnails) for dynamic visuals |
| `Health_Image_Dataset.csv` | Disease-to-image URL mapping for contextual disease cards |
| `Image_Dataset.csv` | Organ × Condition image matrix for state-based visual rendering |

**Model type:** Star Schema — fact tables linked to dimension/lookup tables for efficient filtering and clean DAX logic.

---

## ⚙️ DAX Engineering Highlights

Custom measures and calculated columns were built to elevate basic aggregations into intelligent, context-aware KPIs:

### 📊 `vs Avg Age` — Contextual Benchmark Indicator
```dax
vs Avg Age = 
VAR _CurrentAge  = AVERAGE(health_dataset[Age])
VAR _OverallAge  = CALCULATE(AVERAGE(health_dataset[Age]), ALL(health_dataset))
VAR _Diff        = _CurrentAge - _OverallAge
RETURN
SWITCH(
    TRUE(),
    _Diff > 0, UNICHAR(9650) & " " & FORMAT(_CurrentAge, "0.0"),
    _Diff < 0, UNICHAR(9660) & " " & FORMAT(_CurrentAge, "0.0"),
    FORMAT(_CurrentAge, "0.0")
)
```
> **Why it matters:** Instantly communicates whether a filtered cohort skews older or younger than the overall population — critical for age-stratified risk analysis.

---

### 📊 `vs Avg BMI` — Body Mass Index Deviation Flag
```dax
vs Avg BMI = 
VAR _CurrentBMI  = AVERAGE(health_dataset[BMI])
VAR _OverallBMI  = CALCULATE(AVERAGE(health_dataset[BMI]), ALL(health_dataset))
VAR _Diff        = _CurrentBMI - _OverallBMI
RETURN
SWITCH(
    TRUE(),
    _Diff > 0, UNICHAR(9650) & " " & FORMAT(_CurrentBMI, "0.0"),
    _Diff < 0, UNICHAR(9660) & " " & FORMAT(_CurrentBMI, "0.0"),
    FORMAT(_CurrentBMI, "0.0")
)
```
> **Why it matters:** Enables clinical staff to flag patient groups with elevated BMI vs. baseline — a leading indicator for cardiovascular and metabolic risk.

---

### 📊 `Age Group` — Calculated Column for Demographic Segmentation
```dax
Age Group = 
SWITCH(
    TRUE(),
    health_dataset[Age] <= 28, "18–28",
    health_dataset[Age] <= 38, "29–38",
    health_dataset[Age] <= 48, "39–48",
    health_dataset[Age] <= 58, "49–58",
    health_dataset[Age] <= 68, "59–68",
    "69+"
)
```
> **Why it matters:** Transforms a continuous age field into structured cohorts, enabling demographic slicing across every visual without repeated code.

---

## 📊 Dashboard Pages & Key Visuals

### Page 1 — 🌍 Global Disease Surveillance
- **10-year trend lines** of Total Cases, New Cases, and Deaths by disease and country
- **KPI cards** for total tested population, vaccination coverage, and treatment coverage
- **Choropleth / region filters** by Africa, Asia, Americas, Europe, Oceania
- **Disease image cards** (dynamic via URL table) for HIV/AIDS, Hepatitis B, HPV, Syphilis
- Slicers: Year, Country, Region, Gender, Disease, Age Group

### Page 2 — 🫀 Patient Organ Risk Profiler
- **Dynamic organ image switcher** — renders Healthy vs. Damaged organ visuals based on filter selection
- **Patient risk breakdown** across smoking status, alcohol consumption, BP risk, cholesterol, and family history
- **BMI and Age benchmark cards** using `vs Avg BMI` and `vs Avg Age` DAX measures
- Slicers: Organ type, Condition (Healthy/Damaged), Gender, Age Group

---

## 🛠️ Technical Skills Demonstrated

| Skill | Detail |
|---|---|
| **Data Modelling** | Star schema with 6 tables, proper relationships, cardinality management |
| **Advanced DAX** | VAR/RETURN patterns, CALCULATE + ALL for context transition, SWITCH for conditional formatting |
| **Dynamic Visuals** | Image URLs bound to slicer state for organ condition rendering |
| **UX Design** | Multi-page layout, consistent colour theme, icon-driven navigation |
| **Data Cleaning** | Cross-file consistency checks, lookup table design, % formatting normalisation |
| **Storytelling** | Layered narrative from global macro-trends down to individual patient profiles |

---

## 📁 Project Files

```
📦 Global Health Intelligence Dashboard
 ├── Heath_Dashboard.pbix              ← Main Power BI report file
 ├── Health_Dataset.csv                ← Global disease surveillance data
 ├── health_dataset.csv                ← Patient-level clinical records
 ├── condition.csv                     ← Organ condition lookup
 ├── Organs.csv                        ← Organ image URL table
 ├── Health_Image_Dataset.csv          ← Disease image URL table
 ├── Image_Dataset.csv                 ← Organ × Condition image matrix
 └── Measures_and_Columns_Formula.txt  ← All custom DAX documented
```

---

## 🚀 How to Run

1. Clone or download this repository
2. Open `Heath_Dashboard.pbix` in **Power BI Desktop** (July 2024 or later recommended)
3. If prompted, update the data source paths to match your local file locations
4. Refresh the dataset — all visuals will populate automatically
5. Use the slicers on each page to explore cohorts interactively

> **Note:** The organ and disease images are loaded from Google Drive URLs embedded in the CSV files. An internet connection is required for image rendering.

---

## 🌐 Industry Impact — Why This Dashboard Matters

### 🏛️ Public Health & Government Agencies
Health ministries and WHO/UNICEF regional offices need to track disease progression across demographics and geographies in real time. This dashboard provides exactly that — decade-long trend analysis at a glance, enabling evidence-based decisions on vaccine rollout, testing campaigns, and resource distribution.

### 🏥 Hospitals & Clinical Networks
With patient-level risk profiling (organ condition, BMI benchmarking, smoking and alcohol flags), clinical administrators can identify high-risk cohorts before they become critical — reducing preventable admissions and optimising care pathways.

### 💊 Pharmaceutical & Biotech Companies
Drug developers and market access teams need granular epidemiological data to prioritise R&D investment and target markets. The 10-year incidence and treatment coverage data in this dashboard directly supports commercial strategy for infectious disease portfolios.

### 🎓 Academic & Research Institutions
Epidemiologists and public health researchers can use this platform as a longitudinal study tool — tracking how prevalence rates and treatment coverage co-evolve, and identifying regions where intervention is lagging behind disease burden.

### 📋 Insurance & Health Risk Assessment
Actuarial and underwriting teams can leverage the patient risk profiling layer — combining BMI deviation, BP risk, cholesterol levels, family history, and lifestyle factors — to build more accurate, data-driven risk segmentation models.

------------------------------
## 1. Smoking Health Risk Analysis Dashboard
This dashboard provides a comprehensive look at how smoking behaviors correlate with organ damage and clinical risk factors like BMI and cholesterol.

* Organ Health Visualization: The central focus is an interactive anatomical model. Users can toggle between "Healthy" and "Damaged" views to see the physical impact on major organs (Heart, Kidney, Liver, Lungs).
* Patient Profile: It tracks a cohort of 155 patients. Key KPIs compare the current selection's average age (57.5) and BMI (29.2) against the overall population average using visual indicators (up/down arrows).
* Smoking Demographics:
    * Status: Over half of the analyzed group (50.97%) are current smokers.
    * Intensity: The line chart reveals that smoking duration (YOS) and daily intake (CPD) peak significantly in the 39–48 and 59–68 age brackets.
* Clinical Risk Correlation: The stacked bar chart shows that as patients age, the proportion of High Cholesterol and Hypertension Risk increases, particularly starting in the 49–58 age group.

------------------------------
## 2. Sexually Transmitted Diseases Analysis Dashboard
This dashboard tracks global epidemiological trends for STDs, with the current view filtered for Syphilis.

* Temporal Trends: The line chart tracks average new cases and deaths from 2015 to a projected 2025. It shows significant volatility, with peaks in cases around 2019 and 2022, followed by a declining trend toward 2025.
* Geographic Distribution:
   * Regional Prevalence: Africa has the highest prevalence rate by a wide margin, followed by Asia and the Americas.
   * Global Map: The globe highlights specific "hotspots," allowing health officials to see exactly where the disease density is highest (darker shaded regions).
* Demographic Breakdown:
   * Gender: The "Incidence Rate by Gender" plot shows that Syphilis affects males and females at nearly identical rates, though the male rate appears slightly higher based on the dot plot.
* Microscopic Visual: The 3D model on the left provides a visual identification of the bacterium (Treponema pallidum), which is useful for educational contexts.


