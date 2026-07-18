# Finnish NHL Players: A Zone-Level Shooting Efficiency Analysis
xG analysis comparing Finnish players' shooting efficiency to other top professionals. Data from seasons 22-23, 23-24 and 24-25

![Status](https://img.shields.io/badge/Status-Completed-brightgreen)
![Python](https://img.shields.io/badge/Python-3.11%2B-blue)
![Data Source](https://img.shields.io/badge/Data-MoneyPuck-green)

## Project overview
This project investigates whether Finnish NHL players exhibit systematic zone-specific shooting efficiency patterns relative to all other NHL players, potentially providing insight into broader trends in Finnish player development. Expected Goals (xG) is used as the benchmark. The project uses regular season data from seasons 2022-2023, 2023-2024 and 2024-2025. 

This project doesn't look into individual Finnish players but rather investigates whether there is a structural nationality-level pattern among Finnish NHLers and how they convert goal-scoring opportunities from different shooting zones. If there is a clear pattern it could carry direct implications for player development practices in Finnish ice hockey. 

## Research questions
- Do Finnish NHL players systematically overperform or underperform expected goal models relative to the rest of the NHL?
- Are these differences zone-specific and if so, which zones show these signals?
- If there is a pattern, is it recognizable across all seasons or does an outlier year cause this?

## Key findings

**Blue line - statistically significant weakness**

Finnish NHL players show a consistent and statistically significant underperformance from the blue line zone relative to the NHL average:
- Three-season average: -23.1% vs. NHL average
- 95% bootstrapped confidence interval: [-42.2%, -2.4%] (bootstrapped ci's can vary a little between runs due to the randomness of the process) - does not cross zero
- Pattern is consistent and worsening: 2022–23: -9.8%, 2023–24: -30.3%, 2024–25: -32.3%
- Finnish players rank last among all analyzed nationalities in blue line efficiency

**Slot - Positive tendency but not statistically significant**
- Three-season average: +5.5% vs. NHL average
- 95% confidence interval: [-1.7%, +13.2%] - crosses zero
- Consistent across all three seasons - Finnish players rank 1st in slot efficiency across the observed seasons

**Arc and other - no meaningful pattern**
- Three-season average: -1.1% vs. NHL average
- Inconsistent across seasons - no structural pattern identified

## Methodology

### Data source
MoneyPuck (moneypuck.com) - shot-level data which includes xG values, shot coordinates, shot outcomes and player metadata for all NHL regular season games across the scope period.

### Inclusion criteria
All NHL players across the league are included under the following criteria:

| Criterion | Value | Rationale |
|-----------|-------|-----------|
| Seasons   | 22-23, 23-24, 24-25 | Three seasons give a big enough sample size to smooth out randomness 
| Game type | Regular season only | Eliminates playoff sample size imbalance across players 
| Shot definition | All unblocked shot attempts | Blocked shots are excluded as they are not assigned xG values
| Minimum threshold | 1000 unblocked shot attempts across the defined seasons per nation | Eliminates potential misleading results due to a small sample size

### Metrics

| Metric | Definition |
|--------|------------|
| xG | Expected goals - probability of a shot resulting in a goal, based on location, shot type and game state
| Goals - xG | Raw efficiency delta - positive value = overperformance, negative value = underperformance
| (Goals - xG) / xG | Relative efficiency, which normalizes for shot volume to allow better comparison
| Shooting sector efficiency | Goals - xG calculated within each zone

### Comparison structure
- Primary comparison: Finnish players vs. all other NHL players meeting the defined criteria
- Aggregation level: Finland as a nationality group
- Causal interpretation: Correlation. Zone-specific efficiency differences between Finland and rest of the population reflect observable patterns in the data. Causal interpretations would require additional evidence to development systems which is beyond the scope of this analysis.

### Shooting zone definitions

Zones are defined using absolute values of NHL standard arena-adjusted coordinates (x, y), 
where the offensive zone starts at x > 25 and the net is at x = 89.

| Zone | Definition | Shot type |
|------|-----------|-----------|
| Slot | xABS 76-89, yABS < 10 - shots from maximum 4 meters away from the net and maximum 3 meters to the side of the net | High-danger, close-range shots directly in front of the net |
| Arc and other | xABS 41-89 (non-slot), yABS > 10 if xABS > 76 (slot range) - broad variation of shots that are not from blue line or slot | Mid-range shots from the sides and corners |
| Blue line | xABS 25-41 - shots from maximum 5 meters towards the net from blue line | Long-range shots from defenders at the blue line |

### Statistical approach

- Shooting efficiency metrics are calculated at the nationality group level, not per individual player.
- Bootstrapped confidence intervals are used to quantify uncertainty in the estimated efficiency differences while reflecting the sample sizes of each group.
- Season-over-season consistency is checked for all findings. 

## Project structure

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
│   └── 03_zone_analysis.ipynb      # Zone-level comparison
│
├── visualizations/ # Publishable charts
|
├── AI_WORKFLOW.md
├── requirements.txt
├── .gitignore
└── README.md
```

## Tools

| Tool | Purpose |
|------|---------|
| Python 3.11 | Core language |
| pandas | Data manipulation and aggregation |
| matplotlib | Visualizations |
| numpy | Bootstrapping |
| Jupyter Notebook | Interactive analysis environment |
| Git / GitHub | Version control and portfolio presentation |
| Claude | AI-workflows |

## Limitations

- xG models are estimates. MoneyPuck's model is well-regarded but not 
  perfect. Results should be read as relative to the model, not as 
  absolute measures of shooting skill.
- Our zone-definitions cause a systematic bias with the xG model values.
  This was accounted by normalizing the results to NHL averages. 
- Shot coordinate data has minor recording inconsistencies across NHL arenas.
  Arena adjustment partially corrects for this.
- Nationality-level analysis hides individual variation. A Finnish player
  who is excellent from the slot is averaged together with one who struggles.
- Three seasons is enough to identify medium-term patterns, but a longer 
  window would give a clearer picture of structural tendencies.
- This analysis cannot establish causation. Any patterns found reflect 
  what the data shows, not why it happens.

## Author

Juuso Forsman 
BSc., Information and Service Management at Aalto University  
Incoming MSc. (sep. 2026-), Business Analytics at Aalto University  

## Data

Shot data from [MoneyPuck](https://moneypuck.com). 
Free to use for non-commercial and research purposes, credit MoneyPuck.com.


