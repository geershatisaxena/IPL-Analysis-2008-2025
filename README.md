🏏 IPL Data Analysis (2008 - 2025)

An enterprise-grade Exploratory Data Analysis (EDA) of the Indian Premier League (IPL) matches, player metrics, and team trends spanning 18 seasons (2008 to 2025). This repository implements advanced data wrangling, feature engineering, and high-impact statistical visualizations.

📌 Features & Core Insights

Team Domination Matrix: Win/loss ratio profiling, championship conversions, and home-ground advantage trends.

Player Performance Modeling: Batting Strike Rate vs. Consistency indexes, Bowler Economy vs. Wickets maps.

Contextual Factors: Multi-variable analysis on Toss Influence, Venue scoring patterns, and DLS (Duckworth-Lewis-Stern) impact.

Temporal Trends: Tracking how average first-innings scores and team strategy (chasing vs. defending) have evolved from 2008 to 2025.

💻 Code Showcase: Generating Toss Decision Trends

The following production-ready Python script is used to analyze and visualize how toss decisions have evolved over the years. This can be executed directly from your local setup:

import os
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

# Configure global visualization style
sns.set_theme(style="whitegrid")
plt.rcParams.update({
    'font.size': 12,
    'axes.labelsize': 14,
    'axes.titlesize': 16,
    'xtick.labelsize': 11,
    'ytick.labelsize': 11,
    'figure.figsize': (14, 7)
})

def plot_toss_trends(filepath):
    """
    Loads IPL match data and saves a stacked percentage bar plot of toss trends.
    """
    if not os.path.exists(filepath):
        raise FileNotFoundError(f"Dataset not found at {filepath}")
        
    # Read the match-by-match metadata
    df = pd.read_csv(filepath)
    
    # Calculate percentage distribution of toss decisions per season
    toss_pivot = (
        df.groupby('season')['toss_decision']
        .value_counts(normalize=True)
        .unstack() * 100
    )
    
    # Plot configuration
    fig, ax = plt.subplots()
    colors = ['#1f77b4', '#ff7f0e'] # High-contrast professional palette
    
    toss_pivot.plot(
        kind='bar', 
        stacked=True, 
        color=colors, 
        width=0.75, 
        ax=ax, 
        edgecolor='black', 
        linewidth=0.7
    )
    
    # Customizing axes and titles
    ax.set_title("IPL Toss Decision Evolution (2008 - 2025)", pad=20, weight='bold')
    ax.set_ylabel("Decision Percentage (%)")
    ax.set_xlabel("IPL Season")
    ax.legend(["Field First", "Bat First"], bbox_to_anchor=(1.02, 1), loc='upper left')
    
    # Add percentage labels directly onto the bar elements
    for container in ax.containers:
        ax.bar_label(container, fmt='%.1f%%', label_type='center', color='white', weight='bold', fontsize=9)
        
    plt.tight_layout()
    
    # Save visualization to output directory
    os.makedirs('plots', exist_ok=True)
    output_path = 'plots/toss_decision_trends.png'
    plt.savefig(output_path, dpi=300)
    print(f"[✓] Toss trend visualization successfully exported to: {output_path}")
    plt.close()

if __name__ == "__main__":
    plot_toss_trends('data/ipl_matches_2008_2025.csv')


📂 Repository Architecture

├── data/
│   ├── ipl_matches_2008_2025.csv       # Match-level details (Teams, Toss, Results, Venue)
│   └── ipl_deliveries_2008_2025.csv    # Ball-by-ball performance metrics
├── notebooks/
│   └── ipl_exploratory_analysis.ipynb  # Documented Jupyter notebooks detailing EDA workflow
├── plots/                              # Generated high-resolution static graphs
│   ├── toss_decision_trends.png
│   └── bowler_economy_vs_strike.png
├── requirements.txt                    # Python environment dependencies
└── README.md                           # Documentation


🛠️ Setup & Installation

Prerequisites

Python 3.9 or higher installed.

Installation Steps

Clone the repository:

git clone https://github.com/your-username/ipl-data-analysis-2008-2025.git
cd ipl-data-analysis-2008-2025


Establish a virtual environment:

python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate


Install exact dependencies:

pip install --upgrade pip
pip install -r requirements.txt


Execute the analysis scripts:

python scripts/generate_plots.py


📊 Sample Output Metrics

A snapshot of the computed insights available in the notebook:

Metric

Historical Value / Team

Season / Player

Highest Team Scoring Innings

287/3 (SRH vs RCB)

2024

Most IPL MVP Titles

Shane Watson & Sunil Narine (2)

All-Time

Most Successful Toss Strategy

Field First (Win Rate: ~54.2%)

All-Time Trend

🤝 Contributing & License

Feel free to fork this project, open issues, or submit Pull Requests for enhancements (such as predictive modeling for IPL 2026/2027 matches using Scikit-Learn).

Distributed under the MIT License. See LICENSE for more information.
