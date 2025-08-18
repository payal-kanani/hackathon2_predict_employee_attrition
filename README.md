# Predict Employee Attrition

**Predict Employee Attrition** is a comprehensive data analysis tool designed to streamline data exploration, analysis, and visualisation. The tool supports multiple data formats and provides an intuitive interface for both novice and expert data scien


## Dataset Content
This project uses multiple datasets and processed versions relating to employee attrition:
* WA_Fn-UseC_-HR-Employee-Attrition.csv: The original dataset containing HR data such as demographics, work conditions, and attrition labels.
* predict_employee_attrition_copy.csv: A cleaned copy of the original dataset, prepared for exploration.
* predict_employee_attrition_transformed.csv: The transformed dataset including derived features (e.g., age brackets, total satisfaction index) to support deeper analysis.

The datasets contain 1,470 employee records with 34 attributes covering demographics, job role, income, tenure, work-life balance, satisfaction metrics, and attrition outcomes.


## Business Requirements
* Identify key drivers of employee attrition across departments, roles, and demographics.
* Build a structured workflow (load → transform → extract → analyze) that allows reproducibility.
* Provide insights to guide HR policies and improve employee retention.
* Develop dashboard visuals to communicate attrition patterns and predictors.


## Hypothesis and how to validate?
The project tests the following five hypotheses:

1. Gender and Attrition - Null: Gender and attrition are independent.Validation: Chi-square test of independence on a contingency table (Gender × Attrition); visualise with a stacked bar showing attrition proportions by Gender.Outcome: p > 0.05 - fail to reject null (no significant relationship observed).
2. Age and Attrition (via AgeBracket) - Null: Age bracket and attrition are independent.Validation: Chi-square test of independence on AgeBracket × Attrition; support with a stacked column chart of attrition rate by age bracket.Outcome: p < 0.05 - reject null (attrition significantly varies across age brackets).
3. Department and Attrition - Null: Department and attrition are independent.Validation: Chi-square test of independence on Department × Attrition; bar chart of attrition proportions by department (counts and % for context).Outcome: p < 0.05 - reject null (department is significantly related to attrition).
4. Monthly Income and Attrition - Null: Monthly income and attrition are unrelated.Validation: Compare distributions by attrition status using normality-checked two-sample tests (Welch’s t-test if approximately normal; otherwise Mann–Whitney U). Add point-biserial correlation as a robustness check; visualise with box/violin plots by attrition status.Outcome: p < 0.05 - reject null (income levels differ significantly between attrition groups, lower income linked to higher attrition).
5. Total Satisfaction Level and Attrition - Null: Overall satisfaction level and attrition are unrelated.Validation: Two-sample test by attrition status (Welch’s t-test or Mann–Whitney U) on the engineered TotalSatisfaction metric; supplement with a logistic regression (Attrition ~ TotalSatisfaction) to quantify effect size (odds ratio). Visualise with boxplots and a probability curve from the logistic model.Outcome: p < 0.05 - reject null (lower overall satisfaction strongly associated with higher attrition).

