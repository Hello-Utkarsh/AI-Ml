# Linear Algebra

## 📐 What is a Vector?

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

- In a 2D vector like

```
|3|
|4|
```

- `3` → movement along the **x-axis**
- `4` → movement along the **y-axis**
- In a 3D vector like

```
|3|
|4|
|5|
```

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

```
| 3 |     | 5 |     | 3 + 5 |      | 8 |
| 4 |  +  |-2 |  =  | 4 + (-2) | = | 2 |
```

![Vector Example](./assets/Vector%20Addition1.png)

![Vector Example](./assets/Vector%20Addition2.png)

**Visual Interpretation**:

- Go `3m` east and `4m` north →

```
| 3 |
| 4 |
```

- Then go `5m` east and `2m` south →

```
| 5  |
|-2  |
```

- Final position: `8m` east, `2m` north →

```
| 3 |     | 5 |     | 3 + 5 |     | 8 |
| 4 |  +  |-2 |  =  | 4 + (-2) | = | 2 |
```

### ✖️ **Vector Multiplication**

There are two main types:

#### 1. **Scalar Multiplication**

Multiply each element of the vector by a scalar (just a number):

```
3 × | 1 | = | 3 |
    | 2 |   | 6 |
```

**In physics terms**:  
Going `1m` east and `2m` north, 3 times in a row, lands you at `3m` east and `6m` north.

---

## 📐 What is Linear Transformation?

A **linear transformation** is a function that takes vectors as input and transforms them into new vectors, while preserving two key properties:

1. The **origin stays fixed** (no shifting).
2. **Grid lines remain straight and parallel** (lines stay straight and equally spaced).

Think of it as changing the _rulers_ (basis vectors) you use to measure space, not the space itself.

### 🧠 Example:

Let’s say you have a vector:

```
v = | 2 |
    | 3 |
```

In the **default grid**, this means:

- Move **2 units along the x-axis** → using the standard basis

```
|1|
|0|
```

- Move **3 units along the y-axis** → using the standard basis

```
|0|
|1|
```

Now, apply a **linear transformation** that changes the basis vectors:

- New x-axis basis vector →

```
i′ = | 1 |
     |-1 |
```

- New y-axis basis vector →

```
j′ = | 1 |
     | 1 |
```

So instead of building the vector using `[1, 0]` and `[0, 1]`, we now use the new basis:

```
v′ = 2 × i′ + 3 × j′
   = 2 × | 1 | + 3 × | 1 |
         |-1 |       | 1 |

   = | 2 | + | 3 | = | 5 |
     |-2 |   | 3 |   | 1 |
```

This means the vector `[2, 3]` is **mapped to** `[5, 1]` under the new grid.

![Vector Transformation](./assets/Vector%20Transformation.png)

In short: Linear transformations **reshape the grid**, not the space. They give you a new way to describe and work with vectors!

---

## 🌀 Matrix Composition

In linear algebra, transformation matrices can rotate, scale, shear, or reflect vectors. When you apply transformations multiple times, you can **compose** them using matrix multiplication.

### 2D Matrix

#### 🔁 One 90° Rotation

The transformation matrix for a **90° counterclockwise rotation** is:

```
R = | 0   1 |
    |-1   0 |
```

#### 🔁🔁 Two 90° Rotations (180° Total)

To rotate a vector 90° **twice**, you multiply the rotation matrix by itself:

```
R × R =
| 0   1 |     | 0   1 |
| -1  0 |  ×  | -1  0 |

[0][0] = (0 × 0) + (1 × -1) = 0 + (-1) = -1
[0][1] = (0 × 1) + (1 × 0)  = 0 + 0     = 0
[1][0] = (-1 × 0) + (0 × -1) = 0 + 0    = 0
[1][1] = (-1 × 1) + (0 × 0)  = -1 + 0   = -1

= | -1   0 |
  |  0  -1 |
```

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

```
R = | 0   1 |
    |-1   0 |
```

We applied the same rotation matrix twice:
R × R = R² = 180° rotation

Since both matrices were the same, the order didn’t matter **in this special case**. But in general, **always be mindful of the order** when combining transformations!

---

## 📐 Determinants

