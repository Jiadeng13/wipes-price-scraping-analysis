# Wipes — Retail Price Scraping & Analysis

Scraping baby/feminine wipes listings from Amazon, Walmart, Target, and
Walgreens, and analyzing prices and search demand.
Personal care category research · Google Colab / Python

## Objective
Build a cross-retailer view of the wipes category: extract structured
product data (brand, count/pack size, price) from retailer pages, then
analyze pricing and the search terms that drive the category.

## Notebooks

### 1. `Amazon_Wipes_Scraping_V2_05202026.ipynb` (251 cells)
Two-stage Amazon pipeline:
- **Scraping/extraction** — renders Amazon wipes pages with **Playwright**
  and parses them (including complete saved HTML files from Google Drive)
  with **BeautifulSoup**: brand (from URL/title patterns), count and pack
  size via a custom `extract_count_pack_from_text`, price and product
  details → `amazon_wipes_full_extract.csv`.
- **Search-demand analysis** — the shared keyword-classification engine:
  search terms classified into intent categories with the **OpenAI API
  (GPT-5)**, grouped into concepts with a regex-based
  `group_keyword_concept`, and aggregated into monthly-search charts.

### 2. `Walmart_Target_Wipes_Scraping_V4_07072026.ipynb` (20 cells)
Multi-retailer parser: **Playwright** + **BeautifulSoup** extract detailed
product information from saved Walmart, Target, and Walgreens feminine
wipes product tiles (name, price, pack details) into clean CSV tables —
one parser section per retailer.

### 3. `Amazon_Wipes_Price_Analysis_V1_05292026.ipynb` (338 cells)
Price modeling on the scraped Amazon wipes dataset (17,004 unique ASINs
with ratings; 2,979 matched to Profitero API ASINs):
- **EDA** of price, count/pack, ratings, and brand distributions
- **Regression models (scikit-learn)** — Linear Regression, Ridge, Lasso,
  Decision Tree, Random Forest, Bagging, and KNN regressors, tuned with
  GridSearchCV and compared on R² / MAE / RMSE
- **statsmodels** for statistical modeling; **Plotly**, matplotlib, and
  seaborn for interactive and static charts
- *(Uploaded with outputs cleared — the original is 55 MB+ of embedded
  chart images, over GitHub's practical limits.)*

## Tools & packages
- **Playwright (async)** — browser automation / page rendering
- **BeautifulSoup (bs4)** — HTML parsing and product-tile extraction
- **pandas / numpy** — cleaning, merging, aggregation
- **scikit-learn** — regression modeling and GridSearchCV tuning
- **statsmodels** — statistical modeling
- **matplotlib + seaborn + Plotly** — charts
- **OpenAI API (GPT-5)** — LLM classification of search terms
- **Google Colab** — Drive-mounted HTML files and datasets

## Notes
Notebooks are shared with credentials redacted — API keys are loaded from
Colab Secrets (`google.colab.userdata`), never hard-coded.
