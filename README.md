# AI-Enhanced Factor Analysis for Predicting S&P 500 Stock Dynamics

## Project Overview  

This project explores the interplay of technical, market, and statistical factors in predicting S&P 500 stock dynamics. By leveraging machine learning models and financial analytics, the study aims to uncover patterns that enhance predictive accuracy and inform investment strategies.  

---

## Data  

- **Source**: CRSP (Center for Research in Security Prices) Database  
- **Time Period**: January 2019 – December 2023  
- **Scope**: S&P 500 constituents  

**Data Processing Steps**:  
1. **Data Integration**: Merging stock price data, trading volume, and company-level descriptors using `permno` identifiers.  
2. **Temporal Filtering**: Including only periods when companies were actively part of the S&P 500 index.  
3. **Missing Value Handling**: Forward-fill imputation for missing stock-level data.  
4. **Outlier Treatment**: Replacing extreme or infinite values with appropriate defaults to maintain data consistency.  

---

## Factor Construction  

The project incorporates a range of factors to capture key aspects of market behavior, including momentum, volatility, and liquidity.  

| **Factor**                  | **Description**                                               |
|-----------------------------|---------------------------------------------------------------|
| Market Capitalization       | Total market value of a company’s outstanding shares         |
| Momentum                    | Percentage price change over a 12-month period               |
| Amihud Illiquidity          | Price impact per unit of trading volume                      |
| Rolling Volatility          | Standard deviation of returns over 20 periods                |
| Relative Strength Index (RSI)| Measures overbought/oversold conditions                     |
| High-Low Spread             | Difference between highest and lowest prices over 20 periods |
| Turnover Ratio              | Trading volume normalized by shares outstanding              |
| Volatility Dynamics         | Interaction of volatility levels and change rates            |
| Momentum Liquidity          | Product of momentum and illiquidity                          |
| Risk Adjusted Momentum      | Momentum adjusted for volatility and turnover                |

---

## Model Development  

Four machine learning models were employed:  

1. **Linear Regression**: Baseline model for linear relationships.  
2. **Ridge Regression**: Addresses multicollinearity through regularization.  
3. **Random Forest**: Captures nonlinear patterns and identifies feature importance.  
4. **Gradient Boosting**: Iteratively minimizes error for high predictive accuracy.  

**Model Configuration**:  
- Ridge Regression: Regularization parameter α = 1.0  
- Random Forest: 100 estimators, maximum depth = 5  
- Gradient Boosting: 100 iterations, maximum depth = 3  

---

## Factor Selection  

To mitigate overfitting and optimize model performance, a two-stage factor selection process was applied:  

1. **Initial Correlation Filtering**: Eliminated features highly correlated with the target variable (threshold > 0.1).  
2. **Model-Based Refinement**: Used Random Forest Regressor to identify the optimal subset of factors with high predictive power.  

### Final Selected Factors  
- Volatility Dynamics  
- Liquidity Stress  
- RSI  
- Short Momentum  
- High-Low Spread  
- Smoothed Return  
- Momentum Liquidity  
- Long Momentum  
- Amihud Illiquidity  

---

## Results  

### Model Performance  
A comparison of models demonstrated improvements following factor filtering. Gradient Boosting exhibited the highest predictive accuracy.  

### Backtesting Strategy  
- **Framework**: Rolling window with a 36-month training period and a 1-month test window.  
- **Portfolio Construction**: Top 100 stocks selected based on predicted returns.  
- **Performance**: The portfolio demonstrated steady cumulative returns with lower volatility than the market benchmark.  
- **Sharpe Ratio**: 0.25, indicating moderate risk-adjusted returns.  

---

## Limitations and Future Work  

- **Performance Gap**: The strategy underperformed the market benchmark, highlighting the need for further refinement.  
- **Future Improvements**:  
   - Integration of macroeconomic indicators and alternative data sources (e.g., news sentiment).  
   - Advanced dimensionality reduction techniques such as PCA and Autoencoders.  
   - Dynamic portfolio optimization using methods like Markowitz mean-variance and Black-Litterman frameworks.  
   - Factor timing strategies to adapt to market cycles.  

- **Backtesting Enhancements**:  
   - Robust evaluation metrics (e.g., Sortino Ratio, Maximum Drawdown).  
   - Stress testing under extreme market conditions.  
   - Cross-market validation with international indices.  

---

## Disclaimer  

This project is for research purposes only and does not provide financial advice or pre-built trading strategies. The findings highlight challenges in applying machine learning to financial data analysis, including non-stationarity, limited historical data, and low signal content.

---

## References  

1. Tian Song, *Forecasting Stock Returns Using Random Forests and Gradient Boosting*  
2. Gu, S., Kelly, B., & Xiu, D. *Empirical Asset Pricing via Machine Learning*  
3. Chinco, A., Clark-Joseph, A. D., & Ye, M. *Sparse Signals in the Cross-Section of Returns*  
