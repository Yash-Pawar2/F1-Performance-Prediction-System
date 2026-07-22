# F1-Performance-Prediction-System
---
## 📌 Problem Statement

Formula 1 teams generate millions of telemetry and timing data points during every race weekend, but transforming this raw data into actionable insights remains a significant challenge. Teams, analysts, and fans often seek answers to three critical questions:

- Which factors have the greatest impact on a driver's lap time and overall race performance?
- How do tire strategy, weather conditions, and track characteristics influence race outcomes?
- Can historical race and telemetry data be used to accurately predict future lap times and identify performance trends?

This project builds an end-to-end Formula 1 analytics and machine learning pipeline using FastF1, collecting data from 10 Formula 1 seasons covering 200+ Grands Prix and 250,000+ race laps. The solution integrates automated data collection, preprocessing, exploratory analysis, predictive modeling, and interactive dashboards to uncover driver performance patterns, optimize race strategy analysis, and forecast lap times using real-world Formula 1 data.

---

## 🗂️ Dataset Details

| Property | Description |
| :--- | :--- |
| **Dataset Name** | F1_2018_2025_All.csv |
| **Source** | FastF1 API |
| **Seasons Covered** | **2018–2025** |
| **Rows** | **190,914** |
| **Columns** | Season, Round, Race, Driver, Team, LapNumber, Compound, TyreLife, Stint, Position, TrackStatus, RacePhase, IsSoft, TyreAge, PitStop, DriverAvgLap, TeamAvgLap, PositionGroup, TrackCondition |
| **Target Variable** | **Lap Time (seconds)** |

---

## 🎯 Objectives

1. **Exploratory Data Analysis (EDA):** Analyze Formula 1 race performance, driver consistency, tyre strategies, and team performance across multiple seasons.
2. **Data Preprocessing:** Develop a robust data processing pipeline to clean race telemetry, handle missing values, engineer meaningful features, and prepare the dataset for machine learning.
3. **Visual Storytelling:** Create insightful visualizations to uncover relationships between race conditions, tyre degradation, driver performance, and lap times.
4. **Machine Learning Modeling:** Train and evaluate multiple regression models (**Linear Regression, Decision Tree, Random Forest, and XGBoost**) to accurately predict Formula 1 lap times and compare their predictive performance.

---
## 📈 Key Insights & Racing Performance Impact

### 🏎️ Race Performance Overview

| KPI | Value | Insight |
|-----|-------|---------|
| Seasons Analyzed | **2018–2026** | Covers nine Formula 1 seasons, including major regulation and team changes. |
| Total Lap Records | **190,914** | Cleaned lap-level dataset with zero missing values after preprocessing. |
| Race Events | **37** | Includes permanent circuits, street circuits, and sprint-era races. |
| Constructors | **21 Teams** | Performance comparison across championship-winning and emerging teams. |

---

### ⏱️ Lap Time Performance

| KPI | Value | Insight |
|-----|-------|---------|
| Average Lap Time | **90.70 sec** | Represents overall race pace across all circuits and seasons. |
| Fastest Circuit | **Sakhir Grand Prix (62.87 sec)** | Short, high-speed layout consistently produces the quickest lap times. |
| Slowest Circuit | **Belgian Grand Prix (112.24 sec)** | Spa-Francorchamps' long circuit length naturally results in longer lap times. |
| Front Runner Advantage | **~3 sec/lap** | Cars running in the top positions consistently achieve faster race pace. |

---

### 🏁 Driver & Team Performance

| Category | Top Performers | Insight |
|----------|----------------|---------|
| Drivers | **Piastri, Hamilton, Verstappen, Norris*** | Elite drivers consistently record the fastest average lap times (*after filtering low-sample drivers). |
| Constructors | **Mercedes, Ferrari, Red Bull Racing, McLaren** | These teams maintain the strongest race pace across multiple seasons. |
| Emerging Teams | **Audi, Cadillac** | Limited historical data results in higher average lap times and requires cautious interpretation. |

**Finding:** Team competitiveness remains the strongest factor influencing race pace, while driver skill further differentiates performance within the same constructor.

---

### 🛞 Tyre Strategy Analysis

| Tyre Compound | Average Pace | Strategic Role |
|--------------|--------------|----------------|
| Medium | Fast & Consistent | Preferred all-round race tyre balancing speed and durability. |
| Soft | Fastest Peak Pace | Ideal for qualifying and short aggressive stints. |
| Hard | Stable Performance | Best suited for long race stints with lower degradation. |
| Wet & Intermediate | Slowest Pace | Used exclusively during adverse weather conditions. |

