# School-age digital connectivity: data cleaning and exploration

How many school-age children have an internet connection at home, and how does that vary with a country's income level, where a child lives and how wealthy their household is?

This project cleans a messy country-level dataset and explores those three questions with pandas and matplotlib.

Completed in 2023 during my Master of Data Science at RMIT University.

## Data

The data is a variant of UNICEF's [global database on school-age digital connectivity](https://data.unicef.org): for each country, the percentage of children of school attendance age (roughly 3 to 17) with an internet connection at home, in total and broken down by residence (rural, urban) and wealth quintile (poorest, richest). It is based on household surveys from 2010 onwards.

The raw file I worked from had errors deliberately introduced for a data-cleaning exercise. It is not mine to redistribute, so it is not included here. This repository contains:

- `data/school_connectivity_clean.csv`: the cleaned dataset the notebook produces (76 countries)
- `school_connectivity_eda.ipynb`: the full notebook, with its original outputs

Section 1 of the notebook needs the raw file to re-run. Section 2 runs from the cleaned file.

## Cleaning

Problems found in the raw file and how each was handled:

| Problem | Fix |
|---|---|
| Duplicate rows (Turkey appeared three times) | Dropped duplicates, 78 rows to 76 |
| Leading whitespace in category labels and column headers | Stripped |
| Misspelt category ("Lowerr middle income") | Corrected |
| Percentages stored as text ("24%") | Converted to numeric; unit moved into the column name |
| Missing values in the rural, poorest and richest columns | Filled with the column median, since all three are skewed |
| Impossible survey years (2076, 2562) and mixed year formats | Column not needed for the analysis, so dropped |
| Columns not used in the analysis (ISO code, region, data source) | Dropped |

## Findings

- **Overall:** on average 35.9% of school-age children have internet at home (median 31.5%), with a wide spread across countries.
- **Income group:** access rises steeply with national income. The boxplot in section 2.1 shows the four income groups barely overlapping.
- **Rural versus urban:** the median country has 14.0% access in rural areas and 43.5% in urban areas, about 3.1 times higher.
- **Wealth within upper-middle-income countries:** among the 28 countries in this group, the poorest quintile averages 33.3% access (median 27.5%) and the richest 84.2% (median 94.0%). A country's income classification hides a large gap between its richest and poorest households.

## Limitations

- Median imputation keeps every country in the analysis but understates the true spread in the three imputed columns.
- Survey years differ by country (2010 onwards), so the comparison is not of a single point in time.
- The outputs in the notebook are from the original 2023 run and have not been regenerated.

## Running it

```
pip install -r requirements.txt
jupyter notebook school_connectivity_eda.ipynb
```
