# 2022-World-Cup-An-Event-Level-Football-Analytics-Using-StatsBomb-Open-Data
### Introduction

The 2022 FIFA World Cup in Qatar featured 32 national teams competing at the highest level of international football, producing rich event-level data that captures tactical decisions, player actions, and match dynamics.

This project leverages StatsBomb Open Data to conduct a comprehensive football analytics study of the tournament. Using modern data science techniques and pitch-based visualizations with mplsoccer, the analysis translates complex event data into clear, interpretable insights aligned with professional broadcast and club-level analysis standards.

---
### Project Objectives

- Analyze team and player performance using event-level football data

- Visualize tactical structures such as average player positions and passing networks

- Compare finalists (Argentina vs France) in the 2022 World Cup Final

- Evaluate goal patterns and finishing efficiency across the tournament

- Demonstrate professional football analytics workflows using Python.

---
### Data Source

- StatsBomb Open Data

- Competition: FIFA World Cup 2022

- Data Type: Event-level match data (passes, shots, pressures, carries, xG, etc.)

StatsBomb data provides detailed spatial and temporal information for every on-ball and off-ball action.

---
### Tools & Libraries

Python

  - pandas – data manipulation

  - numpy – numerical analysis

  - matplotlib – data visualization

  - mplsoccer – football pitch visualizations

---
### Analysis Workflow

### Data Preparation

  - Loaded StatsBomb event data

  - Structured events into pandas DataFrames

  - Extracted spatial coordinates for pitch-based analysis

  - Filtered relevant football actions

---
```python
# Import required libraries

from statsbombpy import sb
import pandas as pd
import numpy as np
from mplsoccer import Pitch
import matplotlib.pyplot as plt

# Get competion
competitions = sb.competitions()

# Filter world cup 2022
wc_2022 = competitions[
    (competitions["competition_name"] == "FIFA World Cup") &
    (competitions["season_name"] == "2022")
]

# Load matches
matches = sb.matches(
    competition_id=wc_2022.iloc[0]["competition_id"],
    season_id=wc_2022.iloc[0]["season_id"]
)

# Pick one match
match_id = matches.iloc[0]["match_id"]

# Load event level data
events = sb.events(match_id=match_id)

```
*Successfully loaded 64 matches with 234,652 events*

---
### Key Analyses Performed
### Average Player Positions (Team Structure) - Argentina VS France

- Computed average on-ball positions for each player for the finalists - Argentina VS France

- Bubble size represents on-ball involvement

- Tactical shape visualization using StatsBomb pitch dimensions

