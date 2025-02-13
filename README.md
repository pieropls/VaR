# **📉 Value at Risk (VaR) in Python**

## **📌 Overview**
This repository demonstrates three methods for estimating **Value at Risk (VaR)**, a key risk management metric used to quantify potential losses in a portfolio. Here are the **methods implemented 🛠**:

1. **🎲 Monte Carlo Method** – Uses simulated price paths to model possible future returns.
2. **📈 Parametric Method (Variance-Covariance)** – Assumes normally distributed returns and calculates risk analytically.
3. **📜 Historical Method** – Relies on actual past returns to estimate risk without distributional assumptions.

Each method is **explained mathematically** and **implemented in Python** with clear visualizations.

## **📊 What is Value at Risk (VaR)?**
**Value at Risk (VaR)** measures the **potential loss** in a portfolio over a given time period at a specified confidence level. It answers the fundamental risk management question:

> *"What is the maximum expected loss over a given time horizon with a certain probability?"*

Mathematically, **VaR at confidence level $1 - \alpha$** is defined as:

$$
VaR_{1-\alpha}(X) := \inf_{t \in \mathbb{R}} \left( t : \mathbb{P}(X \le t) \ge 1 - \alpha \right)
$$

where:
- $X$ is the portfolio return distribution,
- $\alpha$ is the significance level (e.g., 0.05 for a 95% confidence interval),
- $t$ is the loss threshold exceeded with probability $\alpha$.

### **🔍 Interpretation:**
If VaR(95%) = $10.000, this means that:
- There is a **95% probability** that losses **will not exceed** $10.000 over the given period.
- Conversely, there is a **5% probability** that losses **will exceed** this amount.

## **🎲 1. Monte Carlo Method**
🔹 **Description:**  
This approach estimates VaR by simulating **thousands of possible future portfolio returns** using a **stochastic process**. It is particularly useful for **non-normal return distributions** and portfolios with complex risk factors.

🔹 **Mathematical Representation:**  
Given:
- **Initial portfolio value**: $P_0$
- **Expected daily return**: $\mu$
- **Daily volatility (standard deviation)**: $\sigma$
- **Time horizon (in days)**: $T$
- **A standard normal random variable**: $Z$

The portfolio return over $T$ days is simulated as:

$$
\Delta P = P_0 \cdot \mu \cdot T + P_0 \cdot \sigma \cdot Z \cdot \sqrt{T}
$$

Once **N** simulations are performed, VaR is estimated as the **negative percentile** of the simulated return distribution:

$$
VaR = -\text{Percentile}(\Delta P, (1-\alpha) \times 100)
$$

📄 Notebook: [`1.VaR.Montecarlo.ipynb`](1.VaR.Montecarlo.ipynb)

## **📈 2. Parametric Method (Variance-Covariance)**
🔹 **Description:**  
This approach assumes that **portfolio returns follow a normal distribution** and calculates VaR using the **portfolio's standard deviation** and the corresponding **Z-score** from the normal distribution. It is widely used due to its simplicity and efficiency.

🔹 **Mathematical Representation:**  
Given:
- **Portfolio value**: $P_0$
- **Portfolio standard deviation**: $\sigma_p$
- **Time horizon (in days)**: $T$ (typically normalized to 252 trading days per year)
- **Z-score corresponding to $\alpha$**: $Z_{\alpha}$

VaR is computed as:

$$
VaR = P_0 \cdot \sigma_p \cdot Z_{\alpha} \cdot \sqrt{\frac{T}{252}}
$$

📄 Notebook: [`2.VaR.Parametric.ipynb`](2.VaR.Parametric.ipynb)

## **📜 3. Historical Method**
🔹 **Description:**  
Unlike the other methods, the **historical approach does not assume any distribution**. Instead, it calculates VaR by directly analyzing past **realized portfolio returns** and selecting the **worst-case losses** at the chosen confidence level.

🔹 **Mathematical Representation:**  
Given a series of historical returns $X$, VaR is defined as:

$$
VaR = -\text{Percentile}(X, 100 \times (1-\alpha)) \times \text{Portfolio Value}
$$

This method is **simple and intuitive**, but its accuracy depends on the assumption that **historical returns are representative of future risks**.

📄 Notebook: [`3.VaR.Historical.ipynb`](3.VaR.Historical.ipynb)

## **📚 Acknowledgments**
This project is based on the tutorials by **Ryan O'Connell, CFA, FRM** on Value at Risk. His explanations provided great insights and inspiration for this work. You can check out his videos here:

- 🎥 [Value at Risk (VaR) In Python: Monte Carlo Method](https://www.youtube.com/watch?v=X8aNFXJEENs)
- 🎥 [Value at Risk (VaR) In Python: Parametric Method](https://www.youtube.com/watch?v=n8N1KK_1T50)
- 🎥 [Value at Risk (VaR) In Python: Historical Method](https://www.youtube.com/watch?v=jZJsPi4j7wQ)

A huge thank you to him for sharing his expertise! 🙌
