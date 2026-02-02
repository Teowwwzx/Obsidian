![[Pasted image 20260131175352.png]]
$$E[R] = [(\tau \Sigma)^{-1} + P^T \Omega^{-1} P]^{-1} [(\tau \Sigma)^{-1} \Pi + P^T \Omega^{-1} Q]$$

---

**QUESTION 1**

The rate of return on Apex was _rA=_ 3.1%. The rate of return on Bpex was only _rB =_ 2.5%. The market today responded to very encouraging news about the unemployment rate, and _rM_ = 3%. The historical relationship between returns on these stocks and the market portfolio has been estimated from index model regressions as:

Apex: rA = .2% + 1.4rM

Bpex: rB = -.1% + .6rM

**Required:**

a.      Derive the forecasted returns using the given regression model.

b.      Develop a returns evaluation statement with a trading call recommendation based on the stock's rate of returns versus the forecasted returns.

the specific math in **Question 1** uses the **[[Single-Index Model]] ([[Regression Model]])**, which estimates returns based on a stock's relationship with the overall market.


>[!info] Single-Index Model
> 
>This model assumes a stock's return is driven by only **one** thing: the overall market.
>- **The Logic:** If the market (e.g., FBMKLCI) goes up, the stock follows it based on its **Beta**.
>- **The Formula:** You saw this in your tutorial: $r = \alpha + \beta(r_M)$. Only one variable here $r_M$


> [!info] Multiple-Index Model
>This model assumes a stock is influenced by **multiple** factors which refer to economic factors like **inflation, interest rates, or industry-specific trends**.
>
>- **The Formula:** $r = \alpha + \beta_1(Factor 1) + \beta_2(Factor 2) \dots$


>[!info] Regression Model
>
>This model assumes a stock is influenced by **multiple** factors at once.
>- When you use a **Single-Index Model**, you are performing a **Simple Linear Regression** to see how much the market predicts the stock.


> [!info] What is Default?
>- **Standard Finance (CAPM):** The **Single-Index Model** is the default because it's simpler.
>- **Black-Litterman Model (BLM):** You are right—BLM is more advanced. While it starts with a **market equilibrium** (which looks like a single index), its power comes from letting you add **multiple views** or factors. In professional Fintech settings, **Multiple-Index** is the default for BLM because it's meant to handle complex, real-world data.

> [!info] Market Equilibrium (市场均衡)
> In finance and the context of the **Black-Litterman Model (BLM)**, **Market Equilibrium** refers to a "neutral" state where the market is considered efficient. It assumes that current market prices reflect all available information and that the supply of assets exactly equals the demand from investors.
> - It is the starting point of the BLM. We use "Reverse Optimization" to find the **Implied 隐含 Market Returns ($\pi$)**. This tells us what returns the market _expects_ to see, based on the current **Market-cap weights ($W_m$)** and the **Risk aversion ($\lambda$)** of investors.
> - 市场均衡是指市场处于一种“中性”或“平衡”的状态。在 BLM 模型中，它是我们的**初始起点**。我们假设市场目前的资产配置（市值权重 $W_m$）是完美的。通过这个权重，我们可以反向推导出**隐含市场回报率 ($\pi$)**。简单来说，就是看看“大盘认为这些股票未来应该涨多少”。

