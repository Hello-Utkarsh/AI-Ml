# Logistic Regression

Logistic regression is a technique for predicting a probability (a value between 0 and 1) from input features. It does this by transforming a linear combination of features through the **sigmoid** (logistic) function.

#### 1. Linear Combination (Log‑Odds)

First, compute the **log‑odds** $z$ as you would in linear regression:

$$z = b + w_{1}x_{1} + w_{2}x_{2} + \cdots + w_{N}x_{N}$$

- $b$ is the **bias** (intercept).
- $w_{i}$ are the **learned weights**.
- $x_{i}$ are the **feature values** for one example.

#### 2. Sigmoid Function

To map $z$ to a probability $y\in(0,1)$, use the sigmoid:

$$y = \frac{1}{1 + e^{-z}}$$

- As $z \to +\infty$, $y \to 1$.
- As $z \to -\infty$, $y \to 0$.

#### Example

Suppose a model has three features with:

- Bias: $b = 1$
- Weights: $w_{1}=2,\;w_{2}=-1,\;w_{3}=5$
- Feature values: $x_{1}=0,\;x_{2}=10,\;x_{3}=2$

1. **Compute $z$:**

$$\begin{aligned}
 z &= b + w_{1}x_{1} + w_{2}x_{2} + w_{3}x_{3} \\
   &= 1 + (2)(0) + (-1)(10) + (5)(2) \\
   &= 1 + 0 - 10 + 10 \\
   &= 1
 \end{aligned}$$

2. **Compute $y$:**

$$\begin{aligned}
 y &= \frac{1}{1 + e^{-z}} = \frac{1}{1 + e^{-1}} \\
   &\approx \frac{1}{1 + 0.36} \\
   &\approx 0.73
 \end{aligned}$$

e = 2.718
So the model predicts a probability of **0.731**.

---

## Log Loss

Log Loss is the error measure function used in **logistic regression**, which predicts probabilities (values between 0 and 1). Lower Log Loss means better predictions.

---

### Log Loss Formula

For **one example** with true label $y\in\{0,1\}$ and predicted probability $\hat{y}\in(0,1)$:

$$\text{Log Loss}
= -\bigl[y \cdot \ln(\hat{y}) \;+\;(1 - y)\cdot \ln(1 - \hat{y})\bigr]$$

- $y$: true label
  - $y=1$ means “positive”
  - $y=0$ means “negative”
- $\hat{y}$: model’s predicted probability that $y=1$
- $\ln(\cdot)$: natural logarithm (base $e\approx2.718$)

---

### Why Not Squared Loss?

- **Squared Loss** (used in linear regression) measures simple distance:
  $$\text{Squared Loss} = (\,y_{\text{true}} - y_{\text{pred}}\,)^2$$
- In logistic regression, predictions are **probabilities** from a sigmoid.
- Squared Loss on probabilities doesn’t punish confident mistakes enough.

Lets understand it with an example

1. **Case $y=1$:**  
   Loss = $-\ln(\hat{y})$

   - If $\hat{y}\approx1$, $\ln(\hat{y})\approx0$ → small loss
   - If $\hat{y}\approx0$, $\ln(\hat{y})\to -\infty$ → large loss

2. **Case $y=0$:**  
   Loss = $-\ln(1 - \hat{y})$
   - If $\hat{y}\approx0$, $1-\hat{y}\approx1$ → small loss
   - If $\hat{y}\approx1$, $1-\hat{y}\to0$ → large loss

---

### Quick Numerical Example

- True $y=1$, predicted $\hat{y}=0.9$:
  $$\text{Loss} = -\ln(0.9) \approx 0.105$$
- True $y=1$, predicted $\hat{y}=0.1$:
  $$\text{Loss} = -\ln(0.1) \approx 2.303$$

Confidently wrong predictions incur much higher penalty than confident correct ones.