Note: Job Satisfaction vs Attrition (a sub-hypothesis of #5) was also explored using a Chi-square test across the ordinal satisfaction levels, with a stacked bar for visualisation. Outcome: p < 0.05 - reject null (attrition differs significantly by job satisfaction level).

## Project Plan
* Data Collection: Gather raw HR dataset (WA_Fn-UseC_-HR-Employee-Attrition.csv).
* Data Loading: Initial load performed in predict_employee_attrition_load.ipynb.
* Data Transformation: Feature engineering and cleaning in predict_employee_attrition_transform.ipynb.
* Data Extraction: Preparation of focused analysis subsets in predict_employee_attrition_extract.ipynb.
* Analysis & Interpretation: Hypothesis testing, visualisation, and business impact assessment.

The chosen methodology ensures reproducibility and traceability across stages of the pipeline.

### Workflow Diagram:

graph TD
    A[Raw Data (CSV)] --> B[Data Loading Notebook]
    B --> C[Data Transformation Notebook]
    C --> D[Data Extraction Notebook]
    D --> E[Statistical Analysis + Visualisation]
    E --> F[Power BI Dashboard]


## Rationale to map Business Requirements to the Data Visualisations
* Overview Page (KPIs: Attrition Rate, Active/Inactive Employees, Total Employees) → Provides high-level business metrics for quick decision-making by HR leadership.
* Attrition by Gender and Marital Status (Donut Chart) → Helps assess whether demographic groups are disproportionately impacted, supporting fair and inclusive retention policies.
* Attrition by Age and Age Bracket (Histogram and Bar Chart) → Identifies life-stage trends (e.g., higher attrition in younger cohorts), guiding tailored engagement strategies.
* Attrition by Job Role and Department (Clustered Bar) → Surfaces role- and department-specific hotspots where interventions are most urgently needed.
* Attrition by Years at Company and Distance from Home (Line Charts) → Shows tenure- and commute-related attrition drivers, allowing HR to address onboarding/early career attrition and remote work/travel policies.
* Attrition by Overtime and Monthly Income (Bar/Column Charts) → Links compensation and workload balance to attrition, guiding policy changes in pay scales and overtime management.
* Attrition by Business Travel (Bar Chart) → Highlights mobility-related pressures contributing to attrition, especially in frequent travel roles.
* Attrition by Satisfaction Dimensions (Environment, Job, Work-Life Balance, Relationship) → Measures engagement factors, enabling HR to focus retention strategies on areas with the strongest negative impact.
* Attrition by Marital Status (Donut Chart) → Provides demographic context on personal-life balance, complementing work-life balance analysis.

## Analysis techniques used
* Chi-square tests: For categorical independence testing.
* Correlation analysis: To assess linear relationships between satisfaction, income, and attrition.
* Data visualisation: Bar charts, histograms, boxplots for pattern discovery.
* Feature engineering: Creating new variables (e.g., Age Bracket, Total Satisfaction index).

Limitations: Dataset is relatively small (1,470 rows), limiting generalisability. Certain categories (e.g., HR department) have low representation, impacting statistical robustness.

Generative AI was used to:

* Ideate hypothesis-testing approaches.
* Suggest dashboard layouts and visualisation techniques.
* Optimise code readability and structure.

## Ethical considerations
* Data Privacy: The dataset is anonymised and synthetic; no personal identifiers are included.
* Bias/Fairness: Representation imbalances (e.g., small HR sample) may bias interpretations.
* Societal Considerations: Analysis focuses on fairness and preventing biased HR decision-making.

## Dashboard Design
1. Overview Page: KPIs (attrition rate, headcount, average age, average income).
2. Attrition Analysis: Donut chart (Attrition Yes/No), bar charts by Department and Job Role.
3. Demographics: Age distribution, gender, and marital status stacked charts.
4. Tenure & Experience: Attrition trends by years at company and income distribution.
5. Work Conditions: Attrition split by Overtime, Business Travel, and Satisfaction Heatmaps.

Communication: Visuals were designed for non-technical HR managers with tooltips, labels, and interactivity. Technical audiences can further query Jupyter notebook outputs. 

## Unfixed Bugs
* Some categorical values in the original dataset (e.g., Department) are imbalanced, making certain statistical results less reliable.
* Visualisation scaling issues may arise in Power BI when comparing small vs large departments.
* Feedback from peers led to adjustments in feature engineering (e.g., Age Brackets), but some improvements remain ongoing.

## Development Roadmap
* Challenges: Handling categorical imbalance and ensuring statistical significance.
* Strategies: Use both proportions and raw counts, and validate findings with multiple metrics.
* Next Skills: Explore predictive modelling (e.g., logistic regression, random forests) for attrition prediction; improve Power BI dashboard interactivity with DAX measures.

## Main Data Analysis Libraries
* pandas: Data manipulation and cleaning (read_csv, groupby, feature creation).
* numpy: Numerical transformations.
* matplotlib & seaborn: Visualisation of attrition patterns.
* scipy.stats: Hypothesis testing (Chi-square).


## Credits 
### Content 

- Base dataset: IBM HR Analytics Employee Attrition & Performance Dataset (Kaggle)
- Guidance on Chi-square testing: SciPy documentation
- Code structuring best practices: Inspired by open-source HR analytics notebooks

### Media

- Code Institute CI logo provided via their asset repository

## Acknowledgements (optional)
* Thanks to our facilitator, Emma Lamont, and mentor, Spencer Barriball for their availability and feedback during the hackathon.
