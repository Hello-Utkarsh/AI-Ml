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

To fit a straight line through two points $(x₁, y₁)$ and $(x₂, y₂)$, we calculate:

1. **Slope (m)**  
    $m = \frac {y₂ - y₁}{x₂ - x₁}$

   - Choose any two points from the data.
   - Subtract the y-values (outputs) and divide by the difference in x-values (inputs).
     > **Note:** This is a simplified method for estimating slope using just two data points. In actual linear regression, especially with multiple data points, the slope is computed using optimization techniques (like minimizing mean squared error) over the entire dataset.

2. **Bias (b)**  
   Once the slope $m$ is known, pick one of the two points $(x_i, y_i)$ and solve for $b$ in:
   $y_i = m·x_i + b\quad\Longrightarrow\quad b = y_i - m·x_i$
   - The bias is just the intercept where the line crosses the y-axis.

**Example (from our dataset):**

- Pick two points, e.g., $(3.50, 18)$ and $(4.34, 15)$.
  1. Calculate slope:
     $m = \frac{15 - 18}{4.34 - 3.50}= \frac{-3}{0.84}\approx -3.57$
  2. Calculate bias using $(3.50, 18)$:
     $b = 18 - (-3.57)·3.50= 18 + 12.495\approx 30.495$
  3. The resulting line is:
     ```
     y = 30.495 + (-3.57)x
     ```
  4. To predict MPG for a 4,000-pound car ($x = 4.00$):
     $ y = 30.495 + (-3.57)·4.00= 30.495 - 14.28= 16.215$
     So, approximately 16.2 MPG.

> **Note:** In practice, when fitting a model on many data points, weight and bias are found by minimizing a cost function (e.g., mean squared error) across all points, not just two. The above illustrates how slope and bias relate to any two points on a straight line.

---

#### Extending to Multiple Features

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

| Loss type                     | Definition                                                  | Equation                                                                                 |
| ----------------------------- | ----------------------------------------------------------- | ---------------------------------------------------------------------------------------- |
| **L1 loss**                   | Sum of absolute differences between predictions and actuals | $\displaystyle\sum{} \bigl(\,\text{actual value} - \text{predicted value})^2$            |
| **Mean Absolute Error (MAE)** | Average of L1 loss over _N_ examples                        | $\frac{1}{N}\displaystyle\sum{} \bigl(\text{actual value} - \text{predicted value})^2$   |
| **L2 loss**                   | Sum of squared differences between predictions and actuals  | $\displaystyle\sum{}\bigl(\text{actual value} - \text{predicted value})^2$              |
| **Mean Squared Error (MSE)**  | Average of L2 loss over _N_ examples                        | $\frac{1}{N}\displaystyle\sum{} \bigl(\,\text{actual value} - \text{predicted value})^2$ |

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

## Gradient Descent

**Gradient descent** is an iterative method to find the weights and bias that minimize the loss (error) of a linear regression model.

### 1. Initialization

- Set weight $w = 0$ and bias $b = 0$.
- Choose a **learning rate** $\alpha$ (a small positive number, can be anything).
- Decide on the number of iterations (or stop when convergence is reached ie the loss is changing very little or is not changing at all).

---

### 2. Repeat Until Convergence

For each iteration:

#### a. Compute predictions

$\hat y_i = w \, x_i \;+\; b$

- $x_i$: feature value of example $i$
- $\hat y_i$: predicted label for example $i$

#### b. Calculate Mean Squared Error (MSE)

$\frac{1}{M}\sum_{i=1}^M \bigl(\text{actual value} - \text{predicted value})^2$

- $M$: total number of training examples

#### c. Compute gradients (“slopes” of the loss surface)

**Weight derivative**  
$\frac{\partial J}{\partial w} = \frac{1}{M}\sum_{i=1}^M \bigl[\,2\,(\text{predicted value} - \text{actual value})]$

- $x_i$: feature value for example $i$
- The factor 2 comes from differentiating the square $(\text{predicted value} - \text{actual value})^2$.

**Bias derivative**  
$\frac{\partial J}{\partial b} = \frac{1}{M}\sum_{i=1}^M \bigl[\,2\,(\text{predicted value} - \text{actual value})\bigr]$

- No $x_i$ term because $b$ shifts the prediction by a constant amount for every example.

#### d. Update parameters

- **New weight**:  
  $w_{\text{new}}= w_{\text{old}}\;-\;\alpha\,\frac{\partial J}{\partial w}$
- $w_{old}$ is the old previous weight, usually 0 in the starting of the process
- $\alpha$ is a small positive number, can be anything
- $\frac{\partial J}{\partial w}$ is the weight derivative we discussed above
- **New bias**:  
  $b_{\text{new}}= b_{\text{old}}\;-\;\alpha\,\frac{\partial J}{\partial b}$
- $b_{old}$ is the old previous bias, usually 0 in the starting of the process
- $\alpha$ is a small positive number, can be anything
- $\frac{\partial J}{\partial b}$ is the bias derivative we discussed above

### 3. Convergence

- After each update, the loss $J(w,b)$ should decrease.
- Stop when:
  - The change in loss between iterations is very small (converged), or
  - You reach a preset maximum number of iterations.

> **Tip:** If you continue training past convergence, loss will fluctuate slightly around the minimum. To confirm convergence, train until loss stabilizes.

### Implementation

