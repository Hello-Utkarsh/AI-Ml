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

## 🎯 Basis / Unit Vectors

**Basis vectors** are special vectors that:
- Have a **magnitude of 1**
- Represent the **direction** of each axis

They are usually written as:
- `î` → unit vector in the **x-direction**
- `ĵ` → unit vector in the **y-direction**
- `k̂` → unit vector in the **z-direction**

---

## 🌌 Span

The **span** of a set of vectors is the collection of all points you can reach using them (by scaling and adding).

- Using `î` and `ĵ`, you can reach any point on a 2D plane → the span is **2D**
- Using `î`, `ĵ`, and `k̂`, you can reach any point in 3D space → the span is **3D**

---

## 📚 Types of Vectors

### 1. Linearly Dependent Vectors
These vectors **don’t add a new direction**. They are just scalar multiples of each other and lie on the same line or axis.

> Example: `3î` and `5î` both lie on the x-axis. One is just a longer/shorter version of the other, but no new direction is introduced.

---

### 2. Linearly Independent Vectors
These vectors **introduce new directions** or dimensions.

> Example: `3î` and `5ĵ` are linearly independent because `î` lies on the x-axis and `ĵ` lies on the y-axis — two different directions.

---

## ➕✖️ How Do We Add or Multiply Vectors?

### ➕ **Vector Addition**

Adding vectors is just like adding numbers **axis-wise**:

[3, 4] + [5, -2] = [3 + 5, 4 + (-2)] = [8, 2]


![Vector Example](./assets/Vector%20Addition1.png)

![Vector Example](./assets/Vector%20Addition2.png)


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

---

## 📐 What is Linear Transformation?

A **linear transformation** is a function that takes vectors as input and transforms them into new vectors, while preserving two key properties:

1. The **origin stays fixed** (no shifting).
2. **Grid lines remain straight and parallel** (lines stay straight and equally spaced).

Think of it as changing the _rulers_ (basis vectors) you use to measure space, not the space itself.

---

### 🧠 Example:

Let’s say you have a vector:

v = [2, 3]


In the **default grid**, this means:
- Move **2 units along the x-axis** → using the standard basis `[1, 0]`
- Move **3 units along the y-axis** → using the standard basis `[0, 1]`

Now, apply a **linear transformation** that changes the basis vectors:

- New x-axis basis vector → `i' = [1, -1]`
- New y-axis basis vector → `j' = [1, 1]`

So instead of building the vector using `[1, 0]` and `[0, 1]`, we now use the new basis:

v' = 2 × [1, -1] + 3 × [1, 1] = [2, -2] + [3, 3] = [5, 1]


This means the vector `[2, 3]` is **mapped to** `[5, 1]` under the new grid.

![Vector Transformation](./assets/Vector%20Transformation.png)

In short: Linear transformations **reshape the grid**, not the space. They give you a new way to describe and work with vectors!

---

## 🌀 Matrix Composition

In linear algebra, transformation matrices can rotate, scale, shear, or reflect vectors. When you apply transformations multiple times, you can **compose** them using matrix multiplication.

## 2D Matrix

### 🔁 One 90° Rotation

The transformation matrix for a **90° counterclockwise rotation** is:

R = [ [ 0, -1 ], [ 1, 0 ] ]


### 🔁🔁 Two 90° Rotations (180° Total)

To rotate a vector 90° **twice**, you multiply the rotation matrix by itself:

R × R = [ [ 0, -1 ], [ [ 0, -1 ], [ 1, 0 ] ] × [ 1, 0 ] ]

  = [ [-1,  0 ],
     [ 0, -1 ] ]


This result is the matrix for a **180° rotation**, which flips both x and y directions.

### ✅ Conclusion

Matrix multiplication lets us **combine transformations**:

- One 90° rotation ➝ `R`
- Two 90° rotations ➝ `R × R = 180° rotation`
- And so on...

By composing matrices, we can stack multiple linear transformations together into one!

## 🔄 Order of Transformations Matters!

When composing transformations using **matrix multiplication**, the **order** in which you multiply them affects the result.

Matrix multiplication is **not commutative**, which means:

A × B ≠ B × A

Let’s say:
- `R` is a **rotation matrix**
- `S` is a **shear matrix**

If you rotate then shear:
Final = S × R (First apply R, then S)

If you shear then rotate:
Final = R × S (First apply S, then R)

These will generally give **different results**, because the transformation is applied **in sequence**, and each one changes the coordinate system for the next.

### ✅ Exception: Same Matrices

In our previous example:
R =  [[ 0, -1 ], [ 1, 0 ] ]

We applied the same rotation matrix twice:
R × R = R² = 180° rotation

Since both matrices were the same, the order didn’t matter **in this special case**. But in general, **always be mindful of the order** when combining transformations!

---

# 📐 Determinants – Explained Simply

A determinant is a scalar value that can be computed from a square matrix. It gives insight into the transformation properties of a matrix—especially area/volume scaling, invertibility, and orientation (flipping).

---

## 🔷 2D Determinant

Given a 2×2 matrix:

| a b | | c d |


The **determinant** is:
det = ad - bc


### What it means:
- `det = 1`: Area unchanged
- `det = 2`: Area doubled
- `det = 0`: Collapsed into a line (not invertible)
- `det < -2`: Flipped across an axis (mirrored) and scaled 2 times

### Example:

Matrix:
| 2 1 | | 1 1 |
det = 2×1 - 1×1 = 1


✅ Area stays the same, but the shape gets sheared.

---

## 🔷 3D Determinant

In 3D, the determinant of a 3×3 matrix gives the volume scaling factor of a parallelepiped formed by three vectors.

Given a 3×3 matrix:
A = | a1  a2  a3 |
    | b1  b2  b3 |
    | c1  c2  c3 |

det(A) = a1(b2c3 - b3c2) - a2(b1c3 - b3c1) + a3(b1c2 - b2c1)

### Example:
| 1 0 0 | | 0 2 0 | | 0 0 3 |
det = 1 × 2 × 3 = 6