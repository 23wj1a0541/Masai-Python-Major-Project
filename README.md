# Masai-Python-Major-Project(School Student Attendance Analysis & Proxy Detection)

## Problem Statement
Design an automatic attendance taking system for a class of 600. How would you keep a  track of proxies and low attendance notifications to students. 

## Overview
This project analyzes daily student attendance data across multiple schools to identify students with low attendance and potential proxy behavior. Using the first 600 entries of the publicly available **School-Student-Daily-Attendance** dataset, the project calculates attendance percentages, flags students below a 75% threshold, detects proxy attendance patterns, generates notifications, and visualizes key insights for instructors.

The analysis was implemented using Python in Google Colab, and the results are exported as CSV files with corresponding plots for easy tracking and reporting.

---

## Dataset
The dataset was sourced from the [School-Student-Daily-Attendance GitHub repository](https://github.com/sankarisubbulakshmi/School-Student-Daily-Attendance).

It contains the following columns:

| Column Name | Description |
|---------------|------------------------------------------------------|
| `School DBN`  | Unique identifier for each school                    |
| `Date`        | Date of the attendance record                        |
| `Enrolled`    | Total number of classes a student is enrolled in     |
| `Absent`      | Number of classes a student was absent for           |
| `Present`     | Number of classes a student was present for          |
| `Released`    | Number of classes for which a student had approved leave |
| `Roll_No`     | Unique identifier added manually to categorize students |

For this project, only the first **600 entries** were used to simplify analysis and demonstrate the methodology.

---

## Project Structure
The repository contains the following files:

-   **Colab Notebook:** `project_notebook.ipynb` – The main code for data processing, analysis, and visualization.
-   **CSV Files:**
    -   `attendance_alerts_all.csv` – Contains attendance messages for all students.
    -   `attendance_alerts_low_only.csv` – Lists only students with attendance below 75%.
    -   `low_attendance_notifications.csv` – A log of notifications sent to low-attendance students.
    -   `proxy_risk_report.csv` – A report of students with suspected proxy attendance behavior.
-   **Plots/Visuals:**
    -   `attendance_histogram.png` – A histogram showing the distribution of student attendance percentages.
    -   `proxy_bar_chart.png` – A bar chart of the top students with high proxy risk scores.

### Visual Examples:
Here are examples of the plots generated:

**Attendance Percentage Histogram**
This histogram visualizes the distribution of attendance percentages across all students, helping to identify common attendance ranges and potential clusters of low attendance.
![Attendance Histogram]
**Proxy Risk Bar Chart**
This bar chart displays the top students identified with the highest proxy risk scores, making it easy to spot individuals requiring further investigation.
![Proxy Bar Chart]

---

## Methodology
The methodology can be summarized in four main steps:

### 1. Attendance Calculation
-   Compute the number of effective classes a student is enrolled in:
    $$
    \text{Effective Enrolled} = \text{Enrolled} - \text{Released}
    $$
-   Calculate each student's attendance percentage:
    $$
    \text{Attendance \%} = \frac{\text{Total Present}}{\text{Effective Enrolled}} \times 100
    $$
-   Students with attendance below **75%** are flagged for notifications.

### 2. Proxy Detection
-   Analyze row-wise attendance patterns to identify unusual behavior:
    -   `Proxy_Soft_Outlier` flags minor anomalies in daily records.
    -   `Proxy_Row_Score` aggregates suspicious behaviors over time.
-   Students with high cumulative proxy scores are listed in the `proxy_risk_report.csv`.

### 3. Automated Notifications
-   A custom notification message is generated for each student who falls below the attendance threshold:
    ```text
    Dear [Roll No], your attendance is [Attendance %] ([Present]/[Enrolled]). Please improve to reach at least 75%.
    ```

### 4. Visualization
-   **Histogram:** Shows the overall distribution of attendance percentages.
-   **Boxplots:** Highlight at-risk students and identify statistical outliers.
-   **Bar Charts:** Display the top students with the highest proxy risk scores.

These visualizations allow instructors to quickly monitor attendance trends and identify potential issues.

---

## Results
-   **Attendance Alerts:** Alerts were successfully generated for all students, with a separate report for those below the 75% threshold.
-   **Proxy Risk:** The top 10 students with suspected proxy behavior were identified and visualized.
-   **Visual Insights:** Histograms and boxplots helped in clearly identifying clusters of low-attendance students.

### Example Notification Table

| Roll_No | Attendance % | Notification Message                                                                     |
|:--------|:-------------|:-----------------------------------------------------------------------------------------|
| 46      | 52.3%        | Dear 46, your attendance is 52.3% (22/42). Please improve to reach at least 75%. |
| 91      | 64.0%        | Dear 91, your attendance is 64.0% (32/50). Please improve to reach at least 75%. |

---

## How to Use
1.  Clone or download this repository.
2.  Open the Google Colab notebook: `project_notebook.ipynb`.
3.  Upload your dataset CSV file (e.g., `School-Student-Daily-Attendance.csv`).
4.  Run the notebook cells sequentially to generate the following:
    -   Attendance alert CSV files
    -   Proxy detection CSV file
    -   Visual plots for attendance and proxy risks
5.  Download the generated files and plots for reporting or further analysis.

---

## Observations
-   A small subset of students consistently had attendance below the required threshold.
-   The proxy detection heuristics successfully flagged patterns such as multiple consecutive absences followed by a sudden streak of perfect presence.
-   Visualizations were crucial for identifying at-risk students and trends that were not immediately evident from raw data tables.

---

## Future Work
-   **Extend Analysis:** Apply the methodology to the full dataset to analyze trends across all schools and students.
-   **Predictive Modeling:** Implement models (e.g., logistic regression, time series analysis) to forecast attendance and identify at-risk students proactively.
-   **Enhance Proxy Detection:** Use machine learning algorithms (e.g., Isolation Forest, K-Means Clustering) for more robust anomaly detection.
-   **Automate Notifications:** Integrate an email or SMS API to send notifications directly to students and guardians from the system.

---

## Acknowledgements
-   The **School-Student-Daily-Attendance** dataset by sankarisubbulakshmi.
-   Guidance from instructors and online resources for Python, Pandas, Matplotlib, and Seaborn.
-   Inspiration from research papers on educational data analytics and student attendance monitoring.
-   Special thanks to colleagues who provided feedback on the project methodology and visualizations.

---

## References
-   Sankari Subbulakshmi. *School Student Daily Attendance Dataset*. GitHub Repository. 2021.
-   Alred, Gerald J., Charles T. Brusaw, and Walter E. Oliu. *The Business Writer's Handbook*. 11th Edition, Bedford/St. Martin's, 2019.
-   Provost, Foster, and Tom Fawcett. *Data Science for Business*. O’Reilly Media, 2013.
-   Romero, Cristóbal, and Sebastián Ventura. “Educational Data Mining: A Review of the State of the Art.” *IEEE Transactions on Systems, Man, and Cybernetics, Part C*, vol. 40, no. 6, 2010, pp. 601–618.
-   Baker, Ryan S.J.d. “Data Mining for Education.” *International Encyclopedia of Education*, 3rd Edition, 2010.
