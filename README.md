# 👗 Fashion & Economy Cycles

**Author:** [Jinxiang (Jessie) Zhou](https://github.com/jinxiangjessiezjx)

This project builds a machine learning pipeline to test whether economic cycles mathematically predict fashion trend shifts — specifically whether "boom" periods drive maximalist fashion (logomania, neon, Y2K) and "bust" periods drive minimalist fashion (quiet luxury, capsule wardrobes, neutral tones). It answers the question: **"Do macroeconomic conditions predict shifts between maximalist and minimalist fashion trends, and if so, with what lag?"** using 20 years of US economic data from the [FRED API](https://fred.stlouisfed.org) and Google Trends search volume data via [pytrends](https://github.com/GeneralMills/pytrends).

I built a composite Fashion Index by pulling Google Trends search volumes for 10 carefully chosen keywords — 5 maximalist (logomania, neon fashion, mini skirt, sequin outfit, Y2K fashion) and 5 minimalist (quiet luxury, capsule wardrobe, neutral outfit, loafers outfit, maxi skirt) — z-scoring each independently and computing a net index (maximalism minus minimalism). I then merged this with four economic indicators (consumer sentiment, unemployment, GDP growth, CPI inflation) and ran OLS regression with contemporaneous and lagged feature sets to test the predictive relationship.

My key finding is: **economic indicators explain approximately 24% of the variance in the fashion index, but the relationship is regime-dependent rather than stable.** The popular narrative that recessions cause minimalism and booms cause maximalism is too simplistic — the GFC recession coincided with the most maximalist period in the sample (+0.207 average fashion index during Slow Recovery 2009-2014), while the strongest minimalist period (Post-Inflation 2024-2025, -0.670) occurred when unemployment was near historic lows. The relationship only clearly aligns with the hypothesis in the most recent period, where falling consumer sentiment and rising quiet luxury search interest moved together strongly (rolling correlation reaching +0.64 by December 2025). The remaining 76% of fashion variance is driven by factors outside this model — social media, viral moments, and cultural contagion that macroeconomic data cannot capture. Check out the notebooks to understand how I arrived at these conclusions.

## 📂 Repository Structure

```output
/
├── notebooks/
│   ├── NB01-Economic-Data.ipynb
│   ├── NB02-Fashion-Trend-Data.ipynb
│   ├── NB03-Exploratory-Analysis.ipynb
│   ├── NB04-Regression-Model.ipynb
│   └── NB05-Visualisation.ipynb
├── data/
│   ├── raw/
│   │   ├── economic_data_raw.csv
│   │   └── fashion_trends_raw.csv
│   └── processed/
│       ├── economic_data_clean.csv
│       ├── fashion_index.csv
│       ├── fashion_trends_normalised.csv
│       ├── merged_dataset.csv
│       └── model_predictions.csv
├── figures/
│   ├── economic_indicators.png
│   ├── economic_correlation.png
│   ├── keyword_trends.png
│   ├── fashion_index.png
│   ├── merged_overview.png
│   ├── correlation_matrix.png
│   ├── lag_analysis.png
│   ├── scatter_plots.png
│   ├── model_comparison.png
│   ├── coefficients.png
│   ├── actual_vs_predicted.png
│   ├── residuals.png
│   ├── rolling_correlation.png
│   ├── regime_analysis.png
│   └── final_dashboard.png
├── requirements.txt
└── README.md
```

## 🚀 How to Run

1. Clone this repository:

```bash
    git clone https://github.com/yourusername/fashion-economy-cycles.git
    cd fashion-economy-cycles
```

2. Install required packages:

```bash
    pip install pandas numpy matplotlib seaborn scikit-learn statsmodels fredapi pandas-datareader pytrends scipy jupyter
```

3. Run `notebooks/NB01-Economic-Data.ipynb` to pull 20 years of US economic data from the FRED API. This populates `data/raw/economic_data_raw.csv` and `data/processed/economic_data_clean.csv`.

4. Run `notebooks/NB02-Fashion-Trend-Data.ipynb` to pull Google Trends data for all 10 fashion keywords and build the composite Fashion Index. This populates `data/raw/fashion_trends_raw.csv` and `data/processed/fashion_index.csv`. Note: pytrends has rate limits — the notebook adds a 2-second delay between each keyword pull.

5. Run `notebooks/NB03-Exploratory-Analysis.ipynb` to merge the two datasets, run correlation analysis, and identify the best lag structure for each economic indicator.

6. Run `notebooks/NB04-Regression-Model.ipynb` to fit OLS regression models (contemporaneous and lagged) and run residual diagnostics.

7. Run `notebooks/NB05-Visualisation.ipynb` to generate the final publication-quality charts and findings summary.

## 📊 Key Results

| Model | R² | Adj. R² | F p-value |
|-------|----|---------|-----------|
| Baseline (mean) | 0.000 | 0.000 | — |
| OLS Contemporaneous | 0.241 | 0.229 | < 0.001 |
| OLS Lagged | 0.245 | 0.231 | < 0.001 |

| Economic Regime | Period | Avg Fashion Index | Direction |
|----------------|--------|------------------|-----------|
| Pre-Crisis Boom | 2005-2007 | +0.080 | Maximalist |
| GFC Recession | 2007-2009 | +0.139 | Maximalist |
| Slow Recovery | 2009-2014 | +0.207 | Maximalist |
| Expansion | 2015-2019 | -0.157 | Minimalist |
| COVID Shock | 2020-02 to 04 | +0.069 | Maximalist |
| Revenge Spending | 2020-2021 | +0.201 | Maximalist |
| Inflation Crisis | 2022-2023 | +0.089 | Maximalist |
| Post-Inflation | 2024-2025 | -0.670 | Minimalist |

## 📟 Get in touch

If you like my work, get in touch with me on [LinkedIn](https://www.linkedin.com/in/jessie-zhou-37156b268/) or [GitHub](https://github.com/jinxiangjessiezjx).