A determinant is a scalar value that can be computed from a square matrix. It gives insight into the transformation properties of a matrix—especially area/volume scaling, invertibility, and orientation (flipping).

---

### 🔷 2D Determinant

Given a 2×2 matrix:

```
| a b |
| c d |
```

The **determinant** is:
det = ad - bc

#### What it means:

- `det = 1`: Area unchanged
- `det = 2`: Area doubled
- `det = 0`: Collapsed into a line
- `det < -2`: Flipped across an axis (mirrored) and scaled 2 times

#### Example:

Matrix:

```
| 2 1 |
| 1 1 |
```

det = 2×1 - 1×1 = 1

✅ Area stays the same, but the shape gets sheared.

---

### 🔷 3D Determinant

In 3D, the determinant of a 3×3 matrix gives the volume scaling factor of a parallelepiped formed by three vectors.

Given a 3×3 matrix:

```
A = | a1 a2 a3 |
    | b1 b2 b3 |
    | c1 c2 c3 |
```

det(A) = a1(b2c3 - b3c2) - a2(b1c3 - b3c1) + a3(b1c2 - b2c1)

#### Example:

```
| 1 0 0 |
| 0 2 0 |
| 0 0 3 |
```

det = 1(6-0) - 0(0-0) + 0(0-0) = 6

---

## 🔄 Inverse Matrices, Column Space, and Null Space

### 🧼 Inverse Matrix (The Undo Button)

An **inverse matrix** undoes the effect of a transformation.

🟢 Example:  
If a transformation rotates a vector **90° clockwise**, the inverse matrix will rotate it **90° counterclockwise**, bringing it back to its original position.

📌 Mathematically:
If `A` is a matrix and `A⁻¹` is its inverse, then:
A × A⁻¹ = I
Where `I` is the **identity matrix**

```
| 1   0 |
| 0   1 |
```

(does nothing — like multiplying by 1).

---

### 🔢 Rank (How Many Dimensions Survive?)

The **rank** of a matrix tells you how many **independent directions** survive after transformation.

🟢 Example 1:
If a transformation **flattens** everything onto the x-axis, you lose the y-dimension.  
✅ Only x-dimension survives → **Rank = 1**

🟢 Example 2:
If a matrix just **rotates** the 2D space (like 90° rotation), both x and y dimensions stay alive.  
✅ Both directions stay → **Rank = 2**

📌 In 3D:

- If all space collapses to a plane → Rank = 2
- If it collapses to a line → Rank = 1
- If nothing collapses → Rank = 3

---

### 🧱 Column Space (All Possible Outputs)

The **column space** of a matrix is the collection of all **possible outputs** you can get by multiplying the matrix with different input vectors.

🟢 Example:
If your matrix can transform vectors to reach any point on a plane, then:
✅ Column space = The whole plane  
If all outputs lie on a single line →  
✅ Column space = That line only

Think of column space as:

> “Where can this transformation take us?”

---

### 🕳️ Null Space (What Gets Crushed?)

The **null space** is the set of all input vectors that get sent to the **zero vector** (i.e., disappear).

🟢 Example:
If a matrix turns every vector on the y-axis into

```
|0|
|0|
```

then:
✅ All those vectors are in the **null space**  
They're lost after the transformation — like flattening paper into a line.

📌 If:
A × x = 0

Then `x` is part of the null space of matrix `A`.

---

### Nonsquare matrices

Not all transformation matrices are square! A **nonsquare matrix** either increases or decreases the number of dimensions during transformation.

#### 🟩 What does a 3×2 Matrix Mean?

A `3 × 2` matrix has:

- 3 rows → **3D output**
- 2 columns → **2D input**

It **transforms 2D vectors into 3D vectors**.

**Example:**

```
A = |  2   0 |
    | -1   1 |
    | -2   1 |
```

This means the 2D basis vectors `[1, 0]` and `[0, 1]` get mapped into 3D:

- x-axis → `[2, -1, -2]`
- y-axis → `[0, 1, 1]`

So a 2D vector like `[3, 1]` becomes:

```
A × v
   = 3 × | 2 | + 1 × | 0 |
         | -1 |   | 1 |
         | -2 |   | 1 |

   = | 6  | + | 0 |
     | -3 |   | 1 |
     | -6 |   | 1 |

   = | 6  |
     | -2 |
     | -5 |
```

