# Logistic Regression

Logistic regression is a technique for predicting a probability (a value between 0 and 1) from input features. It does this by transforming a linear combination of features through the **sigmoid** (logistic) function.

---

### 1. Linear Combination (Log‑Odds)

First, compute the **log‑odds** $z$ as you would in linear regression:

$$z = b + w_{1}x_{1} + w_{2}x_{2} + \cdots + w_{N}x_{N}$$

- $b$ is the **bias** (intercept).  
- $w_{i}$ are the **learned weights**.  
- $x_{i}$ are the **feature values** for one example.  

---

### 2. Sigmoid Function

To map $z$ to a probability $y\in(0,1)$, use the sigmoid:

$$y = \frac{1}{1 + e^{-z}}$$

- As $z \to +\infty$, $y \to 1$.  
- As $z \to -\infty$, $y \to 0$.  

---

### 3. Worked Example

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
   
   So the model predicts a probability of **0.731**.

---