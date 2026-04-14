# DSA 210 

## Does a spike in job-related Google searches predict a rise in youth unemployment in Turkey, and by how many months?

### Motivation

Youth unemployment in Turkey has remained high for over a decade  and official TÜİK figures come out with a delay of several weeks.This project investigates how many months in advance job-related Google searches predict a rise in youth unemployment.When labor market conditions worsen, people tend to search for job listings and employment services before any official report captures the shift. The goal is to measure the size of this time delay and test whether it is statistically consistent.

---

### Research Questions

**Main question:**
Does a spike in job-related Google searches predict a rise in youth unemployment in Turkey, and by how many months?

**Sub-questions:**
1. Is the correlation between search terms and unemployment strongest at 0, 1, or 2 months ahead?
2. Which search terms show the strongest correlation with youth unemployment at different time delays?
3. Did the relationship between search behavior and unemployment change during periods of economic shock, such as the 2018 currency crisis or COVID-19?


---

### Data Description

For this project I used four data sources, all at monthly frequency and covering January 2015 to December 2024. All sources are merged into a single dataset using the month as a shared key, giving 120 observations and 16 variables in total.

**TÜİK Labour Force Statistics** — The main outcome variable is the monthly youth unemployment rate for ages 15 to 24. The non-seasonally adjusted series is used, and seasonality is controlled in the analysis. Downloaded as a single Excel file from data.tuik.gov.tr.

**Google Trends** — Monthly search index (0–100) for 10 job-related terms in Turkey: işkur, iş ilanı, iş arıyorum, linkedin, kariyer.net, iş kurumu, cv hazırlama, işsizlik maaşı, işsizlik sigortası, işsizlik ödeneği. Collected via the pytrends Python library.

**TCMB EVDS** — Four monthly macroeconomic variables: CPI inflation, USD/TRY exchange rate, policy interest rate, and industrial production index. Collected via the evds Python library.

**Unemployment insurance applications** — Monthly number of people who applied for unemployment benefits, from TCMB EVDS. A direct measure of job loss, collected via the evds Python library.

---

### Methods

- **EDA:** Time series plots, correlation matrix
- **Cross-correlation analysis:** Pearson correlation at time delays of 0–6 months
- **Hypothesis testing:** Independent samples t-test (high vs low search volume months)

---

### Key Findings

**Cross-correlation:**
- `işkur` shows the strongest signal: correlation peaks at 2 months ahead (r = 0.54, p < 0.05)
- `iş_ilanı` also shows a growing correlation with time delay, peaking at 3 months (r = 0.43)
- `linkedin` and `cv_hazırlama` show negative correlations these terms are searched more when the economy is doing well
- `iş_arıyorum` shows no statistically significant relationship

**T-test (time delay = 2 months):**
- When `işkur` search volume is high, youth unemployment 2 months later averages 22.0% vs 18.7% when search volume is low (t = 6.90, p < 0.001)
- `iş_ilanı` also shows a significant difference (p = 0.044)

---

### Tools & Libraries

- Python, pandas, numpy, matplotlib, seaborn
- scipy.stats (Pearson correlation, t-test)
- pytrends (Google Trends API)
- evds (TCMB EVDS API)
