# Forecasting Recent College Graduate Unemployment with SARIMA

A time series forecasting project analyzing unemployment trends among recent college graduates (ages 20-24 with Bachelor's degrees) using Seasonal AutoRegressive Integrated Moving Average (SARIMA) modeling and interactive Tableau dashboards.

[![Tableau Dashboard](https://img.shields.io/badge/Tableau-Dashboard-E97627?style=for-the-badge&logo=tableau)](https://public.tableau.com/app/profile/gourav.pal/viz/UnemploymentAnalysis_17638317576870/Dashboard1)
[![Python](https://img.shields.io/badge/Python-3.x-3776AB?style=for-the-badge&logo=python)](https://www.python.org/)
[![FRED API](https://img.shields.io/badge/Data-FRED_API-darkgreen?style=for-the-badge)](https://fred.stlouisfed.org/)
[![Report](https://img.shields.io/badge/Report-Gamma-6C5CE7?style=for-the-badge)](https://gamma.app/docs/Forecasting-Recent-College-Graduate-Unemployment-h753e0kwulogp2d)

## 📊 Project Overview

This project develops a robust forecasting model to predict unemployment rates for recent college graduates, providing insights into labor market dynamics and seasonal employment patterns. The analysis combines statistical modeling with comprehensive exploratory data analysis to identify concerning trends in the entry-level job market.

### Primary Dataset
**Series**: Unemployment Rate - College Graduates - Bachelor's Degree, 20 to 24 years  
**Source**: [Federal Reserve Economic Data (FRED)](https://fred.stlouisfed.org/series/CGBD2024)  
**Time Period**: Monthly data from January 2000 to September 2025  
**Frequency**: Monthly observations (300+ data points)

## 🎯 Key Findings

### 📈 Critical Labor Market Signals

1. **Structural Shift Post-2019**: Recent college graduate unemployment has remained consistently above the national unemployment rate for over 3 years—a departure from historical patterns where the national rate served as the rolling average.

2. **Record Consecutive Increases**: As of September 2025, unemployment has increased for 5 consecutive months (April-September 2025), matching the longest streak observed since March 2007 during the Great Recession.

3. **Seasonal Patterns**: Clear seasonality exists with peaks in summer months (June-August) as graduates enter the job market, followed by declines in winter/spring months.

### 🔍 Correlation Analysis (2000-2025)
Based on state-level analysis across all 50 states:
- **Unemployment Rate vs. Minimum Wage**: -0.22 (weak negative correlation)
- **Unemployment Rate vs. Labor Force Participation**: -0.28 (weak negative correlation)  
- **Labor Force Participation vs. Minimum Wage**: -0.24 (weak negative correlation)

*These correlations indicate no statistically significant relationships between these macroeconomic factors.*

### 🚨 September 2025 Update
- **Actual Rate**: 9.7% (higher than expected due to government shutdown delays)
- **Expected Rate**: ~7.0% (typical seasonal decline)
- **Historical September Average**: 6.7%
- **Model Performance**: Confidence intervals successfully captured the actual value

## 🛠️ Technical Implementation

### Methodology

#### 1. SARIMA Model Specification
**Model**: SARIMA(1, 0, 1)(0, 1, 0)[12]

**Components**:
- **p=1**: Non-seasonal autoregressive term (AR)
- **d=0**: Non-seasonal differencing term
- **q=1**: Non-seasonal moving average term (MA)
- **P=0**: Seasonal autoregressive term
- **D=1**: Seasonal differencing term
- **Q=0**: Seasonal moving average term
- **s=12**: 12-month seasonal cycle

#### 2. Model Validation
**Approach**: Rolling Forecast Origin Method
- **Training Set**: 2000-2021 (21 years)
- **Validation Set**: 2021 - August 1, 2025
- **Evaluation**: One-step-ahead predictions with iterative model expansion
- **Performance**: Mean Squared Error (MSE) = 0.98

This low MSE indicates excellent model performance, with confidence intervals consistently capturing actual unemployment rates throughout the validation period.

### Technology Stack
- **Python 3.x** - Core programming language
- **pandas** - Data manipulation and time series handling
- **statsmodels** - SARIMA model implementation
- **fredapi** - Federal Reserve Economic Data API integration
- **matplotlib/seaborn** - Statistical visualizations
- **Tableau Public** - Interactive dashboard creation

### Project Structure
```
├── forecast.ipynb                              # SARIMA model development & forecasting
├── data_scraping_additional_analysis.ipynb     # Data collection & EDA
├── unemp_20_24_year_olds (1).csv               # Primary unemployment dataset
├── State_Info (2).csv                          # State-level economic indicators
├── Forecasting-Recent-College-Graduate-Unemployment.pdf  # Full project report
└── README.md                                   # Project documentation
```

## 🚀 Getting Started

### Prerequisites
```bash
pip install pandas numpy matplotlib seaborn statsmodels fredapi
```

### FRED API Setup
1. Register for a free API key at [FRED API](https://fred.stlouisfed.org/docs/api/api_key.html)
2. Set your API key as an environment variable:
```bash
export FRED_API_KEY='your_api_key_here'
```

### Running the Analysis

1. **Clone the repository**
```bash
git clone https://github.com/ggpal7117/Forecasting-Recent-College-Grad-Unemployment-with-SARIMA.git
cd Forecasting-Recent-College-Grad-Unemployment-with-SARIMA
```

2. **Execute data collection & EDA**
```bash
jupyter notebook data_scraping_additional_analysis.ipynb
```
This notebook:
- Pulls unemployment data from FRED (145 total series)
- Scrapes state-level unemployment, labor force participation, and minimum wage data
- Performs correlation analysis and exploratory data analysis
- Exports cleaned data for Tableau

3. **Run SARIMA forecasting model**
```bash
jupyter notebook forecast.ipynb
```
This notebook:
- Performs time series decomposition
- Identifies SARIMA parameters using ACF/PACF plots
- Trains model using rolling forecast origin validation
- Generates future unemployment rate forecasts
- Evaluates model performance with MSE and confidence intervals

4. **Explore interactive dashboard**
   - [Open Tableau Dashboard](https://public.tableau.com/app/profile/gourav.pal/viz/UnemploymentAnalysis_17638317576870/Dashboard1)
   - Compare SARIMA forecasts with Tableau's built-in forecasting
   - Analyze seasonal patterns and state-level variations

## 📈 Model Evaluation

### Rolling Forecast Origin Method
The rolling forecast approach provides a realistic evaluation of model performance by:
1. Making a one-step prediction for the next month
2. Adding the actual observed value to the training set
3. Retraining the model with the expanded dataset
4. Repeating until the entire validation set is evaluated

This method prevents look-ahead bias and simulates real-world forecasting scenarios where future data is unavailable.

### Confidence Intervals
The SARIMA model generates prediction intervals at 95% confidence, providing uncertainty estimates around point forecasts. Throughout validation, actual unemployment rates consistently fell within these intervals, demonstrating robust probabilistic forecasting.

![SARIMA Model Performance](https://private-user-images.githubusercontent.com/177767054/505650419-6ab0ecb3-0c09-43ae-a138-10ff823d6cbc.png?jwt=eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3NjY5ODM4MDQsIm5iZiI6MTc2Njk4MzUwNCwicGF0aCI6Ii8xNzc3NjcwNTQvNTA1NjUwNDE5LTZhYjBlY2IzLTBjMDktNDNhZS1hMTM4LTEwZmY4MjNkNmNiYy5wbmc_WC1BbXotQWxnb3JpdGhtPUFXUzQtSE1BQy1TSEEyNTYmWC1BbXotQ3JlZGVudGlhbD1BS0lBVkNPRFlMU0E1M1BRSzRaQSUyRjIwMjUxMjI5JTJGdXMtZWFzdC0xJTJGczMlMkZhd3M0X3JlcXVlc3QmWC1BbXotRGF0ZT0yMDI1MTIyOVQwNDQ1MDRaJlgtQW16LUV4cGlyZXM9MzAwJlgtQW16LVNpZ25hdHVyZT01NmYxNjYwM2RmYjQ2NWUxY2YzMjIxNTBlMWQ1M2Q1MmRjM2U5YzA0NDE1NWFjZWQ3OTY2NjRhMDc5NDA4M2ZkJlgtQW16LVNpZ25lZEhlYWRlcnM9aG9zdCJ9.wJJLO0LSgXBgpNldlxJ6xMLAF-aPqwYo9_t-MqRQRZY)

## 🔍 Additional Analysis

### Longest Unemployment Increase Streaks

**📈 Record Streak Analysis**: 6-month maximum consecutive increases (tied twice in history)

#### Streak #1: Great Recession Era
- **Period**: March 2007 - August 2007
- **Starting Rate**: 3.5%
- **Ending Rate**: 7.3%
- **Total Increase**: +3.8 percentage points

#### Streak #2: Current Period
- **Period**: April 2025 - September 2025
- **Starting Rate**: 4.4%
- **Ending Rate**: 9.7%
- **Total Increase**: +5.3 percentage points

The current 5-month consecutive increase (as of September 2025) marks only the second time this has occurred since 2000, signaling potential structural challenges in the entry-level labor market.

## 💡 Economic Insights & Hypotheses

### Potential Drivers of Elevated Unemployment

Based on recent research and economic data, several factors may contribute to rising graduate unemployment:

1. **AI Displacement & Automation**
   - Entry-level cognitive tasks increasingly automated by AI tools
   - Traditional starter roles (data entry, basic analysis, junior support) facing disruption

2. **Supply-Demand Imbalance**
   - 52% of college graduates underemployed upon labor market entry (Federal Reserve, August 2025)
   - 45% remain underemployed 10 years post-graduation
   - Entry-level corporate job listings down 15% while applications surged 30% (CBS News, July 2025)

3. **Credential Inflation & Grade Deflation**
   - College GPAs rose 16% from 1990-2020 (US Department of Education, September 2025)
   - "A" is now the most common grade awarded
   - Potential disconnect between academic performance and job-readiness

4. **Macroeconomic Headwinds**
   - Policy uncertainty affecting business hiring decisions
   - Tariff impacts: Small businesses reported 3% employment decline due to trade uncertainty (U.S. Congress Joint Economic Committee, May 2025)
   - Economic uncertainty reducing risk appetite for entry-level hiring

5. **Political & Regulatory Factors**
   - Political polarization affecting business confidence
   - Regulatory complexity increasing hiring friction for small businesses

## 📊 Interactive Dashboard Features

The [Tableau dashboard](https://public.tableau.com/app/profile/gourav.pal/viz/UnemploymentAnalysis_17638317576870/Dashboard1) includes:

- **Time Series Comparison**: Recent college grad unemployment vs. national rate vs. non-college 20-24 year olds
- **Seasonal Decomposition**: Visualize trend, seasonality, and residuals
- **State-Level Analysis**: Interactive map with unemployment, participation, and minimum wage metrics
- **Forecast Comparison**: SARIMA model predictions vs. Tableau's built-in forecasting
- **Correlation Heatmaps**: Explore relationships between economic indicators
- **Rolling Statistics**: Moving averages and volatility measures

## 🎓 Statistical Concepts

### ACF & PACF Analysis
- **ACF (Autocorrelation Function)**: Identifies moving average (MA) components by showing correlation between observations at different lags
- **PACF (Partial Autocorrelation Function)**: Identifies autoregressive (AR) components by showing correlation after removing effects of intermediate lags
- **Cutoff Identification**: Sharp drops in PACF suggest AR order; sharp drops in ACF suggest MA order

### Seasonal Differencing
Applying first-order seasonal differencing (D=1) removes the 12-month seasonal pattern, making the series stationary and suitable for ARIMA modeling.

### Stationarity
Time series must be stationary (constant mean and variance over time) for ARIMA modeling. The ADF (Augmented Dickey-Fuller) test confirms stationarity after differencing.

## 🔮 Future Enhancements

- **External Regressors**: Incorporate GDP growth, job openings (JOLTS), and consumer confidence as exogenous variables
- **Machine Learning Comparison**: Benchmark SARIMA against LSTM/Prophet models
- **Occupational Breakdowns**: Analyze unemployment by degree major/field
- **Real-time Updates**: Automate monthly data pulls and forecast updates
- **Scenario Analysis**: Model impacts of policy changes (minimum wage, student loan forgiveness)

## 📄 Documentation

For the complete analysis including detailed methodology, additional visualizations, and comprehensive findings, see:
- **[Full Project Report (PDF)](Forecasting-Recent-College-Graduate-Unemployment.pdf)**

## 🤝 Contributing

Contributions are welcome! Areas for collaboration:
- Alternative forecasting models (Prophet, LSTM, VAR)
- Additional economic indicators integration
- Enhanced visualization dashboards
- Causal inference analysis

## 📚 References

- **Federal Reserve Economic Data (FRED)**: Primary data source
- **U.S. Bureau of Labor Statistics**: Supplementary employment statistics
- **Box, G. E. P., & Jenkins, G. M.** (1976). *Time Series Analysis: Forecasting and Control*
- **Hyndman, R. J., & Athanasopoulos, G.** (2021). *Forecasting: Principles and Practice* (3rd ed.)

## 👤 Author

**Gourav Pal**
- GitHub: [@ggpal7117](https://github.com/ggpal7117)
- Tableau Public: [Profile](https://public.tableau.com/app/profile/gourav.pal)

## 📝 License

This project is available for educational and non-commercial use. Data from FRED is subject to their [terms of use](https://fred.stlouisfed.org/legal/).

## 🙏 Acknowledgments

- Federal Reserve Bank of St. Louis for FRED API access
- U.S. Bureau of Labor Statistics for comprehensive employment data
- The Python time series forecasting community
- Tableau Public for visualization hosting

---

⭐ **Star this repository** if you're interested in labor market analytics and time series forecasting!
