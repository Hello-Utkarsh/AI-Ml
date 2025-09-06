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
  $$
  r(i,j) =
  \begin{cases}
  1 & \text{if viewer j has rated movie i} \\
  0 & \text{otherwise}
  \end{cases}
  $$

- Actual rating
  $$ y(i,j) = \text{rating given by viewer } j \text{ to movie } i $$  

- Movie features
  $$ x^i = \begin{bmatrix}x_1^i \\ x_2^i \end{bmatrix} $$  

**Examples:**  
- $ r(5,1) = 0 \;\Rightarrow\; $ Alice has **not** rated the 5th movie, so $y(5,1)$ is undefined.  
- $ r(5,4) = 1 \;\Rightarrow\; $ David **has** rated the 5th movie, so $y(5,4) = 5$.  

## How Predictions Work

For each user $j$, we learn a weight vector $w^j$ and bias $b^j$:

$$ y^{i,j} = w^j \cdot x^i + b^j $$
This models how much the user cares about romance vs. action.
Example: Suppose Alice’s preferences are
$w^1 = \begin{bmatrix}5\\0\end{bmatrix}$
This means:

- She loves romance (weight = 5)
- She doesn’t care about action (weight = 0)


$$ w^1 = \begin{bmatrix}5 \\ 0\end{bmatrix}, \quad b^1 = 0 $$  

This means:  
- She cares a lot about **romance** ($5$)  
- She does not care about **action** ($0$)  

Now, The Notebook has features $ x^3 = \begin{bmatrix}0.99 \\ 0\end{bmatrix} $  

Prediction:

$$
y^{i,j} = \begin{bmatrix} 5 \\ 0 \end{bmatrix} \cdot 
\begin{bmatrix} 0.99 \\ 0 \end{bmatrix} + 0
= 4.95
$$  

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