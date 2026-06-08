# Finnish NHL Players: A Zone-Level Shooting Efficiency Analysis
xG analysis comparing Finnish players' shooting efficiency to other top professionals. Data from seasons 22-23, 23-24 and 24-25

![Status](https://img.shields.io/badge/Status-In%20Progress-yellow)
![Python](https://img.shields.io/badge/Python-3.11%2B-blue)
![Data Source](https://img.shields.io/badge/Data-MoneyPuck-green)

## Project Overview
This project investigates whether Finnish NHL players exhibit systematic zone-specific shooting efficiency patterns relative to all other NHL players, using Expected Goals (xG) as the benchmark. The project uses regular season data from seasons 2022-2023, 2023-2024 and 2024-2025. 

This project doesn't look into individual Finnish players but rather investigates whether there is a structural nationality-level pattern among Finnish NHLers and how they convert goal-scoring opportunities from different shooting zones. If there is a clear pattern it carries direct implications for player development practices in Finnish ice hockey. 

## Research Questions
- Do Finnish NHLers differ from the overall NHL population by a statistically meaningful margin in shooting efficiency (goals - xG)?
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


