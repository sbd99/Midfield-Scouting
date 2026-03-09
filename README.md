# Midfield Scouting — Top 5 Leagues 2024/25

A data-driven scouting project profiling young midfielders (ages 21–26) across Europe's top five leagues using FBref 2024/25 data. Two analytical frameworks are used to identify the best Deep-Lying Playmakers and Defensive Midfielders.

## Overview

Traditional scouting is subjective and time-consuming. This project applies statistical methods to objectively surface the most promising young midfielders across the Premier League, La Liga, Bundesliga, Serie A, and Ligue 1.

**Filter criteria:** Pure midfielders (Pos = MF), aged 21–26, minimum 1,300 minutes played → 276 qualifying players.

## Analytical Frameworks

### 1. Deep-Lying Playmaker (DLP) — Cosine Similarity
Identifies players stylistically similar to **Vitinha** (PSG) as a prototype DLP. Metrics include progressive passing, ball retention, and build-up involvement. Cosine similarity is used to rank the closest matches across 121 eligible players.

**Top finding:** Angelo Stiller (Stuttgart) identified as the closest Vitinha lookalike.

### 2. Defensive Midfielder (DM) — Composite Z-Score
Ranks players across a composite z-score built from ball-winning metrics: tackles, interceptions, recoveries, and aerial duels.

**Top finding:** Moisés Caicedo (Chelsea) ranked #1 among all eligible DMs.

## Visualisations

- Ranked top 20 tables for both profiles
- Scatter plots: Progression vs Pass Completion, Build-Up Involvement, Tackle Volume vs Efficiency, Interceptions vs Recoveries
- Percentile radar charts comparing shortlisted players against prototypes

## Data

| File | Description |
|---|---|
| `data/players_data_light-2024_2025.csv` | FBref player stats, top 5 leagues, 2024/25 season |

## Setup

### 1. Clone the repository
```bash
git clone https://github.com/sbd99/Midfield-Scouting.git
cd Midfield-Scouting
```

### 2. Create a virtual environment (optional but recommended)
```bash
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate
```

### 3. Install dependencies
```bash
pip install -r requirements.txt
```

### 4. Launch Jupyter and run the notebook
```bash
jupyter notebook
```

Open `Midfield_players.ipynb` and run all cells.

## Requirements

- Python 3.10+
- See `requirements.txt` for package versions
