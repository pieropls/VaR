# Value at Risk (VaR) in Python

## Overview

This repository presents three methods, mathematically detailed and implemented in Python, for estimating Value at Risk (VaR), a key metric in financial risk management.

```
VaR/
│
├── 1.VaR.Montecarlo.ipynb          # Monte Carlo Simulation approach
├── 2.VaR.Parametric.ipynb          # Parametric (Variance-Covariance) approach
├── 3.VaR.Historical.ipynb          # Historical Simulation approach
```

## What is VaR?

**Value at Risk (VaR)** measures the maximum expected loss of a portfolio over a given time horizon at a specified confidence level. Formally, for confidence level $1 - \alpha$, it is defined as:

$$
VaR_{1-\alpha}(X) := \inf_{t \in \mathbb{R}} \left( t : \mathbb{P}(X \le t) \ge 1 - \alpha \right)
$$

where $X$ is the portfolio return distribution, $\alpha$ the significance level (e.g., $\alpha = 0.05$ for 95% confidence), and $t$ the loss threshold exceeded with probability $\alpha$. 

> In practice, if VaR(95%) = \$10,000, there is a 95% chance that losses will not exceed \$10,000 and a 5% chance they will.

## Methods Comparison

| Method                          | Assumptions                                                                                                                                                                               | Formula & Key Points                                                                                                                              |
|----------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------|
| **Monte Carlo Simulation**      | - In this implementation: returns are simulated from a normal distribution.<br>- In general: any return distribution can be modeled.<br>- Model parameters (mean $\mu$, volatility $\sigma$) are constant.<br>- Sufficient number of simulations to approximate distribution. | Simulate $N$ portfolio return paths.<br>Deterministic part: $P_0 \mu T$<br>Stochastic part: $P_0 \sigma Z \sqrt{T}$<br><br>$$\Delta P = P_0(\mu T + \sigma Z \sqrt{T})$$<br>$$VaR = -\text{Percentile}(\Delta P, (1-\alpha) \times 100)$$ |
| **Parametric (Variance-Covariance)** | - Portfolio returns are normally distributed.<br>- Constant mean and variance over time.<br>- Portfolio is linear (no significant derivatives). | Analytical solution using $\sigma_p$ and $Z_\alpha$.<br>Time adjustment via $\sqrt{T/252}$.<br><br>$$VaR = P_0 \sigma_p Z_\alpha \sqrt{\frac{T}{252}}$$ |
| **Historical Simulation**       | - Historical returns are representative of future risks.<br>- No specific distributional assumptions.<br>- Past extreme events must be reflected in historical data. | Empirical quantile approach.<br>VaR based on historical percentiles.<br><br>$$VaR = -\text{Percentile}(X, 100 \times (1-\alpha)) \times P_0$$ |

## Acknowledgments

This project was inspired by the tutorials of Ryan O'Connell, CFA, FRM. You can check out his videos here:

- 🎥 [VaR in Python: Monte Carlo Method](https://www.youtube.com/watch?v=X8aNFXJEENs)
- 🎥 [VaR in Python: Parametric Method](https://www.youtube.com/watch?v=n8N1KK_1T50)
- 🎥 [VaR in Python: Historical Method](https://www.youtube.com/watch?v=jZJsPi4j7wQ)

