# NBA Player Salary Analysis

Analyzing how direct performance stats (PPG, RPG, APG) vs. advanced metrics (PER, eFG%, Win Shares) predict NBA player salaries, and whether player position influences compensation.

**Course:** STA 141A - Fundamentals of Statistical Data Science, UC Davis  
**Team:** Roy Ho, Winson Yu  
**Professor:** Alexander Aue  
**Date:** Summer 2024

---

## Research Questions

1. Do direct metrics (points, rebounds, assists per game) predict salary more accurately than advanced metrics (player efficiency rating, effective field goal percentage, win shares)?
2. To what extent does a player's position influence their salary?

## Dataset

Two CSV files from [Kaggle](https://www.kaggle.com/datasets/ulrikthygepedersen/nba-player-salaries/data) were combined:

- **players.csv** - Player attributes and career performance statistics
- **salaries_1985to2018.csv** - Season-by-season salary data from 1985 to 2018

Salaries were aggregated into career averages per player and joined with performance data on player ID.

## Key Results

### Question 1: Direct vs. Advanced Metrics

R-squared values across transformations:

| Transform | Direct (combined) | Points | Rebounds | Assists | Advanced (combined) | PER | eFG% | Win Shares |
|---|---|---|---|---|---|---|---|---|
| None | 0.446 | 0.411 | 0.312 | 0.158 | 0.388 | 0.178 | 0.062 | 0.371 |
| Log | 0.396 | 0.348 | 0.301 | 0.130 | 0.298 | 0.164 | 0.097 | 0.261 |
| Sqrt | 0.466 | 0.419 | 0.341 | 0.160 | 0.374 | 0.188 | 0.085 | 0.347 |
| Poly | - | 0.426 | 0.361 | 0.179 | - | 0.193 | 0.097 | 0.414 |

Direct metrics explained more variance in salary than advanced metrics overall. Points and rebounds were the strongest individual predictors, while effective field goal percentage was the weakest. Transformations did not meaningfully improve model fit, suggesting the linear relationship is already the best approximation with these features.

All predictors had statistically significant p-values and VIF values below 5 (no multicollinearity).

### Question 2: Salary by Position

| Position | Average Salary |
|---|---|
| Center | $2,438,832 |
| Power Forward | $2,392,134 |
| Small Forward | $2,220,477 |
| Shooting Guard | $2,041,212 |
| Point Guard | $1,973,207 |

Centers earned the most on average, with a roughly $465K gap between the highest and lowest paid positions.

## Methods

- Simple and multiple linear regression (R `lm()`)
- Response variable transformations: log, square root, polynomial
- Variance Inflation Factor (VIF) to check for multicollinearity
- Visualization with ggplot2 and gridExtra

## Project Structure

```
nba-salary-analysis/
├── README.md
├── finalProject.Rmd          # Full R Markdown analysis
├── report.pdf                # Final written report
└── data/
    └── README.md             # Instructions for obtaining the dataset
```

## Setup

### Requirements
- R 4.0+
- Packages: `car`, `dplyr`, `tidyverse`, `ggplot2`, `gridExtra`, `viridis`

```r
install.packages(c("car", "dplyr", "tidyverse", "ggplot2", "gridExtra", "viridis"))
```

### Data
Download both CSV files from [Kaggle](https://www.kaggle.com/datasets/ulrikthygepedersen/nba-player-salaries/data) and place them in a `dataset/` directory one level above this project, or update the file paths in `finalProject.Rmd`.

### Running
Open `finalProject.Rmd` in RStudio and knit to HTML.

## References

Pedersen, Ulrik Thyge. *NBA Player Salaries.* Kaggle, 2023. [https://www.kaggle.com/datasets/ulrikthygepedersen/nba-player-salaries/data](https://www.kaggle.com/datasets/ulrikthygepedersen/nba-player-salaries/data)
