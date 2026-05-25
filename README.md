<div align="center">

<img width="100%" src="https://capsule-render.vercel.app/api?type=waving&height=320&color=gradient&customColorList=24,12,20,17,30,6,2&text=IPL%202008-2025%20DATA%20ANALYSIS&fontSize=50&fontColor=ffffff&animation=twinkling&fontAlignY=40&desc=Complete%20Exploratory%20Data%20Analysis%20of%20Indian%20Premier%20League&descAlignY=62"/>

<br>

<img src="https://readme-typing-svg.demolab.com?font=Orbitron&weight=900&size=30&duration=3000&pause=1000&color=FF0000&center=true&vCenter=true&multiline=true&repeat=true&width=1200&height=130&lines=🏏+INDIAN+PREMIER+LEAGUE+ANALYTICS;📊+IPL+2008+TO+2025+COMPLETE+EDA;🚀+Pandas+%7C+NumPy+%7C+Matplotlib+%7C+Seaborn;🔥+Teams+Players+Matches+Records+Insights"/>

<br>

<img src="https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white"/>
<img src="https://img.shields.io/badge/Pandas-150458?style=for-the-badge&logo=pandas&logoColor=white"/>
<img src="https://img.shields.io/badge/NumPy-013243?style=for-the-badge&logo=numpy&logoColor=white"/>
<img src="https://img.shields.io/badge/Matplotlib-11557C?style=for-the-badge"/>
<img src="https://img.shields.io/badge/Seaborn-4C72B0?style=for-the-badge"/>

<br>

<img src="https://img.shields.io/badge/Matches-2000+-orange?style=flat-square"/>
<img src="https://img.shields.io/badge/Seasons-18-success?style=flat-square"/>
<img src="https://img.shields.io/badge/Ball_by_Ball_Data-Available-blue?style=flat-square"/>
<img src="https://img.shields.io/badge/Analysis-Professional-purple?style=flat-square"/>

</div>

---

# 🌈 Overview

<div align="center">

<img src="https://readme-typing-svg.demolab.com?font=Poppins&weight=700&size=25&pause=1000&color=00FFFF&center=true&vCenter=true&width=1000&lines=Discovering+18+Years+of+IPL+History;Uncovering+Winning+Patterns+and+Player+Performance;Transforming+Cricket+Data+Into+Actionable+Insights"/>

</div>

The **Indian Premier League (IPL)** is one of the biggest T20 cricket tournaments in the world.

This project performs a **comprehensive Exploratory Data Analysis (EDA)** on IPL ball-by-ball data from **2008 to 2025** using:

- 📊 Pandas
- 🔢 NumPy
- 📈 Matplotlib
- 🎨 Seaborn

The analysis explores:

- Team performances
- Match trends
- Batting records
- Bowling statistics
- Run scoring patterns
- Wicket distributions
- Venue performance
- Seasonal trends
- Winning strategies

---

# 📂 Dataset Information

## Dataset Columns

| Column | Description |
|----------|-------------|
| match_id | Unique Match Identifier |
| date | Match Date |
| match_type | League / Playoff |
| event_name | IPL Season |
| innings | Innings Number |
| batting_team | Batting Team |
| bowling_team | Bowling Team |
| over | Over Number |
| ball | Ball Number |
| striker | Current Batter |
| bowler | Current Bowler |
| runs_off_bat | Runs Scored |
| extras | Extra Runs |
| wicket_type | Dismissal Type |
| player_dismissed | Dismissed Player |
| team_runs | Team Total Runs |
| team_wicket | Team Wickets |
| batter_runs | Individual Runs |
| batter_balls | Balls Faced |
| bowler_wicket | Bowler Wickets |

---

# 📊 Project Workflow

```text
Raw IPL Dataset
        │
        ▼
Data Cleaning
        │
        ▼
Feature Engineering
        │
        ▼
Exploratory Data Analysis
        │
        ▼
Visualization
        │
        ▼
Insights & Findings
        │
        ▼
Business & Cricket Intelligence
```

---

# 📥 Import Libraries

```python
import pandas as pd
import numpy as np

import matplotlib.pyplot as plt
import seaborn as sns

sns.set_theme(
    style="darkgrid",
    palette="rainbow"
)
```

---

# 🚀 Data Loading

```python
df = pd.read_csv("ipl_2008_2025.csv")

df.head()
```

---

# 🔍 Initial Exploration

## Dataset Shape

```python
df.shape
```

## Dataset Information

```python
df.info()
```

## Missing Values

```python
df.isnull().sum()
```

## Statistical Summary

```python
df.describe()
```

---

# 🧹 Data Cleaning

## Missing Values

```python
df.isnull().sum()
```

## Duplicate Records

```python
df.duplicated().sum()
```

## Convert Date Column

```python
df["date"] = pd.to_datetime(
    df["date"]
)
```

## Extract Season

```python
df["season"] = (
    df["date"]
    .dt.year
)
```

---

# 📈 Exploratory Data Analysis

---

# 🏏 Total Matches Per Season

```python
matches = (
    df.groupby("season")
      ["match_id"]
      .nunique()
)
```

![Matches Per Season](plots/matches_per_season.png)

### Insights

✅ IPL expansion visible

✅ Increase in number of matches

✅ Modern seasons contain significantly more games

---

# 🔥 Runs Scored Per Season

