# V.A.R.S Model: Volatility-Adaptive-Robust-Scorer
Created by **Aldo**, a 15-year-old student from Indonesia. 🇮🇩

## 🚀 The Concept
V.A.R.S (also known as **AWSM - Adaptive-Weighted-Scoring-Model**) is a dynamic scoring algorithm designed to handle high-volatility data while maintaining robustness against extreme outliers. 

### 🧠 The Mathematical Formula
$$F(n) = \sum_{i=1}^{n} w_i q'_i + \lambda \cdot \frac{\ln(n+1)}{1+n^\beta}$$

### Key Components:
1. **Softsign Normalization**: $q'_i = \frac{q_i}{1+|q_i|}$ 
   - *Purpose*: Prevents extreme outliers from dominating the entire score.
2. **Volatility Multiplier ($\lambda$)**: Uses $\sigma$ (Standard Deviation) to scale the growth term.
3. **Adaptive Stability ($\beta$)**: $\beta = \frac{1}{1+\sigma}$
   - *Purpose*: Acts as a mathematical "shock absorber" during high chaos.

---

## 💻 Python Implementation (Pure Python)
You can test this model directly without any external libraries:

```python
import math

def vars_awsm_scorer(data):
    n = len(data)
    if n == 0: return 0
    
    # Calculate Mean & Standard Deviation
    mean_val = sum(data) / n
    sigma = math.sqrt(sum((x - mean_val)**2 for x in data) / n)
    
    # Softsign Normalization
    q_prime = [x / (1 + abs(x)) for x in data]
    
    # Parameters
    lambd = sigma
    beta = 1 / (1 + sigma)
    
    # V.A.R.S Final Formula
    growth = (lambd * math.log(n + 1)) / (1 + n**beta)
    return (sum(q_prime) / n) + growth

# Test Scenario
data = [10, 12, 10, 11, 500]
print(f"V.A.R.S Score: {vars_awsm_scorer(data):.4f}")