This is **useful for lifting lower-dimensional data into a higher-dimensional space**, such as in machine learning or graphics.

---

#### 🟨 What does a 2×3 Matrix Mean?

A `2 × 3` matrix has:

- 2 rows → **2D output**
- 3 columns → **3D input**

It **transforms 3D vectors into 2D vectors**.

**Example:**

```
A = | 1  0  2 |
    | 0 -1  3 |
```

This means:

- x-axis `[1, 0, 0]` → `[1, 0]`
- y-axis `[0, 1, 0]` → `[0, -1]`
- z-axis `[0, 0, 1]` → `[2, 3]`

So a 3D vector like `[1, 2, 1]` becomes:

```
A × v =
= 1 × | 1 | + 2 × | 0 | + 1 × | 2 |
      | 0 |       | -1 |      | 3 |

= | 1 | + | 0 | + | 2 |
  | 0 |   | -2 |  | 3 |

= | 3 |
  | 1 |
```

This is like **projecting a 3D object onto a 2D plane** — similar to how a camera projects the 3D world onto your screen.

---

## 🔸 Dot Products

The **dot product** is a way to measure how much two vectors "agree" in direction.

Think of it like asking:  
👉 _"How much of one vector goes in the direction of the other?"_

### ✅ Simple Rule:

If you have two vectors **A** and **B**, the dot product is:

A · B = |A| × |B| × cos(θ)

Where:

- `|A|` and `|B|` are lengths (magnitudes) of the vectors, which is calculated by `|A| = √(x² + y²)`
- `θ` is the angle between them

### 📌 Interpretation:

- **Positive (+)** → Vectors point in **same direction**
- **Zero (0)** → Vectors are **perpendicular**
- **Negative (-)** → Vectors point in **opposite direction**

#### 💡 Example:

Let’s say:

```
A = |2|
    |4|
B = |3|
    |1|
```

**Dot product =** `(2 × 3) + (4 × 1) = 6 + 4 = 10` → positive  
✅ So the angle between them is **less than 90°**

#### 🔁 Geometric Way to See It:

Imagine dropping a shadow (projection) of one vector onto the other.

- If the shadow goes in the same direction → +ve
- Opposite direction → -ve
- No shadow (perpendicular) → 0

---

## ✖️ Cross Product

The **cross product** of two 3D vectors is a vector that:

- Is **perpendicular** to both the original vectors.
- Has a **magnitude equal to the area** of the parallelogram formed by the two vectors.
- Follows the **right-hand rule** for direction.

### 📐 Formula

If

```
a =  | a₁ |
     | a₂ |
     | a₃ |

b =  | b₁ |
     | b₂ |
     | b₃ |
```

then:

```
a × b =  | a₂·b₃ − a₃·b₂ |
         | a₃·b₁ − a₁·b₃ |
         | a₁·b₂ − a₂·b₁ |
```

#### ✅ Example

Let’s say:

```
a =  | 2 |
     | 3 |
     | 4 |

b =  | 5 |
     | 6 |
     | 7 |

a × b = | (3×7 − 4×6) |
        | (4×5 − 2×7) |
        | (2×6 − 3×5) |

      = | (21 − 24) |
        | (20 − 14) |
        | (12 − 15) |

      = | -3 |
        |  6 |
        | -3 |
```

This result `[-3, 6, -3]` is a new vector that is **orthogonal (perpendicular)** to both `a` and `b`.

### ✋ Right-Hand Rule

To find the direction of the cross product:

- Point your **index finger** in the direction of **vector a**.
- Point your **middle finger** in the direction of **vector b**.
- Your **thumb** will point in the direction of **a × b**.

---

## 🧠 Solving for Original Vectors: Different Methods Explained

Sometimes, you're given the **final vector after transformation** and the **transformation matrix**, and you want to find the **original vector**. Here are a few ways to do that:

### 🔁 1. **Cramer's Rule**

**Cramer's Rule** is a method used to solve a system of linear equations using **determinants**. It is based on the formula:

x = det(A_x) / det(A) y = det(A_y) / det(A)

- `A` is the transformation matrix.
- `A_x` is the matrix formed by replacing the **x-column** of `A` with the result vector.
- `A_y` is the same but for the **y-column**.

