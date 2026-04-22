# Health-Dashboard
 **Organ Health &amp; Risk Analytics Dashboard**

**This is a comprehensive, professional breakdown of your **Organ Health Risk & Diagnostic Analytics** project. This project showcases a high level of proficiency in medical data modeling, custom DAX engineering, and advanced Power BI visualization.**

---

# 🏥 Organ Health & Risk Analytics Dashboard
**A Data-Driven Diagnostic Tool for Predictive Health Assessment**
**This project leverages clinical data to analyze the impact of lifestyle choices (smoking, alcohol, BMI) on vital organ conditions. By combining comparative DAX measures with dynamic visual storytelling, the system provides an intuitive interface for identifying high-risk patient profiles.**

---

## 🔬 Project Architecture & Data Modeling

### 1. The Clinical Core :  - <a href ="https://github.com/priyanshu2003719/Health-Dashboard-/blob/main/health_dataset.csv"> (`health_dataset.csv`)</a>
A robust dataset featuring **2,488 patient records**, tracking critical health markers:
* **Lifestyle Indicators:** Smoking status (years/frequency) and alcohol consumption levels.
* **Biometric Data:** Age, Gender, BMI, and Cholesterol levels.
* **Medical Risk Factors:** Blood Pressure (BP) Risk and Family History.
* **Target Diagnostics:** Specific organ focus (Heart, Lungs, Liver, Kidney) and their condition (Healthy/Damaged).

### 2. Multi-Dimensional Reference Layers
To enhance the analytical depth, the model incorporates specialized support tables:
* **`Organs.csv` & `Image Dataset.csv`:** Mapping clinical data to high-resolution icons and diagnostic thumbnails via Google Drive URLs for a visually-rich user experience.
* **`condition.csv`:** A normalized reference for binary state tracking (Healthy vs. Damaged).

---

## 🧮 Advanced DAX Engineering (`Measures and Columns Formula.txt`)
The intelligence of the dashboard is driven by custom-coded logic designed for comparative analysis:

* **Dynamic Benchmarking (`vs Avg Age` & `vs Avg BMI`):**
    * Uses `AVERAGE` and `CALCULATE(ALL())` to compare individual/filtered groups against the global dataset average.
    * **Visual Logic:** Employs `UNICHAR(9650)` (▲) and `UNICHAR(9660)` (▼) within a `SWITCH` statement to provide instant directional feedback on health metrics.
* **Demographic Segmentation (`Age Group`):**
    * A calculated column utilizing nested `SWITCH(TRUE())` logic to bin patients into logical cohorts (e.g., "18–28", "29–38") for trend identification.

---

## 📊 Business Intelligence & Visualization : <a href ="https://github.com/priyanshu2003719/Health-Dashboard-/blob/main/Heath%20Dashboard.pbix"> (`Heath Dashboard.pbix`)</a>

The dashboard is engineered to transform raw clinical data into a diagnostic story:

* **Executive KPIs:** High-level cards tracking total patients, average BMI, and percentage of "Damaged" vs "Healthy" organ states.
* **Risk Correlation Analysis:** Visualizing how "Years of Smoking" directly impacts the probability of "Damaged" organ results.
* **Interactive Slicers:** Utilizing **Chiclet Slicers** (as seen in the `.pbix` metadata) for intuitive filtering by Organ type, Gender, and Smoking Status.
* **Visual Identity:** A premium medical interface utilizing customized background canvases (`Background_Viz`) and high-fidelity organ icons to bridge the gap between data and clinical reality.

---

## 🚀 Key Insights Delivered
* **Risk Identification:** Pinpoints specific age groups and BMI ranges where organ damage risk is statistically higher.
* **Lifestyle Impact:** Quantifies the correlation between "Cigarettes Per Day" and specific organ failure (e.g., Lungs vs. Heart).
* **Clinical Benchmarking:** Allows healthcare providers to see at a glance if a patient’s metrics are above or below the normative population average.

