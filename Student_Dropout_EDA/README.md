# Student Dropout & Academic Success — Exploratory Data Analysis

Exploratory Data Analysis (EDA) on the **"Predict Students' Dropout and Academic Success"** dataset, aiming to identify early warning signals for student dropout in higher education using demographic, socio-economic, and academic performance data.

##  About the Dataset

This project uses the **"Predict Students' Dropout and Academic Success"** dataset, originally published by the **UCI Machine Learning Repository** as part of a research project supported by the **SATDAP - Capacitação da Administração Pública** program (grant **POCI-05-5762-FSE-000191**, Portugal).

**Original dataset source:** [UCI Machine Learning Repository — Predict Students' Dropout and Academic Success](https://archive.ics.uci.edu/dataset/697/predict+students+dropout+and+academic+success?utm_source=chatgpt.com)

Its purpose is to help reduce academic dropout and failure in higher education by using machine learning techniques to identify at-risk students at an early stage of their academic path, so that support strategies can be put in place in time.

The dataset includes information known at the time of student enrollment (academic path, demographics, and socio-economic factors), along with academic performance data from the first and second semesters. The problem is formulated as a **three-class classification task**, predicting the student's status at the end of the normal course duration:

- **Dropout**
- **Enrolled**
- **Graduate**

| Property | Value |
|---|---|
| Number of instances | 4,424 students |
| Number of features | 36 |
| Target classes | Dropout (1,421) · Enrolled (794) · Graduate (2,209) |
| Missing values | None (pre-cleaned) |
| Recommended split | 80% train / 20% test |

##  Project Goal

This project performs an exploratory data analysis to answer a set of guided questions, moving from a general overview of the target distribution down to detailed relationships between individual features and student outcomes, in order to identify which factors are the strongest early predictors of dropout.

##  Repository Structure

```text
.
├── Student_Dropout_EDA.py       # Full EDA script (generates all 11 charts)
├── dataset_overview.md          # Full dataset & feature documentation
├── dataset.xlsx                 # Raw dataset
└── README.md
```

##  Tech Stack

- Python 3
- pandas
- matplotlib
- seaborn
- openpyxl

##  How to Run

```bash
# 1. Clone the repository
git clone https://github.com/romina1831/Student_Dropout_EDA.git
cd Student_Dropout_EDA

# 2. Install dependencies
pip install pandas matplotlib seaborn openpyxl

# 3. Run the analysis
python Student_Dropout_EDA.py
```

##  Analysis Questions & Charts

Each question below was answered with a chart type suited to the data it explores.

| # | Question | Chart Type |
|---|---|---|
| 1 | What is the distribution of the target classes? | Countplot |
| 2 | Does 2nd semester grade differ across target groups? | Boxplot |
| 3 | How does the number of approved curricular units relate to dropout? | Barplot |
| 4 | Is there a relationship between admission grade and final outcome? | KDE plot |
| 5 | Do debtor / tuition-fees-not-up-to-date students drop out more? | Stacked percentage bar |
| 6 | How does scholarship status relate to outcome? | Grouped countplot |
| 7 | How does age at enrollment vary by outcome? | Violin plot |
| 8 | Is parents' education level related to student outcome? | Barplot |
| 9 | Does the macroeconomic unemployment rate relate to dropout? | Boxplot |
| 10 | Which numeric features correlate most with each other / the target? | Correlation heatmap |
| 11 | Can two key features together separate the outcome groups? | Scatterplot |

##  Key Findings

- **Class imbalance**: 50% Graduate, 32% Dropout, 18% Enrolled — should be accounted for in any downstream modeling.
- **Academic performance is the strongest predictor**: 2nd-semester approved units and grades show the highest correlation with the target (≈0.62 and ≈0.57 respectively). Dropout students typically have near-zero approved units and grades, since many leave before completing evaluations.
- **Financial status matters a lot**: only ~6% of students with tuition fees not up to date graduate, versus the majority who drop out. Debtor students graduate at roughly a third of the rate of non-debtors.
- **Scholarship holders** graduate at a much higher rate than dropout rate within that group, likely reflecting both reduced financial pressure and merit-based eligibility.
- **Age at enrollment**: dropout students show a wider age distribution with a longer tail toward older ages, while graduates cluster tightly around 18–22.
- **Admission grade and macroeconomic indicators (unemployment, inflation, GDP) show weak-to-no correlation with the outcome** — they are not useful standalone predictors.
- Combining **approved units** and **semester grade** visually separates the three outcome groups well, suggesting these are strong candidate features for a predictive model.

##  Dataset Documentation

See [`dataset_overview.md`](./dataset_overview.md) for the full feature dictionary (36 features across 7 categories, with descriptions and value codings).

##  Dataset Source

The original dataset is publicly available through the **UCI Machine Learning Repository**:

[Predict Students' Dropout and Academic Success — UCI Machine Learning Repository](https://archive.ics.uci.edu/dataset/697/predict+students+dropout+and+academic+success?utm_source=chatgpt.com)

Please refer to the original UCI dataset page for the complete dataset description, feature definitions, research context, and licensing information.

##  License

This project uses a publicly available academic dataset. Please refer to the original dataset source for licensing terms. The analysis code in this repository is provided for educational purposes.

##  Author

Personal project, built for educational purposes.