*![Average Player position](https://github.com/Uzo-Hill/2022-World-Cup-An-Event-Level-Football-Analytics-Using-StatsBomb-Open-Data/blob/main/Project%20Image/AvgPosition_Arg_Fra.png)*

Finalists Comparison: Argentina vs France

- Argentina deployed a compact 4-3-3 with Messi operating high on the right flank

- France utilized a 4-2-3-1 formation with Mbappé positioned wide on the left

- Argentina's midfield trio showed stronger central control compared to France's double pivot

---
### Passing Networks Analysis

- Constructed passing networks based on pass frequency for Argentina VS France

- Node size represents player involvement

- Edge thickness represents pass volume between players

Key Observations

- Argentina showed a dense and well-connected passing structure

- France’s network was more segmented, relying on direct connections

*![Pass Network](https://github.com/Uzo-Hill/2022-World-Cup-An-Event-Level-Football-Analytics-Using-StatsBomb-Open-Data/blob/main/Project%20Image/PassNetworks_Arg_Fra.png)*

---

### xG Timeline : Argentina VS France
Which team created better chances throughout the game?

*![xG Arg VS Fra](https://github.com/Uzo-Hill/2022-World-Cup-An-Event-Level-Football-Analytics-Using-StatsBomb-Open-Data/blob/main/Project%20Image/xG_Arg_Fra.png)*

Key Insights:

- Argentina dominated the first half with significantly higher xG accumulation, creating multiple quality chances before the 45th minute while France struggled to generate threatening opportunities.

- France's xG remained flat for most of regulation time until a dramatic surge from minute 80, indicating they created very few quality chances during the 90 minutes but came alive in the extended period.

- The steep rise in both teams' xG during extra time (minutes 90-120) shows the final period was end-to-end with both sides creating high-quality scoring opportunities, reflecting the dramatic 3-3 scoreline before penalties shootout.

---

### Tournament-Wide Statistics

### Goals by Match Period
When Do Goals Happen Most? Scoring Patterns Across Match Periods.

*![Goals by minute](https://github.com/Uzo-Hill/2022-World-Cup-An-Event-Level-Football-Analytics-Using-StatsBomb-Open-Data/blob/main/Project%20Image/Goals_By_Match_Periods.png)*

Patterns Found:
- Goals peak just before halftime (31–45 minutes), suggesting teams increase attacking intensity as the first half draws to a close.

- The early second half (46–75 minutes) remains highly productive for goals scored, reflecting tactical adjustments and increased tempo after halftime.

- Goal output drops sharply in extra time, indicating fatigue, conservative play, and higher risk management in knockout scenarios.

---

### Conversion Efficiency (Goals vs xG)
Which Teams Had the Best Conversion Rate?

- Comparison of actual goals scored against expected goals (xG) for countries.

*![xG by Country](https://github.com/Uzo-Hill/2022-World-Cup-An-Event-Level-Football-Analytics-Using-StatsBomb-Open-Data/blob/main/Project%20Image/Best_xG_Team.png)*

Key Insights:

- Portugal show the strongest overperformance relative to xG, indicating exceptional finishing efficiency compared to chance quality. England is 2nd with xG of +4.3.

- Argentina and France both exceed their xG totals, combining high chance creation with clinical conversion at the tournament’s highest level.

- Several teams outperform xG by smaller margins, suggesting effective finishing but less consistent chance volume or shot quality.

---

### Where Do Most Goals Come From?
Shot location heatmap for all goals scored in the tournament.

*![Shot Location](https://github.com/Uzo-Hill/2022-World-Cup-An-Event-Level-Football-Analytics-Using-StatsBomb-Open-Data/blob/main/Project%20Image/Goals_Locations.png)*

- The overwhelming majority of goals were scored from inside the penalty area from open play, particularly in central positions near the six-yard box.
- Penalties and free kicks constituted a substantial minority of total goals, highlighting set piece proficiency as a critical tournament success factor.

---

### Goals Distribution by Source
How effective were set pieces vs open play goals?

*![Set Piece VS Open play](https://github.com/Uzo-Hill/2022-World-Cup-An-Event-Level-Football-Analytics-Using-StatsBomb-Open-Data/blob/main/Project%20Image/SetPiece_VS_OpenPlay.png)*

- Nearly 77% of World Cup goals came from open play

- Penalties accounted for 22.1% of all goals, making penalty-area incursions and defensive discipline critical tournament factors.
- Only 1% of goals were scored as free kick.

---
### Average Possession & Passes

*![Team possession](https://github.com/Uzo-Hill/2022-World-Cup-An-Event-Level-Football-Analytics-Using-StatsBomb-Open-Data/blob/main/Project%20Image/Team_Possession_Passes.PNG)*


*![Top Passers](https://github.com/Uzo-Hill/2022-World-Cup-An-Event-Level-Football-Analytics-Using-StatsBomb-Open-Data/blob/main/Project%20Image/Top_Passers.PNG)*

---

### Key Player Comparison (Messi vs Mbappé)

- Shot map comparison

- Metrics comparison

*![Messi & Mbappe](https://github.com/Uzo-Hill/2022-World-Cup-An-Event-Level-Football-Analytics-Using-StatsBomb-Open-Data/blob/main/Project%20Image/ShotMap_Messi_Mbappe.png)*

*![Metrics](https://github.com/Uzo-Hill/2022-World-Cup-An-Event-Level-Football-Analytics-Using-StatsBomb-Open-Data/blob/main/Project%20Image/KeyMetrica_Messi_Mbappe.png)*

---
### Key Insights Summary
- Argentina led the tournament with 110 shots, 20.99 xG, and 23 goals
- Portugal showed the strongest xG overperformance (+4.69), followed by England (+4.26)
- Spain dominated ball control (75.3% possession, 978.5 passes/match) but failed to advance deep
- Goals peaked just before halftime (31-45 minutes), with 77% coming from open play vs 23% from set pieces
- Average goal scored from just 10.8 yards, predominantly from central areas inside the penalty box

---
Conclusion
This comprehensive analysis of the 2022 FIFA World Cup successfully demonstrates how modern data science transforms football understanding. By leveraging StatsBomb's event-level data, we've decoded the tactical narratives, performance patterns, and strategic decisions that shaped the tournament's outcome.

Key Achievements
- Built a robust, reproducible analytics pipeline processing 234,652 events across 64 matches
- Created broadcast-quality visualizations matching Sky Sports/BBC analytics formats
- Uncovered actionable patterns in team tactics and player performance.
- Combined football expertise with data science to produce meaningful, interpretable results
---

THANK YOU ...