```python
# Initialize parameters
weight = 0  # slope
bias = 0    # intercept
learning_rate = 0.05  # step size for gradient descent

# Training data
data = [
    {"x": 3.50, "y": 18},
    {"x": 3.69, "y": 15},
    {"x": 3.44, "y": 18},
    {"x": 3.43, "y": 16},
    {"x": 4.34, "y": 15},
    {"x": 4.42, "y": 14},
    {"x": 2.37, "y": 24}
]

mse_old = float("inf")  # start with infinity so first comparison always passes

while True:
    predictions = []
    total_error = 0
    weight_sum = 0
    bias_sum = 0

    # Step 1: Calculate predictions and accumulate gradients
    for i in data:
        pred = weight * i['x'] + bias  # predicted value
        predictions.append(pred)

        error = pred - i['y']  # predicted - actual

        total_error += error ** 2  # squared error for MSE
        weight_sum += 2 * error * i['x']  # gradient wrt weight
        bias_sum += 2 * error             # gradient wrt bias

    # Step 2: Compute Mean Squared Error
    mse_new = total_error / len(data)

    # Step 3: Check for convergence
    if mse_old - mse_new > 0.1:  # significant improvement
        mse_old = mse_new
        weight_der = weight_sum / len(data)
        bias_der = bias_sum / len(data)

        # Step 4: Update parameters
        weight -= learning_rate * weight_der
        bias -= learning_rate * bias_der

    else:
        break  # stop training

# Test dataset
test_data = [
    {"x": 3.20, "y": 17},
    {"x": 4.00, "y": 15},
    {"x": 2.80, "y": 22}
]

# Predictions for test data
test_predictions = [weight * i['x'] + bias for i in test_data]

print("Final weight:", weight)
print("Final bias:", bias)
print("Test predictions:", test_predictions)

#output [15.665746860982782, 17.264835505939757, 14.866202538504295]
```

## Hyperparameters

**Parameters vs. Hyperparameters**

- **Parameters**: learned by the model during training (weights `w`, bias `b`).
- **Hyperparameters**: set **before** training to control the learning process.

---

### 1. Learning Rate (α)

- **What it is:** A positive scalar you choose before training.
- **Role in gradient descent:** In each update step, the model computes the gradients (slopes)  
  $\frac{∂J}{∂w},\quad \frac{∂J}{∂b}$  
  and then multiplies them by α to decide **how far** to move $w$ and $b$ downhill:  
  $w_{\text{new}}= w_{\text{old}}- \alpha \;\frac{∂J}{∂w},\quad b_{\text{new}}= b_{\text{old}}- \alpha \;\frac{∂J}{∂b}.$
- **Why it matters:**
  - **Too small** → tiny steps → very slow convergence.
  - **Too large** → bounces around the weights and bias that minimize the loss and may never convergence.
- **Example:** If the gradient is 2.5 and α = 0.01, each parameter changes by  
  $2.5 \times 0.01 = 0.025$ per step.

---

### 2. Batch Size

- **Batch size** is the number of training examples the model uses **before it updates weights and bias**.
- Instead of processing the whole dataset at once, we divide it into smaller groups (batches) to make training faster and more efficient.

#### Types of Batch Processing:

| Type                                  | Description                                                                                |
| ------------------------------------- | ------------------------------------------------------------------------------------------ |
| **Full-batch Gradient Descent**       | Model looks at **all examples** in the dataset before each update.                         |
| **Stochastic Gradient Descent (SGD)** | Model updates after **every single example**. Fast but can fluctuate a lot.                |
| **Mini-batch Gradient Descent**       | Model updates after looking at a **small group** of examples (e.g., 32, 64). Best balance. |

#### Why not use the full dataset every time?

- If the dataset is **very large**, going through all examples before every update takes too long and uses too much memory.
- Mini-batches are like breaking the dataset into smaller, manageable chunks so the model learns faster and more efficiently.

> For example, if your dataset has 1000 examples:
>
> - Full-batch: 1 update after looking at all 1000.
> - SGD: 1000 updates (1 per example).
> - Mini-batch (batch size = 100): 10 updates (1 per batch of 100).

---

### 3. Epochs

- Number of times the model processes the **entire** training set.
- More epochs → more passes → usually better fit (but longer training).

#### Update Frequency Examples

| Method                        | Update Frequency                    | Total Updates (1000 examples, 20 epochs) |
| ----------------------------- | ----------------------------------- | ---------------------------------------- |
| **Full-batch GD**             | After all 1000 examples (per epoch) | 20                                       |
| **Stochastic GD (SGD)**       | After each example                  | 1000 × 20 = 20 000                       |
| **Mini-batch GD** (batch=100) | After every 100 examples            | (1000 / 100) × 20 = 200                  |

---

#### Putting It All Together

1. **Initialize** `w=0`, `b=0`.
2. **Repeat** for each epoch:
   - Shuffle data (optional).
   - Split into batches (according to batch size).
   - For each batch:
     1. Compute predictions $\hat y = w x + b$.
     2. Compute error $\hat y - y$.
     3. Compute gradients  
        $\frac{∂J}{∂w}=\frac{2}{m}\sum(\hat y - y)x,\quad\frac{∂J}{∂b}=\frac{2}{m}\sum(\hat y - y)$  
        where $m$ = batch size.
     4. Update  
        $w \;←\; w - α\,\frac{∂J}{∂w},\quad b \;←\; b - α\,\frac{∂J}{∂b}.$
3. **Stop** when loss stabilizes or max epochs reached.

---

_Keep it simple: pick a moderate batch size (32–128), a learning rate that makes loss drop smoothly, and enough epochs to converge._
