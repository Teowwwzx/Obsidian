
## 1. Wealth Management vs. Investment Management
## Wealth Management
Holistic service includes **financial planning, tax services, estate planning.** It's about managing total net worth (Assets - Debts)

## Investment Management
Specific subset of wealth management focused on making money grow through professional trading and portfolio construction.
- Core Functions:
	- **Asset Allocation:** How to split money between stocks, bonds and cash.
	- **Security Selection:** Choosing specific stocks or bonds within those categories.


## 2. The Risk-Return Trade-off
In finance, risk and return are inseparable. Higher return higher volatility (risk).
- **Risk** measured by **Standard Deviation ()**, which tells us how much an investment's return varies from its average.
- **Risk-Free Rate ():** The return on an investment with zero risk like government [[T-bills]].


## 3. Diversification: The "Only Free Lunch"
Diversification involves spreading investment across different assets to reduce **unsystematic risk.**
- **Correlation ():** Secret to diversification. If two stocks move opposite directions (negative correlation), they cancel out each other's volatility making overall portfolio smoother.
- **The Goal:** To achieve the highest possible return for a specific level of risk.


## Statistical Tools for Analysis
To manage a portfolio, we used several metrics:
- **Mean:** Average expected return.
- **Beta ():** Measures how much a stock moves relative to the market. A beta of 1.5 means the stock is 50% more volatile than the market.
- **Skewness:** Measures if returns are **lopsided** toward big gains or big losses.
- **Kurtosis:** Measures the **fatness** of the tails - essentially the likelihood of extreme, unexpected market crashes.


## Monte Carlo Simulation
A **stress test** for your money instead of calculating one possible future, a computer runs thousands of **what-if** scenarios using random variables for market returns, inflation and volatility

**Example:**
1. Planning 10-year investment.
2. Assume steady 7% return every year.
3. But in the real world, market might be +20% one year and -15% to next.

| Metric                 | Meaning                                                                                                                                                                                                                                                                                                                                                                                                                        | How to Use It                                                                              |
| ---------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------ |
| **Mean Return**        | Average return from an investment over time.                                                                                                                                                                                                                                                                                                                                                                                   | Higher value mean better long-term performance.                                            |
| **Standard Deviation** | Measures how much returns flactuate (volatility)                                                                                                                                                                                                                                                                                                                                                                               | Higher value mean more volatile returns. User it to manage portfolio risk diversification. |
| **Skewness**           | Whether returns are more often small with occasional large gains (positive) or losses (negative)                                                                                                                                                                                                                                                                                                                               | Helps to spot asymmetry in return patterns and adjust asset selection accordingly.         |
| **Kurtosis**           | Measures how often extreme returns happen ([[fat tails]]). The **[[Black Swan]], [[2008 financial crisis]] or [[COVID-19]]**<br>---<br>A Perfectly **Normal Distribution** has a Kurtosis of **3**<br>---<br>**Fat Tails (Leptokurtic):** Kurtosis > 3. This tells **Value at Risk (VaR)** might be higher than expected because the **tails** mean where the big losses hide.<br><br>![[Pasted image 20260130151216.png]]<br> | Higher kurtosis signals potential for big ups or downs. Useful for managing tail risk.     |
| **Beta**               | How sensitive of the assets to the market, usually proxied by a [[stock index]]<br><br>[[1997 Asian Financial Crisis]], the KLCI showed **Fat Tails**. A simple model predicted a 2% drop but the reality resulted much larger swings                                                                                                                                                                                          | Higher beta mean more market exposure.                                                     |
| **Correlation Matrix** | How assets move relative to each other.                                                                                                                                                                                                                                                                                                                                                                                        | Use to pick low or negatively correlated assets for better risk diversification.           |

![[Pasted image 20260130150354.png]]



![[Pasted image 20260130145244.png]]

**Skewness:**
- A positive 0.3273 skew like Apple mean that small losses but higher chance of massive gain.
- A negative -0.1057 skew like Google mean that small gain but higher chance to drop and crash hard and fast.


**Kurtosis:**
- A high kurtosis 4.9715 of Google is a leptokurtic distribution and it mean Google has fat tail. Most day very quiet but when things go crazy, they go really crazy. More extreme price swings (both up and down) than a standard bell curve would predict.
- A low kurtosis 0.4839 of DJI is a platykurtic distribution. The returns are more consistent and very few shocks or wild outliers here.

**Beta:**
A beta of 1.77 of Tesla mean if market goes up 1%, Tesla is expected to jump 1.77% which mean more volatile than the general market.

DJI stand for Dow Jones Industrial Average which is a major **US stock index.**


![[Pasted image 20260131170337.png]]
