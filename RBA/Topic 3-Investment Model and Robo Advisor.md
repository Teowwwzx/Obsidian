## 1. Investment Model
A structured approach that guides investor's logic regarding asset selection, capital allocation and balance between risk and return.
- **Quantitative Factor Models:** Analyze statistical driver like size or value.
- **Passive Investment:** Use low-cost [[ETFs]] to track market indices.
- **Risk-Based Portfolio:** Use [[Modern Portfolio Theory (MPT)]] to diversify.

## 2. Asset Pricing Model
This models help calculate **required return** for taking on specific risk.
- **CAPM (Capital Asset Pricing Model):** Relates an asset's return to the overall market risk.
	- **Formula:** $$E(r) = r_f + \beta (r_m - r_f)$$
	- **Components:** risk-free rate (rf), market return (rm), beta (b)
- **Fama-French Three Factor Model:** Expands CAPM by adding **Size** (SMB - Small Minus Big) and **Value** (HML - High minus Low) to better capture real return sources.
	- **Formula:**
	 $$E(r) = R_f + \beta_1 (\text{Market Risk Premium}) + \beta_2(SMB) + \beta_3(HML)$$
- **Arbitrage Pricing Theory (APT):** A flexible model suggesting returns are influenced by multiple macroeconomic factors like inflation, GDP growth, or industry-specific events.

## ==3. The Black-Litterman Model (BLM)==
Traditional [[Mean-Variance Optimization (MVO)]] is often **too sensitive**, meaning tiny changes in assumption lead to extreme, unrealistic portfolio shift.

The **Black-Litterman Mode**l fixes this using **[[Bayesian statistics 贝叶斯统计]]:**
- **Neutral Start 中性开局:** It begins with what the market **believes** (implied market return 隐含市场收益)
- **Investor Views:** It allows to add personal opinions like "I think gold will beat stocks by 2%".
- **Confidence Matter:** How much model adjusts toward your view depends on how confident you are in your opinion.
- **The Goal:** Produces stable, intuitive 直观 portfolio weights.

## 4. Behavioral Finance
Traditional models assume investors are rational, behavioral finance proves they often aren't

Common biases:
- **Overconfidence:** Overestimating ability to predict market.
- **Loss Aversion:** Feeling the pain of loss more intensely than the joy of equivalent gain.
- **Herd Behavior:** Following the crowd regardless of personal analysis.
- **Regret Avoidance:** Making decision just to avoid future emotional pain of being wrong.

## 5. Technical Analysis & Sentiment Indicators
Instead of financial data, this model looks for patterns and **moods** in the market.

- **Trin Ratio (aka Arms Index 阿姆斯指标 / 交易指数):** Compares volume in rising vs falling stocks to measure selling pressure. 衡量市场**强度**的指标 通过对比**上涨股票的数量**与**成交量**，来判断资金流向.
$$\text{Trin} = \frac{(\text{上涨股票家数} / \text{下跌股票家数})}{(\text{上涨股票成交量} / \text{下跌股票成交量})}$$
	- **Trin < 1.0** = big rising volume (Bullish)
	- **Trin > 1.0** = big falling volume (Bearish)

- **Confidence Index 信心指数（通常指巴伦周刊信心指数）:** Uses the yield gap between high-grade and low-grade bonds to see how brave investors are 反映了债券投资者对未来的信心.
	- **How:** Calculating the yield of high-grade and low-grade bond.
		- Index goes up = investor willing to buy more risk, more return bond which mean confidence about future.
- **Put/Call Ration 看跌/看涨期权比率:** Compares the number of sell options to buy option to gauge 测量 fear or optimism.
	- **How:** Compare the volume of investor buy **Put（看跌期权，赌市场跌）** and **Call（看涨期权）**
		- Higher ratio mean everyone buy put, market is panic