```python
season_runs = (
    df.groupby("season")
      ["runs_off_bat"]
      .sum()
)
```

![Season Runs](plots/runs_per_season.png)

### Findings

🏏 Batting dominance increased over time

🏏 Modern IPL seasons produce larger totals

---

# 🎯 Most Successful Teams

```python
team_runs = (
    df.groupby("batting_team")
      ["runs_off_bat"]
      .sum()
      .sort_values(
          ascending=False
      )
)
```

![Team Runs](plots/team_runs.png)

---

# 🌟 Top Run Scorers

```python
top_batters = (
    df.groupby("striker")
      ["runs_off_bat"]
      .sum()
      .nlargest(15)
)
```

![Top Batters](plots/top_batters.png)

---

# 🚀 Highest Strike Rate Batters

```python
strike_rate = (
    df.groupby("striker")
      .agg({
          "runs_off_bat":"sum",
          "ball":"count"
      })
)
```

![Strike Rate](plots/strike_rate.png)

---

# ⚡ Top Boundary Hitters

```python
fours = (
    df[df["runs_off_bat"] == 4]
)
```

```python
sixes = (
    df[df["runs_off_bat"] == 6]
)
```

![Boundary Analysis](plots/boundary_analysis.png)

---

# 🎳 Highest Wicket Takers

```python
top_bowlers = (
    df.groupby("bowler")
      ["bowler_wicket"]
      .sum()
      .nlargest(15)
)
```

![Top Bowlers](plots/top_bowlers.png)

---

# 💀 Wicket Types Analysis

```python
sns.countplot(
    data=df,
    x="wicket_type"
)
```

![Dismissals](plots/wicket_types.png)

---

# 📊 Over Wise Run Distribution

```python
over_runs = (
    df.groupby("over")
      ["runs_off_bat"]
      .sum()
)
```

![Over Runs](plots/over_runs.png)

### Observation

🔥 Death overs produce maximum scoring.

---

# 🌈 Powerplay vs Middle vs Death Overs

```python
def phase(over):

    if over <= 6:
        return "Powerplay"

    elif over <= 15:
        return "Middle"

    return "Death"
```

![Phase Analysis](plots/phases.png)

---

# 📍 Venue Analysis

```python
venue_runs = (
    df.groupby("venue")
      ["runs_off_bat"]
      .mean()
)
```

![Venue Analysis](plots/venue_analysis.png)

---

# 🔥 Correlation Heatmap

```python
corr = df.select_dtypes(
    include=np.number
).corr()
```

```python
plt.figure(figsize=(12,8))

sns.heatmap(
    corr,
    cmap="rainbow",
    annot=True
)
```

![Heatmap](plots/heatmap.png)

---

# 🌟 Advanced Visualizations

## Pairplot

```python
sns.pairplot(
    df.sample(5000)
)
```

![Pairplot](plots/pairplot.png)

---

## Run Distribution

```python
sns.histplot(
    data=df,
    x="runs_off_bat",
    kde=True
)
```

![Run Distribution](plots/run_distribution.png)

---

## Team Comparison

```python
sns.boxplot(
    data=df,
    x="batting_team",
    y="runs_off_bat"
)
```

![Team Comparison](plots/team_comparison.png)

---

# 🏆 Key Insights

### 🔥 Batting

- Top batters scored more than 7000 IPL runs.
- Strike rates increased significantly after 2018.
- Boundary percentage has continuously increased.

### 🎳 Bowling

- Fast bowlers dominate wicket-taking charts.
- Death overs account for majority of wickets.

### 🏏 Teams

- Certain franchises consistently dominate.
- Home venues influence scoring rates.

### 📈 Trends

- IPL scoring rates increased year after year.
- Average innings totals are at historical highs.

---

# 🎨 Visualization Gallery

| Visualization | Description |
|--------------|-------------|
| Matches Per Season | Tournament growth |
| Team Runs | Franchise comparison |
| Top Batters | Highest run scorers |
| Top Bowlers | Wicket leaders |
| Heatmap | Correlations |
| Venue Analysis | Ground impact |
| Run Distribution | Scoring trends |
| Phase Analysis | Powerplay vs Death Overs |

---

# 🤖 Machine Learning Opportunities

### Future Enhancements

- Match Winner Prediction
- Player Performance Forecasting
- Run Prediction Models
- Wicket Probability Models
- Fantasy Cricket Recommendation System
- Team Strength Index

---

# 🛠 Tech Stack

<div align="center">

| Technology | Usage |
|------------|-------|
| Python | Programming |
| Pandas | Data Processing |
| NumPy | Numerical Computing |
| Matplotlib | Visualization |
| Seaborn | Statistical Visualization |
| Jupyter Notebook | Development |

</div>

---

<div align="center">

<img src="https://capsule-render.vercel.app/api?type=waving&height=250&section=footer&color=gradient&customColorList=24,12,20,17,30,6,2"/>

<img src="https://readme-typing-svg.demolab.com?font=Orbitron&weight=800&size=28&duration=3000&pause=1000&color=39FF14&center=true&vCenter=true&width=1200&lines=THANK+YOU+FOR+VISITING;IPL+2008-2025+DATA+ANALYSIS;DATA+DRIVEN+CRICKET+INTELLIGENCE;PANDAS+•+NUMPY+•+MATPLOTLIB+•+SEABORN"/>

### ⭐ Star this repository if you found it useful ⭐

</div>
