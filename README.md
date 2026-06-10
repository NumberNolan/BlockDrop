# Block Drop — Hive Server Analytics
 
Predicting win rate in **Block Drop**, a minigame on [The Hive](https://playhive.com/) Minecraft Bedrock server. In Block Drop, players stand on a platform that crumbles beneath them — the last one standing wins. This project uses leaderboard data from the top 1000 ranked players to model what separates high win-rate players from the rest.
 
---
 
## Dataset
 
Scraped from the Hive Block Drop leaderboard — 1000 players, top-ranked by victories.
 
| Column | Description |
|---|---|
| `Username` | Player's Minecraft username |
| `Rank` | Leaderboard rank |
| `Played` | Total games played |
| `Victories` | Total wins |
| `WinPercentage` | Win rate (target variable) |
| `Deaths` | Total deaths |
| `Blocks Destroyed` | Total blocks destroyed |
| `Powerups Collected` | Total powerups collected |
| `Vaults Used` | Total vaults used |
| `BlocksPerGame` | Blocks destroyed per game |
| `PowerupsPerGame` | Powerups collected per game |
| `VaultsPerGame` | Vaults used per game |
 
Per-game rate features (`BlocksPerGame`, `PowerupsPerGame`, `VaultsPerGame`) are used as predictors rather than raw totals to normalize across players with very different game counts.
 
---
 
## Models
 
| Model | R² | RMSE |
|---|---|---|
| Linear Regression | 0.5550 | 0.1311 |
| Ridge Regression | 0.5553 | 0.1311 |
| Random Forest | 0.6677 | 0.1133 |
| AdaBoost | 0.6693 | 0.1131 |
 
---
 
## Key Findings
 
- **PowerupsPerGame** is the strongest predictor of win rate by a wide margin — it explains ~55% of variance on its own and accounts for ~60% of feature importance in both ensemble models.
- **VaultsPerGame** has a negative coefficient in linear models, suggesting that heavy vault usage is more common among lower-ranked players who react defensively rather than dominating early.
- **BlocksPerGame** has a non-linear relationship with win rate — it matters, but only up to a point.
- Ensemble models (Random Forest, AdaBoost) outperform linear models by ~11% R², confirming the feature-win relationships aren't purely linear.
---
 
## Files
 
```
blockdrop.ipynb   # Full analysis notebook
blockdrop.csv     # Dataset
README.md
```
 
---
 
## Requirements
 
```
pandas
scikit-learn
```
