HR Analytics Dashboard (Tableau + SQL)
Make data-driven HR decisions with an interactive dashboard for attrition, headcount, job satisfaction, and demographics—built end-to-end from raw CSVs to polished insights.
▶️ Live Dashboard:
View on Tableau Public → HR ANALYTICS DASHBOARD
🚀 What I Built
End-to-end data pipeline: Ingested raw HR CSVs → cleaned/validated → modeled into analysis-ready tables.
SQL transformations: Calculated attrition, tenure, satisfaction scores, and departmental KPIs using aggregations and window functions.
Interactive Tableau dashboard: Dynamic filters by department, age band, education, gender, job role; drill-downs for attrition trends and satisfaction distribution.
📊 Key Business Questions Answered
Where is attrition concentrated (department, age, job role, education)?
Which groups have low job satisfaction and high attrition risk?
How do tenure and salary bands correlate with attrition?
What are the top retention opportunities by segment?
🧮 Core Metrics (KPIs)
Overall Attrition Rate = (# Exited) / (Avg Headcount)
Attrition by Segment: Department, Job Role, Age Band, Education, Gender
Job Satisfaction Index (avg score 1–4) by Department/Role
Avg Tenure (Years) and Salary Band Distribution (if available)
🔎 Highlights & Insights (Example Findings)
Sales & R&D show the highest attrition; ages 25–34 are most impacted.
Satisfaction ≤ 2 strongly correlates with higher exits in specific roles.
Early tenure (≤ 2 years) groups churn more—signals onboarding/mentorship gaps.
These examples illustrate the type of insights the dashboard surfaces. Your exact numbers will depend on the dataset in this repo.
🛠️ Tech Stack
Visualization: Tableau Public
Data Prep / SQL: SQLite / PostgreSQL (interchangeable), Excel/CSV
Version Control: Git & GitHub

🔄 Data Workflow (ETL)
Extract: Load raw HR CSVs (employee info, exits, survey scores).
Transform (SQL):
Standardize columns (dates, enums), dedupe, handle nulls.
Derive fields: tenure_years, age_band, salary_band, attrition_flag.
Build fact_employment and dim_employee, then compute KPIs.
Load to Tableau: Connect to processed tables / CSV extracts and publish to Tableau Public.
🧪 Example SQL (KPIs)
-- Attrition Flag
CASE WHEN employment_status = 'Exited' THEN 1 ELSE 0 END AS attrition_flag

-- Tenure (years)
ROUND((JULIANDAY(COALESCE(exit_date, '2025-01-01')) - JULIANDAY(hire_date)) / 365.25, 2) AS tenure_years

-- Attrition Rate by Department
SELECT
  department,
  SUM(attrition_flag) * 1.0 / NULLIF(AVG(headcount), 0) AS attrition_rate
FROM fact_employment
GROUP BY department;
🖥️ How to View the Dashboard
Easiest (recommended): Open the live link:
HR ANALYTICS DASHBOARD on Tableau Public
Local (optional):
Download tableau/HR_ANALYTICS_DASHBOARD.twbx
Open in Tableau Desktop or Tableau Public (Desktop)


