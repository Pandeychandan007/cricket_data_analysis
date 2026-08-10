# Cricket data analysis

## Problem Statement

> "We don't know the strengths and weaknesses of our opponents, but give me the best 11 from this planet."

This dashboard helps a team management group build the best possible T20 playing XI using pure statistics rather than reputation or gut feeling — evaluating 219 players from 16 teams across 45 T20 World Cup matches. Two constraints framed the analysis: the team should be able to score at least 180 runs on average, and defend 150 runs on average.

Since role-specific stat thresholds were used to shortlist players (rather than one blanket criterion for everyone), the resulting XI balances explosive top-order batting, steady middle-order anchoring, death-overs finishing, all-round utility, and disciplined fast bowling.

## Steps Followed

- **Step 1**: Loaded 4 linked CSV tables into Power BI Desktop — match summary (45 matches), player bios (219 players), batting summary (699 records), and bowling summary (500 records).
- **Step 2**: Opened Power Query Editor and checked column quality/distribution across all 4 tables; verified no critical nulls in the key stat columns (Runs, Balls Faced, Wickets, Economy).
- **Step 3**: Modeled relationships between the 4 tables using Player ID and Match ID as keys.
- **Step 4**: Defined role-specific selection criteria (documented in a parameter-scoping reference) for 5 player roles:

  | Role | Criteria |
  |---|---|
  | Openers | Batting Avg > 30, Strike Rate > 140, Innings Batted > 3, Boundary % > 50, Batting Position < 4 |
  | Anchors / Middle Order | Batting Avg > 40, Strike Rate > 125, Innings Batted > 3, Avg Balls Faced > 20, Batting Position > 2 |
  | Finishers / Lower Order | Batting Avg > 25, Strike Rate > 130, Innings Batted > 3, Avg Balls Faced > 12, Batting Position > 4, Innings Bowled > 1 |
  | All-Rounders | Batting Avg > 15, Strike Rate > 140, Innings Batted > 2, Batting Position > 4, Innings Bowled > 2, Economy < 7, Bowling Strike Rate < 20 |
  | Specialist Fast Bowlers | Innings Bowled > 4, Economy < 7, Bowling Strike Rate < 16, Bowling Style = "%Fast%", Bowling Average < 20, Dot Ball % > 40 |

- **Step 5**: Built DAX measures for each stat (Batting Average, Strike Rate, Boundary %, Economy, Bowling Strike Rate, Dot Ball %) at the player level.
- **Step 6**: Created 5 report tabs under **Player Analysis** — Power Hitters, Anchors, Finishers, All Rounders, Specialist Fast Bowlers — each showing a ranked table plus trend sparklines (Batting Avg, Strike Rate, Avg Balls Faced, Boundary %) and a scatter plot (e.g. Strike Rate vs Batting Avg) sized by a combined-performance bubble.
- **Step 7**: Added "Qualifier" / "Super 12" toggle buttons to filter players by tournament stage.
- **Step 8**: Built a **Final 11** page with a searchable player list (checkbox selection) that lets a user hand-pick 5–11 players and see a live-updating "Team Performance" summary card (Batting Avg, Strike Rate, Bowling Avg, Bowling S/R, Economy, Dot Ball %).
- **Step 9**: Published the report and cross-checked the Final 11 combined stats against manually filtered totals for a sample 5-player squad.

## Sample Final XI — Combined Team Performance

| Metric | Value |
|---|---|
| Batting Average | 39.60 |
| Strike Rate | 154.54 |
| Average Balls Faced | 19.71 |
| Bowling Average | 14.12 |
| Bowling Strike Rate | 13.09 |
| Economy | 6.47 |
| Dot Ball % | 41.15% |

## Insights

### [1] Dataset Coverage
- 45 matches, 16 teams, 219 players, 699 batting records, 500 bowling records

### [2] Standout Performers by Role
- **Openers**: Rilee Rossouw posts the best strike rate (169.88) among power hitters; Quinton de Kock leads boundary % (75.81%)
- **Anchors**: Suryakumar Yadav's 189.68 strike rate is the highest of any anchor/middle-order player analyzed; Virat Kohli leads batting average (98.67)
- **Finishers**: Curtis Campher tops the finisher group on strike rate (163.64)
- **All-Rounders**: Rashid Khan leads on strike rate (178.13) despite the highest economy (6.42) in the group
- **Fast Bowlers**: Anrich Nortje posts the best economy (5.37) and dot ball % (55.24%) among specialist fast bowlers

### [3] Other Insights
- Combining role-based filters produces a squad that comfortably clears the project's own benchmark (180+ runs scored, defend 150+ on average).
- The Final 11 tool lets selectors swap individual players in/out and immediately see the impact on team-level batting and bowling averages — useful for what-if squad planning.

These stats will change if the Qualifier/Super 12 toggle or Final 11 selection is changed.