#### ❌ Might fail if:

- `det(A) = 0` → No unique solution.
- System is too large (inefficient for high dimensions).

---

### 🔄 2. **Transpose and Inverse Method**

This is the standard **linear algebra approach**:

Original vector = A⁻¹ × Transformed vector

Where:

- `A⁻¹` is the **inverse** of the transformation matrix.

You can find the inverse using various methods, including the transpose+determinant for 2×2 matrices:

```
A = | a   b |
    | c   d |

A⁻¹ = (1 / det(A)) × |  d  -b |
                     | -c   a |
```

#### ❌ Might fail if:

- `A` is **not invertible** if `det(A) = 0`
- Not suitable for systems with many dependent rows.

---

### 📐 3. **Area-Based / Determinant Logic**

In 2D, if you're dealing with geometric vectors, you can relate **areas** formed by the vector and basis axes. The determinant gives the **scaled area** after transformation.

Area_after = |det(T)| × Area_before

You can use this to back-calculate values if you know the transformed vector forms the same area.

### ❌ Might fail if:

- Vectors aren't in 2D or don't form a parallelogram.
- Non-linear or partial transformations are applied.

---

## 🔄 Changing the Basis

When different people use **different coordinate systems (basis vectors)**, the same point or vector in space can have **different coordinates**. Changing the basis allows you to **translate a vector from one coordinate system to another**.

### 🧑‍🏫 Intuition

- **Person A** uses the **standard basis**:

```
   î = |1|
       |0|
   ĵ = |0|
       |1|
```

- **Person B** uses a **different basis**:

```
   î = | 2|
       |-1|
   ĵ = |1|
       |2|
```

from B's perspective it is [1,0] and [0,1] as it is their basis vectors

The same point in space will have **different coordinates** depending on the basis you're using.

---

### 🔧 Problem

Convert a vector `v = [3, 2]` (in Person A's basis) into **Person B's grid**.

#### 🔁 Step 1: Build the basis matrix of Person B

This matrix has Person B's basis vectors as its columns:

```
B = |2 -1|
    |1  2|
```

#### 🔁 Step 2: Invert the basis matrix

We use the **inverse of B** to convert from standard grid to B's grid:

```
B⁻¹ = (1/det) x | 2 -1|
                | 1  2|
First, compute the determinant:
det(B) = (2)(2) - (-1)(1) = 4 + 1 = 5
So,
B⁻¹ = (1/5) x |2 -1|
              |1  2|
```

#### 🧮 Step 3: Multiply by the inverse

To convert `[3, 2]` to Person B's basis:

```
v_b = B⁻¹ × |3|
            |2|
v_b = (1/5) × | 2  -1 | × |3|
              |-1   2 |   |2|

  = (1/5) × | 2×3 + (-1)×2|
            |-1×3 +    2×2|
  = (1/5) × | 6 - 2|
            |-3 + 4|
  = (1/5) × |4|
            |1|
  = |0.8|
    |0.2|
```

---

## Eigenvectors and Eigenvalues

- **Eigenvectors** are special vectors that, when a linear transformation is applied, **do not change direction** — they only get **stretched or squished**.
- The amount they are stretched or squished is called the **Eigenvalue**.

Mathematically:
`(A - λI)v = 0` or equivalently:  
`Av = λv`  
Where:

- `A` is a square matrix (transformation)
- `v` is the eigenvector
- `λ` (lambda) is the eigenvalue
- `I` is the identity matrix

---

### Intuition

- Most vectors change direction when transformed.
- **Eigenvectors** don’t — they stay on the same line (span).
- Only their **length changes**, scaled by the **eigenvalue**.

---

### Why Are They Useful?

- They reveal the **underlying structure** of transformations.
- In **PCA (Principal Component Analysis)**, the **eigenvectors of the covariance matrix** give the directions of maximum variance (new axes).
- They help in **dimensionality reduction**, **stability analysis**, **quantum computing**, and more.

---

### Real Example Use Case

Suppose we want to convert coordinates between two different grids (basis vectors).  
Instead of working with arbitrary basis vectors, we can use the **eigenvectors** of the transformation matrix — because they simply scale.  
This makes computations and interpretations much easier.

---
