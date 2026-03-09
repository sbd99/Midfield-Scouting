# Young Midfielder Scouting & Profiling — Top 5 European Leagues (2024/25)

A data science scouting project that profiles and ranks young midfielders across Europe's top five leagues using two distinct analytical frameworks: prototype-based cosine similarity and composite z-score ranking.

---

## Overview

Identifying the right midfielder requires asking different questions depending on the role. This project treats the DLP and DM archetypes separately and applies a methodology suited to each:

- **Deep-Lying Playmakers** are profiled using cosine similarity against a real elite prototype (Vitinha, PSG). The underlying logic is that if a player's statistical fingerprint closely resembles Vitinha's, they likely play a similar role — regardless of the league or system they play in.

- **Defensive Midfielders** are ranked using a composite z-score that rewards players who are simultaneously above average across all five ball-winning metrics, with a penalty term discouraging specialists who excel at one metric but drop off elsewhere.

---

## Project Structure

```
├── data/
│   └── players_data_light-2024_2025.csv   # Source: FBref, 2024/25 season (top 5 leagues)
│
└── Mid_players.ipynb                       # Full analysis notebook
```

---

## Notebook Contents

### 1. Data Loading & Filtering
- Source: FBref 2024/25 — Premier League, La Liga, Bundesliga, Serie A, Ligue 1
- Filter: `Pos == "MF"`, ages 21–26, minimum 1,300 minutes played
- 276 qualifying players after filtering

### 2. Per-90 Normalisation
Raw counting stats (tackles, interceptions, progressive passes etc.) are converted to per-90-minute rates to remove the bias from players who have simply played more minutes.

### 3. Part 1 — Deep-Lying Playmaker (DLP) Similarity

**Prototype:** Vitinha (Paris Saint-Germain)

**Features:**

| Feature | Rationale |
|---|---|
| Progressive Passes per 90 | Core DLP output — how often they advance play |
| Touches per 90 | Ball magnetism / involvement in build-up |
| Progressive Carries per 90 | Dynamic dimension of playmaking |
| Passes Attempted per 90 | Passing volume |
| Pass Completion % | Ball retention and technical quality |
| Interceptions per 90 | Defensive awareness — press trigger |

**Method:** `StandardScaler` → `cosine_similarity` between each player's feature vector and Vitinha's

**Output:** Ranked similarity table + case study comparing **Angelo Stiller vs Vitinha** via scatter plots and percentile rank radar

### 4. Part 2 — Defensive Midfielder (DM) Composite Score

**Features:** `Tkl_per90`, `Int_per90`, `Recov_per90`, `Tkl%`, `Pass_Cmp%`

**Scoring formula:**
```
DM_score = mean(Z_scores) - std(Z_scores)
```
The penalty term (`- std`) reduces the score for one-dimensional players who spike on a single metric but underperform elsewhere, favouring well-rounded profiles.

**Output:** Ranked top 20 table + scatter plots highlighting the top 10 + three-way radar comparison: **Agoumé vs Caicedo vs André**

---

## Tech Stack

| Library | Purpose |
|---|---|
| `pandas` | Data manipulation and filtering |
| `numpy` | Numerical operations |
| `matplotlib` | Visualisation |
| `scikit-learn` | StandardScaler, cosine similarity |

---

## Data Source

All data sourced from **[FBref](https://fbref.com)** — 2024/25 season, top 5 European leagues. Players with fewer than 1,300 minutes played are excluded to ensure statistical reliability.

---

## Key Concepts

**Cosine Similarity** — measures the angle between two vectors in feature space. A score of 1.0 means identical profiles; 0.0 means no similarity. Used here to find players whose statistical mix most closely resembles the prototype, rather than players who simply have similar raw numbers.

**Z-Score** — standardises each metric to mean 0, standard deviation 1. Allows metrics measured on different scales (e.g. tackles per 90 vs pass completion %) to be combined into a single composite.

**Percentile Rank Radar** — each radar axis shows where a player sits relative to the rest of the pool on that metric (0 = bottom, 1 = top). More intuitive for comparison than raw z-scores.
