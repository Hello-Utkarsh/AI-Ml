# Clustering: Beginner Introduction

## What is Clustering?

Clustering is an **unsupervised learning** technique used to group similar data points together.

It is different from classification (like logistic regression), where we know the categories (labels) in advance. In clustering, **we don't know the labels**, and the algorithm tries to **discover natural groupings** in the data.

### Clustering vs Classification

| Feature | Classification (e.g., Logistic Regression) | Clustering |
|--------|---------------------------------------------|------------|
| Labels | ✅ Yes (e.g., spam or ham) | ❌ No (e.g., unknown topics in news) |
| Goal | Predict known categories | Discover groups from data |
| Type | Supervised Learning | Unsupervised Learning |


### 💡 Example

- **Classification**: You have emails labeled as **spam** or **not spam**, and your goal is to train a model to predict these labels.
- **Clustering**: You have a large collection of **unlabeled news articles**. You want to group them into topics like **sports**, **finance**, **national**, **international**, etc., even though you don’t know in advance which article belongs to which group.

---

## K-Means Clustering

K-Means is a popular **unsupervised learning algorithm** used to group data into **K clusters**, based on similarity.


### How K-Means Works

1. **Choose the number of clusters (K)**.

2. **Randomly select K points** in the dataset as the initial **centroids** (cluster centers).

3. **Assign each data point** to the **closest centroid**, forming K groups.

4. **Calculate the average (mean) of all data points in each group** to get new centroids.

5. **Repeat steps 3 and 4**:
   - Reassign points to the new nearest centroid
   - Recalculate the centroid of each cluster

6. **Stop when centroids no longer change** (i.e., the average of each group equals the current center).

### 🧠 Intuition

K-Means starts with a guess (random centers) and **keeps improving groupings** by:
- Assigning points to the closest center
- Updating centers based on the new group

This loop continues until the centers **stabilize** (don’t move anymore).

### Cost Function

The **cost function** in K-Means represents the **total error** between each data point and the centroid of its assigned cluster.

$$
J = \frac{1}{m} \sum_{i=1}^{m} \left\| x^{(i)} - \mu_{c(i)} \right\|^2
$$

- **\( m \)** → Total number of data points
- **\( x^{(i)} \)** → The \( i \)-th data point in the dataset
- **\( c(i) \)** → The index of the cluster that point \( x^{(i)} \) is assigned to
- **\( \mu_{c(i)} \)** → The centroid (mean) of the cluster that point \( x^{(i)} \) belongs to
- **\( \| x^{(i)} - \mu_{c(i)} \|^2 \)** → The squared Euclidean distance between the point and its cluster's centroid

Intution: 
- For each data point:
  - Measure how far it is from its cluster center
  - Square the distance (to penalize larger errors)
- Add up these distances for all points
- Divide by the number of points to get the **average cost**

---