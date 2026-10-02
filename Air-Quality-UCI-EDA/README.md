# Air Quality UCI — Exploratory Data Analysis

An exploratory data analysis of the **UCI Air Quality dataset**, telling two parallel stories: how urban traffic, weather, and seasons shape air pollution, and how reliable low-cost metal-oxide sensors actually are compared to certified reference analyzers.

##  Dataset

The [Air Quality UCI dataset](https://archive.ics.uci.edu/dataset/360/air+quality) contains **9,357 hourly instances** of averaged readings from an array of 5 metal-oxide chemical sensors, embedded in an Air Quality Chemical Multisensor Device. The device was deployed at road level in a significantly polluted area of an Italian city, and recorded data from **March 2004 to April 2005** — one of the longest freely available field records of on-field deployed air quality sensor responses.

For each pollutant, the dataset provides two parallel readings:

| Type | Columns | Description |
|---|---|---|
| **Reference (ground truth)** | `CO(GT)`, `NMHC(GT)`, `C6H6(GT)`, `NOx(GT)`, `NO2(GT)` | Certified hourly concentrations from a co-located reference analyzer |
| **Low-cost sensor response** | `PT08.S1(CO)`, `PT08.S2(NMHC)`, `PT08.S3(NOx)`, `PT08.S4(NO2)`, `PT08.S5(O3)` | Raw hourly response of the corresponding metal-oxide sensor |
| **Weather** | `T`, `RH`, `AH` | Temperature, relative humidity, absolute humidity |

**⚠️ Missing values are encoded as `-200`**, not `NaN` — this must be handled before any analysis.

> Source: De Vito, S. et al., *"On field calibration of an electronic nose for benzene estimation in an urban pollution monitoring scenario"*, Sensors and Actuators B: Chemical, 129(2), 2008.
>
> License: for research purposes only; commercial use is excluded.

##  Project Goals

This analysis explores two questions:

1. **The city's story** — How do traffic patterns, time of day, day of week, and seasons affect air pollution?
2. **The sensor's story** — Are low-cost metal-oxide sensors reliable substitutes for certified reference analyzers? Do they suffer from cross-sensitivity or drift over time?

##  Project Structure

```
.
├── AirQualityUCI.xlsx          # Raw dataset
├── Air_Quality_UCI_EDA.ipynb              # Full annotated analysis notebook
└── README.md
```

##  Tech Stack

- **Python 3**
- **pandas** — data loading, cleaning, and aggregation
- **numpy** — numerical operations
- **matplotlib** / **seaborn** — data visualization
- (optional) **statsmodels**, **scipy** — required for `sns.residplot(lowess=True)` and `sns.clustermap`

## ▶ Getting Started

```bash
# clone the repo
git clone https://github.com/romina1831/Air-Quality-UCI-EDA.git
cd Air-Quality-UCI-EDA

# install dependencies
pip install pandas numpy matplotlib seaborn openpyxl statsmodels scipy

# launch the notebook
jupyter notebook Air-Quality-UCI-EDA.ipynb
```

##  Analysis Overview

| Section | Question | Chart |
|---|---|---|
| Data quality | How much data is missing, and where? | `sns.barplot` |
| Distributions | What shape does each pollutant's distribution take? | `sns.histplot` + KDE |
| Daily rhythm | How does CO vary by hour of day? | `sns.boxplot` |
| Weekday vs. weekend | Does the daily pattern change on weekends? | `sns.lineplot` |
| Seasonality | Which season is most polluted? | `sns.violinplot` |
| Hour × weekday | Combined view of daily and weekly patterns | `sns.heatmap` |
| Monthly trend | How does pollution evolve across the year? | `sns.lineplot` (normalized) |
| Weather effects | How do temperature and humidity relate to pollution? | `sns.regplot`, `sns.jointplot` |
| Sensor validation | How well do raw sensors track reference values? | `sns.heatmap` (correlation) |
| Cross-sensitivity | Do sensors respond to more than their target gas? | `sns.pairplot` |
| Sensor drift | Does sensor accuracy degrade over the year? | `sns.lineplot` (rolling correlation) |
| Residual analysis | Where does the sensor over/under-estimate? | `sns.residplot` |
| Pollutant relationships | How do pollutants correlate with each other? | `sns.clustermap`, `sns.jointplot` |

##  Key Findings

- **Data quality matters first**: `NMHC(GT)` is missing in ~90% of records and was excluded from analysis; other reference columns are missing in 15–18% of records.
- **Traffic drives pollution**: CO and NOx show clear double peaks at 8–9 AM and 6–8 PM on weekdays, closely tracking commute hours; this pattern flattens significantly on weekends.
- **Cold, humid weather traps pollution**: pollutant concentrations rise in autumn/winter, consistent with temperature inversion effects that prevent dispersion; a sharp drop occurs in August, likely due to summer holidays.
- **Most low-cost sensors correlate well** with their reference counterparts (r ≈ 0.85–0.90), but **`PT08.S3(NOx)` shows a strong *negative* correlation** with true NOx — a textbook example of cross-sensitivity in metal-oxide sensors.
- **Sensor accuracy drifts over the year**: the correlation between `CO(GT)` and `PT08.S1(CO)` declines from ~0.95 in spring to ~0.84 in winter, suggesting the sensor needs periodic recalibration.
- **Sensors saturate at high concentrations**: residual analysis shows the CO sensor systematically underestimates true concentration once CO exceeds ~6 mg/m³.

##  License

This project is for educational/research purposes, in line with the original dataset's license (non-commercial use only).

##  Author

Personal project, built for educational purposes.