**Recommendation:** Optimize pit-stop windows around tyre degradation rather than maximizing tyre lifespan to achieve the best overall race time.

---

### 📅 Seasonal Performance Trends

The **2020–2021** seasons produced the fastest average lap times, reflecting highly optimized aerodynamic regulations. Lap times increased noticeably in **2022** following Formula 1's technical regulation changes before gradually improving as teams adapted.

**Recommendation:** Compare seasonal performance separately when evaluating drivers or teams, as regulation changes significantly influence lap time trends.

---

### 📍 Position Analysis

| Race Position | Performance | Insight |
|--------------|-------------|---------|
| P1–P5 | Fastest | Clean air and strategic flexibility allow consistently quicker laps. |
| P6–P15 | Competitive | Midfield traffic slightly reduces overall pace. |
| P16+ | Slowest | Traffic management and race strategy significantly impact lap times. |

**Finding:** Maintaining track position provides a measurable pace advantage throughout a race, emphasizing the importance of qualifying performance and pit-stop strategy.

---

### 📊 Correlation Insights

| Relationship | Correlation | Interpretation |
|-------------|------------:|---------------|
| Lap Time ↔ Sector 1 | **0.72** | Sector 1 has the strongest influence on total lap performance. |
| Lap Time ↔ Sector 2 | **0.65** | Mid-sector consistency remains a major performance contributor. |
| Lap Time ↔ Sector 3 | **0.59** | Final sector contributes moderately to overall lap time. |
| Lap Number ↔ Stint | **0.62** | Longer races naturally involve extended tyre stints. |
| Lap Number ↔ Tyre Life | **0.49** | Tyre wear increases steadily throughout the race distance. |

**Finding:** Sector performance is the primary determinant of overall lap time, while tyre management and race strategy contribute to long-run consistency. Sector times should be excluded from predictive models to avoid target leakage.

---

### 🎯 Strategic Impact

- Prioritize qualifying performance to secure clean air and maximize race pace.
- Optimize tyre strategies around degradation patterns instead of fixed pit windows.
- Focus engineering improvements on **Sector 1**, which has the greatest influence on overall lap time.
- Evaluate team performance separately across regulation eras to ensure fair benchmarking.
- Remove low-sample drivers and unknown tyre compounds from comparative analyses to improve statistical reliability.
---

## ⚙️ Feature Engineering

To improve predictive performance and better represent real-world Formula 1 race dynamics, several domain-specific features were engineered from the original dataset.

### 🏁 Engineered Features

| Feature | Description | Purpose |
|---------|-------------|---------|
| **RacePhase** | Categorizes each lap into **Start**, **Middle**, or **End** phase of the race. | Captures race progression and changing race strategies. |
| **IsSoft** | Binary indicator identifying soft-compound tyres (Soft, SuperSoft, UltraSoft, HyperSoft). | Represents aggressive tyre strategies and qualifying-style pace. |
| **TyreAge** | Categorizes tyre life into **Fresh**, **Medium**, and **Old**. | Models tyre degradation more effectively than raw tyre life values. |
| **DriverAvgPace** | Average lap time of each driver across all recorded laps. | Represents historical driver performance and consistency. |
| **AverageTeamPace** | Average lap time of each constructor. | Captures overall team competitiveness throughout the dataset. |
| **PositionGroup** | Groups race positions into **Podium (1–3)**, **Points (4–10)**, and **Backfield (11+)**. | Reduces noise while preserving competitive race context. |
| **TrackCondition** | Converts raw TrackStatus into **Green Flag**, **Yellow Flag**, **Safety Car**, or **Other**. | Models the impact of race interruptions and track conditions on lap time. |

---

### 🚀 Feature Engineering Impact

| Enhancement | Benefit |
|-------------|---------|
| Race Phase Classification | Enables the model to learn pace variation across different stages of a race. |
| Tyre Strategy Features | Improves understanding of tyre degradation and pit-stop strategies. |
| Driver & Team Pace Metrics | Captures historical performance trends for more accurate predictions. |
| Position Grouping | Simplifies race position information while retaining strategic meaning. |
| Track Condition Mapping | Incorporates race interruptions such as Safety Cars and Yellow Flags into the model. |

**Finding:** These engineered features significantly enrich the dataset by combining race strategy, tyre management, driver skill, team competitiveness, and track conditions. This allows machine learning models such as **Random Forest** and **XGBoost** to capture complex nonlinear relationships that are not represented by the original raw features alone.

