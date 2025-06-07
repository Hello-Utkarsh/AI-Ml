# 📈 Linear Regression

Linear regression is a statistical technique used to model the relationship between one or more input variables (features) and an output variable (label) by fitting a linear equation to observed data.

Suppose we want to predict a car’s fuel efficiency (in miles per gallon, MPG) based on its weight (in thousands of pounds). Consider the following dataset:

| Pounds (in 1000s) (feature) | Miles per Gallon (label) |
| --------------------------- | ------------------------ |
| 3.50                        | 18                       |
| 3.69                        | 15                       |
| 3.44                        | 18                       |
| 3.43                        | 16                       |
| 4.34                        | 15                       |
| 4.42                        | 14                       |
| 2.37                        | 24                       |

In algebra, a straight line can be written as:  
y = wx + b

- **y** is the output we want to predict (miles per gallon). The predicted label.
- **x** is the input (pounds of the car, in thousands). A feature.
- **w** is the slope of the line. In ML, this is a parameter learned during training.
- **b** is the y-intercept of the line. In ML, this is also a parameter learned during training.

To fit a straight line through two points \((x₁, y₁)\) and \((x₂, y₂)\), we calculate:

1. **Slope (m)**  
    \[
   m = \frac{y₂ - y₁}{x₂ - x₁}
   \]

   - Choose any two points from the data.
   - Subtract the y-values (outputs) and divide by the difference in x-values (inputs).
     > **Note:** This is a simplified method for estimating slope using just two data points. In actual linear regression, especially with multiple data points, the slope is computed using optimization techniques (like minimizing mean squared error) over the entire dataset.

2. **Bias (b)**  
   Once the slope \(m\) is known, pick one of the two points \((x_i, y_i)\) and solve for \(b\) in:
   \[
   y_i = m·x_i + b
   \quad\Longrightarrow\quad
   b = y_i - m·x_i
   \]
   - The bias is just the intercept where the line crosses the y-axis.

**Example (from our dataset):**

- Pick two points, e.g., \((3.50, 18)\) and \((4.34, 15)\).
  1. Calculate slope:
     \[
     m = \frac{15 - 18}{4.34 - 3.50}
     = \frac{-3}{0.84}
     \approx -3.57
     \]
  2. Calculate bias using \((3.50, 18)\):
     \[
     b = 18 - (-3.57)·3.50
     = 18 + 12.495
     \approx 30.495
     \]
  3. The resulting line is:
     ```
     y = 30.495 + (-3.57)x
     ```
  4. To predict MPG for a 4,000-pound car (\(x = 4.00\)):
     \[
     y = 30.495 + (-3.57)·4.00
     = 30.495 - 14.28
     = 16.215
     \]
     So, approximately 16.2 MPG.

> **Note:** In practice, when fitting a model on many data points, weight and bias are found by minimizing a cost function (e.g., mean squared error) across all points, not just two. The above illustrates how slope and bias relate to any two points on a straight line.

---

## 5. Extending to Multiple Features

A model that relies on multiple features can be written as:

```
y = b + w₁·x₁ + w₂·x₂ + w₃·x₃ + ⋯ + wₙ·xₙ
```

- Each **xₖ** is a distinct feature.
- Each **wₖ** is the corresponding weight for feature xₖ.
- **b** is still the bias term.

**Example (predicting gas mileage):**

- Features might include:
  - Engine displacement (x₁)
  - Acceleration (x₂)
  - Number of cylinders (x₃)
  - Horsepower (x₄)
- Model form with four features:

```
y = b + w₁·(engine displacement)
+ w₂·(acceleration)
+ w₃·(number of cylinders)
+ w₄·(horsepower)
```

## Loss Functions

Loss is a numerical metric that quantifies how wrong a model’s predictions are by measuring the distance between predictions and actual labels. Training aims to minimize loss.

---

## 1. Four Main Loss Types

| Loss type                     | Definition                                                  | Equation                                                                                   |
| ----------------------------- | ----------------------------------------------------------- | ------------------------------------------------------------------------------------------ |
| **L1 loss**                   | Sum of absolute differences between predictions and actuals | \(\displaystyle\sum{} \bigl(\,\text{actual value} - \text{predicted value})^2\)            |
| **Mean Absolute Error (MAE)** | Average of L1 loss over _N_ examples                        | \(\frac{1}{N}\displaystyle\sum{} \bigl(\text{actual value} - \text{predicted value})^2\)   |
| **L2 loss**                   | Sum of squared differences between predictions and actuals  | \( \displaystyle\sum{}\bigl(\text{actual value} - \text{predicted value})^2\)              |
| **Mean Squared Error (MSE)**  | Average of L2 loss over _N_ examples                        | \(\frac{1}{N}\displaystyle\sum{} \bigl(\,\text{actual value} - \text{predicted value})^2\) |

> **Note:** Squaring (in L2/MSE) penalizes large errors more heavily, while absolute value (in L1/MAE) treats all errors linearly.

---

## 2. Calculating Loss Example

Using the previous best fit line, we'll calculate L2 loss. From the best fit line, we had the following values for weight and bias:

Weight = −3.75
Bias = 30.

If the model predicts that a 2,370-pound car gets 21.5 miles per gallon, but it actually gets 24 miles per gallon, we would calculate the L2 loss as follows:

Model prediction: 21.1 MPG for a 2,370-lb car  
Actual: 24 MPG

| Description        | Formula                         | Calculation           | Value      |
| ------------------ | ------------------------------- | --------------------- | ---------- |
| **Actual Value** y | label                           | 24                    | 24 MPG     |
| **Prediction** ŷ   | ŷ = m·x + b                     | ŷ = (−3.75)·2.37 + 30 | ≈ 21.1 MPG |
| **L2 Loss**        | (atualvalue − predicted value)² | (24 − 21.1)²          | ≈ 8.34     |

---

### Choosing Between MAE and MSE

**MAE (Mean Absolute Error)**

- You take each error—big or small—measure how far off you were, and average those distances.

- If one prediction is way off, it affects the average just as much as any other error of the same size.

When to use it:
– You care equally about every point.
– Your data might have some weird values and you don’t want them to pull your line around.

**MSE (Mean Squared Error)**

- You square each error before averaging, so a small error (2 units) contributes 4, but a big error (10 units) contributes 100.

- If you really don’t want your model to ever be wildly off, this will force it to try harder on those tough cases.

When to use it:
- You care more about avoiding large blunders than small slips.
- You’re okay if a few tiny errors happen, as long as you never see a huge surprise.

---

### Intuition with Outliers

- **Outlier in data**: e.g., an 8,000-lb car (outside typical 2,000–5,000 lb range).
- **Outlier in prediction**: e.g., a 3,000-lb car predicted at 40 MPG (outside expected 18–20 MPG).

| Loss type | Behavior                                                           |
| --------- | ------------------------------------------------------------------ |
| **MSE**   | Model shifts toward outliers (large errors carry more weight).     |
| **MAE**   | Model stays closer to the bulk of data (outliers treated equally). |

---
