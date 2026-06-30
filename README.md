# Beyond GDP: Human Development and Capability Analysis

Is GDP alone enough to explain how developed and how happy a country is, or do health, education, freedom, social support and governance matter just as much?

This project brings together four global data sources for the year 2023, builds a single country-level dataset, and studies the relationship between income and other dimensions of human development. The framing is inspired by Amartya Sen's capability approach, which says development should be judged by what people are actually able to do and be, not by income alone.

## Research question

Is GDP alone sufficient to explain human development and well-being, or do education, health, freedom, social support and governance play an equally important role?

## Data sources

All data is for the 2023 reference year.

- UNDP Human Development Report 2025 — HDI, life expectancy, schooling, GNI per capita
- World Happiness Report — happiness score and factor contributions
- World Bank — GDP per capita, health expenditure, unemployment, inflation, population
- Transparency International — Corruption Perceptions Index (CPI) 2025

The raw files are not included here because of their size and the providers' terms. Each source is freely available from the links above.

## Project structure

```
beyond-gdp-capability-analysis/
├── data/
│   └── processed/
│       ├── master_dataset.csv      cleaned, merged dataset (130 countries)
│       └── capability_index.csv    the experimental capability index
├── notebooks/
│   ├── 01_data_understanding.ipynb
│   ├── 02_sql_analysis.ipynb
│   ├── 03_eda.ipynb
│   ├── 04_statistics.ipynb
│   ├── 05_clustering.ipynb
│   ├── 06_outliers.ipynb
│   └── 07_capability_index.ipynb
├── requirements.txt
└── README.md
```

## Methodology

1. Cleaning and merging the four sources. Country names were standardised to ISO3 codes, regional aggregates removed, and the sources merged with an inner join. Ten countries with missing values were dropped, leaving 130 countries with complete data.
2. SQL analysis in a SQLite database (joins, grouping, window functions, a view).
3. Exploratory charts (histograms, scatter plots, correlation heatmap, boxplot, bar charts).
4. Statistics: Pearson and Spearman correlation, a multiple linear regression explaining HDI, and a t-test.
5. Clustering: KMeans grouped countries into three development clusters (number chosen with the elbow method and silhouette score).
6. Outlier detection using z-scores.
7. An experimental capability index built from education, health, freedom and social support (income excluded), compared against GDP, HDI and happiness.

## Key findings

- GDP and HDI have a Pearson correlation of 0.71 but a Spearman correlation of 0.98. Richer countries are almost always higher on HDI, but the extra HDI gained per extra dollar shrinks sharply as countries get rich.
- In a regression explaining HDI from outside factors, GDP was not significant once happiness and governance were included, while happiness and the corruption score were.
- High-HDI countries (average happiness 6.46) are significantly happier than lower-HDI countries (average happiness 4.88).
- Clustering split countries into high, middle and low development groups. Income separated the groups the most, while happiness differed far less.
- The capability index (built without income) correlates 0.94 with HDI and 0.86 with happiness, but only 0.67 with GDP.

## Limitations

- The analysis is for one year (2023), so it shows associations, not causes.
- The happiness factor columns are "explained by" contributions, not raw survey values.
- Some predictors overlap, which makes individual regression coefficients harder to read.
- The capability index is an experimental framework, not a replacement for HDI.

## How to run

```
pip install -r requirements.txt
jupyter notebook
```

Open the notebooks in order (01 to 07).

## Tools used

Python (pandas, numpy, matplotlib, seaborn, scipy, statsmodels, scikit-learn), SQL (SQLite), Jupyter Notebook.

## Author

Ashutosh Jayant

- GitHub: https://github.com/jayantashutosh-rgb
- LinkedIn: https://www.linkedin.com/in/ashutosh-jayant-954a54a0/
