# Masai-Python-Major-Project(School Student Attendance Analysis & Proxy Detection)

##Problem Statement
Design an automatic attendance taking system for a class of 600. How would you keep a  track of proxies and low attendance notifications to students. 

## Overview
This project analyzes daily student attendance data across multiple schools and identifies students with low attendance and potential proxy behavior. Using the first 600 entries of the publicly available **School-Student-Daily-Attendance** dataset, the project calculates attendance percentages, flags students below a threshold, detects proxy attendance patterns, generates notifications, and visualizes key insights for instructors.

The analysis was implemented using Python in Google Colab, and the results are exported as CSV files with corresponding plots for easy tracking.

---

## Dataset
The dataset was sourced from [School-Student-Daily-Attendance GitHub repository](https://github.com/sankarisubbulakshmi/School-Student-Daily-Attendance).  

It contains the following columns:

| Column Name | Description |
|------------|-------------|
| `School DBN` | Unique identifier for each school |
| `Date` | Date of attendance record |
| `Enrolled` | Total number of classes a student is enrolled in |
| `Absent` | Number of classes a student was absent |
| `Present` | Number of classes a student was present |
| `Released` | Number of classes a student had approved leave |
| `Roll_No` | Added manually to categorize students |

For this project, only the first **600 entries** were used to simplify analysis and demonstrate methodology.

---

## Project Structure
The repository contains the following files:  

- **Colab Notebook:** `project_notebook.ipynb` – Main code for processing and visualizations  
- **CSV Files:**  
  - `attendance_alerts_all.csv` – Attendance messages for all students  
  - `attendance_alerts_low_only.csv` – Students below 75% attendance  
  - `low_attendance_notifications.csv` – Notifications sent to students  
  - `proxy_risk_report.csv` – Students with suspected proxy behavior  
- **Plots/Visuals:**  
  - `attendance_histogram.png` – Histogram of attendance percentages  
  - `proxy_bar_chart.png` – Top proxy risk students bar chart  

---

## Methodology
The methodology of the project can be summarized in four main steps:

### 1. Attendance Calculation
- Compute effective enrolled classes:  
\[
\text{Effective Enrolled} = \text{Enrolled} - \text{Released}
\]  
- Calculate student attendance percentage:  
\[
\text{Attendance \%} = \frac{\text{Total Present}}{\text{Effective Enrolled}} \times 100
\]  
- Students below **75% attendance** are flagged for notifications.

### 2. Proxy Detection
- Analyze row-wise attendance patterns for unusual behavior:  
  - `Proxy_Soft_Outlier` identifies minor anomalies  
  - `Proxy_Row_Score` aggregates suspicious behavior  
- Students with high proxy scores are listed in `proxy_risk_report.csv`.