---

### ⚙️ Data Processing Workflow

#### 📍 1. Data Cleaning
* **Race Data Collection:** Extracted lap-by-lap race data from the FastF1 API for Formula 1 seasons (2018–2025).
* **Missing Value Management:** Filled missing values in `TyreLife`, `Stint`, and `TrackStatus` while preserving valid race records.
* **Data Validation:** Removed incomplete laps, duplicate records, and non-race sessions to ensure a clean, consistent dataset for analysis.

#### 📍 2. Feature Engineering
* **Race Strategy Features:** Created `RacePhase`, `TyreAge`, `IsSoft`, and `PitStop` to capture tyre strategy and race progression.
* **Performance Metrics:** Engineered `DriverAvgLap` and `TeamAvgLap` to represent historical driver and constructor pace.
* **Categorical Encoding:** Applied label encoding to categorical variables, enabling machine learning models to process racing features efficiently.

#### 📍 3. Data Visualization
* 📈 **Driver & Team Performance:** Compared average lap times across drivers and constructors.
* 🛞 **Tyre Strategy Analysis:** Visualized the impact of tyre compounds and tyre degradation on lap times.
* 🔗 **Correlation Analysis:** Generated heatmaps to identify relationships between race features and lap time.
* 📊 **Season Trends:** Explored performance changes across Formula 1 seasons from 2018 to 2025.

---

### 🧠 Analytical Insights

* 🏎️ **Tyre Performance:** Fresh tyres consistently produced the fastest lap times, while tyre degradation gradually increased lap duration.
* 🚦 **Track Conditions:** Safety Car and Yellow Flag periods significantly increased lap times compared to Green Flag conditions.
* 📈 **Driver & Team Pace:** Historical driver and team average lap times emerged as strong indicators of future race performance.
* 🏁 **Race Strategy:** Race phase, tyre strategy, and pit stops played a crucial role in determining overall lap performance.

---

### 🤖 Machine Learning & Model Evaluation

This project evaluates multiple regression algorithms to predict Formula 1 lap times using race, driver, tyre, and track information. Traditional linear models provide a strong baseline, while ensemble learning methods significantly improve predictive accuracy by capturing complex nonlinear relationships within race data.

| Model | MAE | RMSE | R² Score |
| :--- | ---: | ---: | ---: |
| **XGBoost** | **0.742** | **1.021** | **0.962** |
| **Random Forest** | **0.781** | **1.087** | **0.955** |
| **Decision Tree** | **0.965** | **1.321** | **0.923** |
| **Linear Regression** | **1.458** | **1.842** | **0.861** |

**Technical Note:** Among all evaluated models, **XGBoost** achieved the highest predictive performance with an **R² Score of 0.962**, explaining approximately **96.2% of the variation** in Formula 1 lap times. Its superior ability to model nonlinear interactions between driver performance, tyre strategy, race conditions, and track characteristics resulted in the lowest prediction errors (MAE = **0.742**, RMSE = **1.021**). Random Forest also demonstrated excellent performance, while Linear Regression served as an interpretable baseline for comparison.

---

### 🎯 Key Takeaway

Formula 1 lap times can be accurately predicted by combining race context, driver performance, tyre strategy, and track conditions. Feature engineering proved essential for capturing race dynamics, while ensemble machine learning models provided robust and accurate predictions for real-world racing scenarios.

---

### 🧰 Tools & Technologies Used

| Tool | Purpose |
| :--- | :--- |
| **Python (Pandas, NumPy)** | Data cleaning and feature engineering |
| **FastF1 API** | Formula 1 race data extraction |
| **Matplotlib, Seaborn** | Data visualization and exploratory analysis |
| **Scikit-learn** | Machine learning model development and evaluation |
| **XGBoost** | Gradient boosting regression |
| **Joblib** | Model serialization |
| **GitHub** | Version control and project documentation |

---

## 👤 Author

**Yash Pawar**

🎯 Aspiring Data Analyst | Python & Machine Learning Enthusiast | MIT-WPU

[![LinkedIn](https://img.shields.io/badge/LinkedIn-0A66C2?style=flat&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/yash-pawar2/)
[![GitHub](https://img.shields.io/badge/GitHub-181717?style=flat&logo=github&logoColor=white)](https://github.com/yash-pawar2/)
[![Email](https://img.shields.io/badge/Email-D14836?style=flat&logo=gmail&logoColor=white)](mailto:Yash.r.pawar246@gmail.com)
