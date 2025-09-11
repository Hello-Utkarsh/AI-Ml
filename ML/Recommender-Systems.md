# Recommender System  

Recommender systems power platforms like Netflix, YouTube, and Spotify by predicting how much a user will like a given item (movie, video, or song).  
At their core, many recommender systems use **linear models** that combine user preferences with item features to estimate ratings.

### Types of Filtering

- **Content-Based Filtering**:  
  Uses explicit features of items (e.g., movies described by how *romantic* or *action-packed* they are).  
  A user’s preferences are learned as weights over these features.  
  Example: Alice likes “romance” a lot, so romantic movies get high predicted ratings for her.  

- **Collaborative Filtering**:  
  Does not rely on predefined item features.  
  Instead, it learns from the **patterns of ratings** across users.  
  Example: If Alice and Carol both liked *Titanic*, and Carol also liked *The Notebook*, then the system may recommend *The Notebook* to Alice.  

Most modern systems are **hybrid**: they combine both approaches for better accuracy.  

In this note, we’ll walk through a **toy example** with movies, their features, and user ratings to understand how this works.  

---

## Content Based Filtering  

This approach assumes we know something about each movie’s features.
We have 5 movies, 4 viewers (Alice, Bob, Carol, David), and two features:  
- $x_1$: Romantic  
- $x_2$: Action  

Each feature is scaled between 0 and 1.  

| Movie             | Alice(1) | Bob(2) | Carol(3) | David(4) | $x_1$ (Romantic) | $x_2$ (Action) |
| ----------------- | -------: | -----: | -------: | -------: | -----------------: | ---------------: |
| La La Land(1)     |        5 |      0 |        4 |        ? |               0.90 |             0.00 |
| Titanic(2)        |        5 |      ? |        ? |        0 |               1.00 |             0.01 |
| The Notebook(3)   |        ? |      0 |        5 |        ? |               0.99 |             0.00 |
| Fast & Furious(4) |        0 |      4 |        0 |        5 |               0.10 |             1.00 |
| F1: The Movie(5)  |        0 |      5 |        0 |        5 |               0.00 |             0.90 |

### Notation  

- Indicator for rating availability
```math
r(i,j) =
\begin{cases}
1 & \text{if viewer j has rated movie i} \\
0 & \text{otherwise}
\end{cases}
```

- Actual rating
$$y(i,j) = \text{rating given by viewer } j \text{ to movie } i$$
- Movie features
```math
x^i = \begin{bmatrix}x_1^i \\ x_2^i \end{bmatrix}
```

**Examples:**  
- $r(5,1) = 0 \;\Rightarrow\;$ Alice has **not** rated the 5th movie, so $y(5,1)$ is undefined.  
- $r(5,4) = 1 \;\Rightarrow\;$ David **has** rated the 5th movie, so $y(5,4) = 5$.  

### How Predictions Work

For each user $j$, we learn a weight vector $w^j$ and bias $b^j$:

$$y^{i,j} = w^j \cdot x^i + b^j$$
This models how much the user cares about romance vs. action.
Example: Suppose Alice’s preferences are
```math 
w^1 = \begin{bmatrix}5\\0\end{bmatrix}
```
This means:

- She loves romance (weight = 5)
- She doesn’t care about action (weight = 0)


```math
w^1 = \begin{bmatrix}5 \\ 0\end{bmatrix}, \quad b^1 = 0
```

This means:  
- She cares a lot about **romance** ($5$)  
- She does not care about **action** ($0$)  

Now, The Notebook has features 
```math
x^3 = \begin{bmatrix}0.99 \\ 0\end{bmatrix}
```

Prediction:

```math
y^{i,j} = \begin{bmatrix} 5 \\ 0 \end{bmatrix} \cdot 
\begin{bmatrix} 0.99 \\ 0 \end{bmatrix} + 0
= 4.95
```

✅ Predicted rating = **4.95**  

### Cost Function (Learning the Parameters)

We don’t set $w^j$ and $b^j$ manually — we learn them by minimizing the error on known ratings.
For user $j$:  

$$
J(w^j, b^j) = \frac{1}{2} \sum_{i: r(i,j)=1} 
\big( w^j \cdot x^i + b^j - y^{i,j} \big)^2
$$  

- The sum runs only over movies that user $j$ has rated.  
- The factor $\tfrac{1}{2}$ simplifies derivatives during optimization.  

To learn parameters for all users simultaneously:  

$$
J(\{w^j, b^j\}) 
= \frac{1}{2} \sum_{j=1}^{n_u} \sum_{i:r(i,j)=1} 
\big( w^j \cdot x^i + b^j - y^{i,j} \big)^2
$$  

---

### Neural Network Based Approach

The linear model we discussed above is mainly a toy example to build intuition. It shows how user preferences and movie features can interact, but it’s too simplistic for real-world recommender systems.

#### Feature Vectors for Users and Movies

- **User vector**: $v_u^j$ → contains features about a user (e.g., age, gender, country, genres they like).  
- **Item (movie) vector**: $v_m^i$ → contains features about a movie (e.g., year, country, genre, average rating, number of reviews).

