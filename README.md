# Finnish NHL Players: A Zone-Level Shooting Efficiency Analysis
xG analysis comparing Finnish players' shooting efficiency to other top professionals. Data from seasons 22-23, 23-24 and 24-25

![Status](https://img.shields.io/badge/Status-In%20Progress-yellow)
![Python](https://img.shields.io/badge/Python-3.11%2B-blue)
![Data Source](https://img.shields.io/badge/Data-MoneyPuck-green)

## Project Overview
This project investigates whether Finnish NHL players exhibit systematic zone-specific shooting efficiency patterns relative to all other NHL players, potentially providing insight into broader trends in Finnish player development. Expected Goals (xG) is used as the benchmark. The project uses regular season data from seasons 2022-2023, 2023-2024 and 2024-2025. 

This project doesn't look into individual Finnish players but rather investigates whether there is a structural nationality-level pattern among Finnish NHLers and how they convert goal-scoring opportunities from different shooting zones. If there is a clear pattern it carries direct implications for player development practices in Finnish ice hockey. 

## Research Questions
- Do Finnish NHL players systematically overperform or underperform expected goal models relative to the rest of the NHL?
- Are these differences zone-specific and if so, which zones show these signals?
- If there is a pattern, is it recognizable across all seasons or does an outlier year cause this?

## Methodology

### Data Source
MoneyPuck (moneypuck.com) - shot-level data which includes xG values, shot coordinates, shot outcomes and player metadata for all NHL regular season games across the scope period.

### Inclusion Criteria
All NHL players across the league are included under the following criteria:

| Criterion | Value | Rationale |
|-----------|-------|-----------|
| Seasons   | 22-23, 23-24, 24-25 | Three seasons give a big enough sample size to smooth out randomness 
| Game type | Regular season only | Eliminates playoff sample size imbalance across players 
| Shot definition | All unblocked shot attempts | Blocked shots are excluded as they are not assigned xG values
| Minimum threshold | 200 unblocked shot attempts across the defined seasons | Eliminates part-time players to keep a certain standard across the pool

### Metrics

| Metric | Definition |
|--------|------------|
| xG | Expected goals - probability of a shot resulting in a goal, based on location, shot type and game state
| Goals - xG | Raw efficiency delta - positive value = overperformance, negative value = underperformance
| (Goals - xG) / xG | Relative efficiency, which normalizes for shot volume to allow better comparison
| Shooting sector efficiency | Goals - xG calculated within each zone

### Comparison Structure
- Primary comparison: Finnish players vs. all other NHL players meeting the defined criteria
- Aggregation level: Finland as a nationality group - individual results are secondary to group level findings
- Causal interpretation: Correlation. Zone-specific efficiency differences between Finland and rest of the population reflect observable patterns in the data. Causal interpretations would require additional evidence to development systems which is beyond the scope of this analysis.

### Shooting Zone Definitions

Zones are defined using NHL standard arena-adjusted coordinates (x, y), 
where the offensive zone starts at x > 25 and the net is at x = 89.

| Zone | Definition | Shot type |
|------|-----------|-----------|
| Slot | x ≥ 69 and within 22 feet of center (∣y∣ ≤ 22) | High-danger, close-range shots directly in front of the net |
| Perimeter | Offensive zone outside the slot (x ≥ 54, outside slot bounds) | Mid-range shots from the sides and corners |
| Point | Blue line and above (x < 54) | Long-range shots from defenders at the blue line |

### Statistical Approach

- Shooting efficiency metrics are calculated at the nationality group level,
  not per individual player
- Bootstrapped confidence intervals are used to quantify uncertainty in the estimated efficiency differences while reflecting the sample sizes of each group.
- Season-over-season consistency is checked for all findings. A pattern that
  appears in all three seasons is treated as structural, while a pattern driven
  by a single season is treated as noise

## Project Structure

```
analysis-on-finnish-nhlers-shooting-efficiency/
│
├── data/
│   ├── raw/               # Original data which was never modified
│   └── processed/         # Cleaned data ready for analysis
│
├── notebooks/
│   ├── 01_data_acquisition.ipynb   # Data loading and validation
│   ├── 02_eda.ipynb                # Exploratory data analysis
│   ├── 03_player_analysis.ipynb    # xG efficiency by nationality
│   └── 04_zone_analysis.ipynb      # Zone-level comparison
│
├── src/
│   ├── data_loader.py
│   ├── preprocessing.py
│   ├── analysis.py
│   └── visualization.py
│
├── visualizations/
├── reports/
├── docs/
│   └── AI_WORKFLOW.md
│
├── requirements.txt
├── .gitignore
└── README.md
```

## Tools

| Tool | Purpose |
|------|---------|
| Python 3.11 | Core language |
| pandas | Data manipulation and aggregation |
| scipy | Statistical testing and confidence intervals |
| plotly / matplotlib | Visualizations |
| Jupyter Notebook | Interactive analysis environment |
| Git / GitHub | Version control and portfolio presentation |

## Limitations

- xG models are estimates. MoneyPuck's model is well-regarded but not 
  perfect. Results should be read as relative to the model, not as 
  absolute measures of shooting skill
- Shot coordinate data has minor recording inconsistencies across NHL arenas.
  Arena adjustment partially corrects for this
- Nationality-level analysis hides individual variation. A Finnish player
  who is excellent from the slot is averaged together with one who struggles
- Three seasons is enough to identify medium-term patterns, but a longer 
  window would give a clearer picture of structural tendencies
- This analysis cannot establish causation. Any patterns found reflect 
  what the data shows, not why it happens

## Author

Juuso Forsman 
BSc, Information and Service Management at Aalto University  
Incoming MSc (sep. 2026-), Business Analytics at Aalto University  

## Data

Shot data from [MoneyPuck](https://moneypuck.com). 
Free to use for non-commercial and research purposes, credit MoneyPuck.com.

## Analytcs Skills Demonstrated
- Data cleaning and processing
- Exploratory data analysis
- Statistical inference and uncertainty estimation
- Group-level comparative analysis
- Data visualization
- Reproducible analytical workflows


