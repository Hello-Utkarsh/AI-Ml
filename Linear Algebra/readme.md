# 📐 What is a Vector?

Vectors are fundamental to understanding concepts in **physics**, **mathematics**, and **computer science** — and each field brings its own perspective:

- **According to Physics**:  
  A vector is an **arrow** pointing in space with a specific **length** (magnitude) and **direction**.

- **According to Computer Science**:  
  A vector is an **ordered list of numbers**, often used in programming and data structures.

- **According to Mathematics**:  
  A vector is a **quantity that has both magnitude and direction**, and is usually represented as an **ordered tuple of numbers** in a coordinate system — combining the intuition from both physics and computer science.

---

## 🧭 What Does a Vector Even Look Like?

> _“A vector starts at the origin and points to a location in space.”_

![Vector Example](./assets/Vector%20Exp.png)

The values in a vector tell us how far and in which direction we move from the origin:

- In a 2D vector like `[3, 4]`,  
  - `3` → movement along the **x-axis**  
  - `4` → movement along the **y-axis**
- In a 3D vector like `[3, 4, 5]`,  
  - `5` → movement along the **z-axis**

It’s like a set of instructions:  
> "Go 3 units to the right, then 4 units up" You’ve moved to the point `(3, 4)`.

---

## ➕✖️ How Do We Add or Multiply Vectors?

### ➕ **Vector Addition**

Adding vectors is just like adding numbers **axis-wise**:

[3, 4] + [5, -2] = [3 + 5, 4 + (-2)] = [8, 2]


**Visual Interpretation**:  
- Go `3m` east and `4m` north → `[3, 4]`
- Then go `5m` east and `2m` south → `[5, -2]`  
- Final position: `8m` east, `2m` north → `[8, 2]`

### ✖️ **Vector Multiplication**

There are two main types:

#### 1. **Scalar Multiplication**

Multiply each element of the vector by a scalar (just a number):

3 × [1, 2] = [3, 6]


**In physics terms**:  
Going `1m` east and `2m` north, 3 times in a row, lands you at `3m` east and `6m` north.