These two vectors can be of **different sizes** (different number of features).

#### Neural Network Embeddings

- A **dense neural network** is applied separately to user features and item features.  
- Each network compresses its input into a **latent representation (embedding)**:  
- Importantly, both embeddings are designed to be of the **same size**, so we can compare them.

#### Prediction Step  

Once we have embeddings, the **predicted rating or preference** is a dot product between user and item embeddings.

$$
\hat{y}_{u,m} = v_u^j \cdot v_m^i
$$  

#### Training Objective  

We compare predicted rating with actual rating:  

$$
J = \frac{1}{M} \sum_{(u,m)} \bigl( \hat{y}_{u,m} - y_{u,m} \bigr)^2
$$  

This is the **Mean Squared Error (MSE)** cost function.  
We minimize it using **gradient descent** to learn neural network weights.  

#### Similarity Between Items  

If we want to find movies similar to a given movie $m^j$, we can compare embeddings using distance:  

$$
\text{similarity}(m^j, m^k) = \lVert v_m^j - v_m^k \rVert^2
$$  

Smaller values = more similar movies.  
We can then pick the top 5 or 10 closest ones.  

### Retrieval and Ranking  

Modern recommenders work in **two stages**:  

#### 🔹 Retrieval  
- From millions of items, retrieve a smaller candidate set (say 500–1000).  
- Done using **embeddings** + fast similarity search (dot product, cosine, ANN search).  
- Goal = **speed & coverage**, not perfect accuracy.  

Example: Netflix retrieves 500 relevant movies out of 50,000.  

#### 🔹 Ranking  
- Take the retrieved candidates and **rank them in order of preference**.  
- Uses richer features: user profile, item metadata, and context.  
- More complex models (deep nets, boosted trees) are used.  
- Goal = **personalization & accuracy**.  

Example: Netflix re-ranks those 500 and shows you the top 10 on your homepage.

### Principal Component Analysis (PCA)

PCA is a **dimensionality reduction** technique.  It helps us reduce the number of features while still keeping most of the important information.

#### Why PCA?

- In real systems, products/movies/users can have **hundreds of features**.
- Many features are **correlated**. Suppose users rate movies based on two correlated features:
  - "Action level" and "Violence level" (highly correlated)
  - PCA might find PC1: "Intensity" (combines action + violence)  
- PCA combines correlated features into fewer **principal components**, reducing computation while preserving patterns.

#### Intuition

- PCA finds **new axes (directions)** in the data where:
  - Data variance is **maximum** (spread out).
  - Axes are **uncorrelated**.
- We project the original data onto these new axes.
- The first principal component captures the most variance, the second captures the next, etc.

We want axes where data is **spread out** because:
- Spread-out data = more variation = more information.
- Squished data = low variation = less information.

Below is a simple implementation of PCA

```python
import numpy as np
from sklearn.decomposition import PCA

# Data: 5 samples, 2 features
a = np.array([
    [2, 5],
    [3, 7],
    [4, 6],
    [5, 9],
    [6, 8]
])

# PCA to reduce from 2D → 1D
pca = PCA(n_components=1)
x_trans = pca.fit_transform(a)

print(x_trans)
# Output: [[ 2.82842712], [ 0.70710678], [ 0.70710678], [-2.12132034], [-2.12132034]] 
```

## Collaborative Filtering

But wait — how do we get features ($x_1$, $x_2$) for millions of movies?
We can’t always tag every movie as “romantic: 0.7, action: 0.3”.

That’s where collaborative filtering comes in.

Instead of relying on explicit features, we learn the movie features directly from user ratings.

### Learning Movie Features

If we assume user weights $w^j$ are known, we can optimize movie features $x^i$ by minimizing:


$$
J(x^i) = \frac{1}{2} \sum_{i: r(i,j)=1} 
\big( w^j \cdot x^i + b^j - y^{i,j} \big)^2
$$

And across all movies:

$$
J(x^1...x^{n_m}) 
= \frac{1}{2} \sum_{i=1}^{n_m} \sum_{j:r(i,j)=1} 
\big( w^j \cdot x^i + b^j - y^{i,j} \big)^2
$$

### The Joint Cost Function

Bringing it all together:

$$
J(w,b,x) = \frac{1}{2} \sum_{i,j:r(i,j)=1} 
\big( w^j \cdot x^i + b^j - y^{i,j} \big)^2
$$

Now we update both user and movie parameters with gradient descent:

- $w^j = w^j - \alpha \frac{\partial}{\partial{w^j}}$
- $b^j = b^j - \alpha \frac{\partial}{\partial{b^j}}$
- $x^i = x^i - \alpha \frac{\partial}{\partial{x^i}}$

## From Ratings to Binary Feedback in Recommender Systems

In theory, we can predict what rating a user might give to a movie by learning from movie features and past ratings.
But in practice — how many times have you actually rated a movie on Netflix, a product on Amazon, or a song on Spotify?
**Very rarely.**

#### The Reality

In the real world, explicit ratings are scarce. Most users never give star ratings. Instead, platforms rely on implicit signals:

- Did the user like the movie or not?
- Did they wishlist or bookmark it?
- Did they watch the full trailer or leave early?
- Did they replay a song multiple times?

These actions provide binary labels:
- 1 → user liked/engaged with the item
- 0 → user did not like/disengaged
- ? → user has not interacted yet

| Movie             | Alice(1) | Bob(2) | Carol(3) | David(4) |
| ----------------- | -------: | -----: | -------: | -------: |
| La La Land(1)     |        1 |      0 |        1 |        ? |
| Titanic(2)        |        1 |      ? |        ? |        0 |
| The Notebook(3)   |        ? |      0 |        1 |        ? |
| Fast & Furious(4) |        0 |      1 |        0 |        1 |
| F1: The Movie(5)  |        0 |      1 |        0 |        1 |

### Logistic Regression in Recommender Systems

For a user $j$ and a movie $i$, we first compute a **linear score**:  

$$
z^{(i,j)} = w^j \cdot x^i + b^j
$$  

- $w^j$: user’s preference weights  
- $x^i$: movie’s feature vector (learned or predefined)  
- $b^j$: user bias  

To convert $z$ into a probability between 0 and 1, we apply the **sigmoid function**:  

$$
\hat{y}^{(i,j)} = \frac{1}{1 + e^{-z^{(i,j)}}}
$$  

- $\hat{y}^{(i,j)}$: probability that user $j$ will like movie $i$

The model is trained using the **log loss** (cross-entropy loss).  

For a single user–movie pair $(i,j)$ with true label $y^{(i,j)}$:  

$$
L(\hat{y}^{(i,j)}, y^{(i,j)}) = -\Bigl[ \hat{y}^{(i,j)} \cdot \ln(\hat{y}^{(i,j)}) + (1 - \hat{y}^{(i,j)}) \cdot \ln(1-\hat{y}^{(i,j)}) \Bigr]$$

- If $y=1$, loss is small only when $y^{(i,j)}$ is close to 1.  
- If $y=0$, loss is small only when $y^{(i,j)}$ is close to 0.

Summing over all known interactions:  

$$
J(w,b,x) = \sum_{(i,j):r(i,j)=1} L(\hat{y}^{(i,j)}, y^{(i,j)})
$$

## Mean Normalization in Recommender Systems

### Problem: User Rating Bias

Different users have different rating habits that can bias the recommendation model:

- **Generous raters**: Frequently give 4-5 star ratings
- **Strict raters**: Rarely exceed 3 stars, even for items they enjoy
- **Conservative raters**: Tend to rate around the middle (2-3 stars)

Without accounting for these differences, the model may incorrectly learn that a "3" from a strict rater means the same as a "3" from a generous rater.

### Solution: Mean Normalization

Mean normalization adjusts each user's ratings relative to their personal average, removing individual rating bias.

#### Step 1: Calculate User Means

For each user j, compute their average rating:

$$\mu^j = \frac{1}{|R_j|} \sum_{i \in R_j} y^{(i,j)}$$

Where:
- $R_j$ = set of items rated by user j
- $|R_j|$ = number of items rated by user j
- $y^{(i,j)}$ = actual rating given by user j to item i

#### Step 2: Normalize Training Data

Transform the ratings by subtracting the user mean:

$$\hat{y}^{(i,j)} = y^{(i,j)} - \mu^j$$

**Example**:
- Alice (generous rater): μ¹ = 4.2
- Bob (strict rater): μ² = 2.1
- Both rate a movie as "3"
- Normalized: Alice = 3 - 4.2 = -1.2, Bob = 3 - 2.1 = +0.9
- Now the model learns Alice disliked it, Bob liked it!

#### Step 3: Train on Normalized Data

Use the normalized ratings in the cost function:

$$J(w,b,x) = \frac{1}{2} \sum_{i,j:r(i,j)=1} \big( w^j \cdot x^i + b^j - y'^{(i,j)} \big)^2$$

#### Step 4: Make Predictions

When predicting for user j on item i, add back the user's mean:

$$\hat{y}^{(i,j)} = (w^j \cdot x^i + b^j) + \mu^j$$

### Benefits

1. **Removes rating bias**: Model learns relative preferences, not absolute scales
2. **Improves accuracy**: Better captures true user preferences
3. **Fair comparisons**: Generous and strict raters are normalized to the same scale
4. **Stable training**: Reduces variance in the training data

### Limitations

1. **Doesn't solve cold-start**: New users have no rating history, so μʲ is undefined
2. **Requires sufficient ratings**: Users with very few ratings may have unreliable means
3. **Static normalization**: Doesn't adapt as user preferences evolve over time

#### Alternative: Global Mean for New Users

For users with insufficient rating history:

$$\mu^j = \frac{1}{N} \sum_{i,j:r(i,j)=1} y^{(i,j)}$$

Where N is the total number of known ratings across all users.
