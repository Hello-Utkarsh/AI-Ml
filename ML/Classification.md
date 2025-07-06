# Classification: From Probabilities to Classes

Imagine your spam detector shows a sidebar with 0%, 1%, 2%…100% “spam”—that’s useless! We want **labels**, not raw probabilities.

**Classification** predicts which class an example belongs to (e.g., Spam vs. Not Spam) by converting the output of a model like logistic regression into discrete categories.

---

## Threshold

A **Threshold** is simply the cutoff probability you choose to turn a model’s output

Suppose your model predicts a probability $p\in[0,1]$ (e.g., $p=0.50$ → 50% chance of spam; $p=0.75$ → 75% chance). To classify, you pick a cutoff $t$: if $p > t$, label **Spam**; otherwise, **Not Spam**. This *t* is called the **Threshold**

Although $t=0.5$ is a common starting point, it can backfire when spam is extremely rare (say 0.01%) or when marking a real email as spam is worse than missing one. Raising $t$ cuts down on false positives; lowering $t$ catches more spam. Choose $t$ based on class imbalance and whether false alarms or misses are costlier.

# Confusion Matrix

A **confusion matrix** summarizes a binary classifier’s performance by comparing its **predicted** labels (rows) against the **actual** labels (columns). It helps you see not only overall accuracy but also the types of errors your model makes.


### Confusion Matrix Table

|                         | **Actual Spam** (Positive) | **Actual Not Spam** (Negative) |
| ----------------------- | :------------------------: | :----------------------------: |
| **Predicted Spam**      | **True Positive (TP)**     | **False Positive (FP)**        |
| **Predicted Not Spam**  | **False Negative (FN)**    | **True Negative (TN)**         |

### Cell Definitions

- **True Positive (TP)**  
  Model predicts **Spam**, and the email **is** Spam.  
  *Good*: catches real spam.

- **False Positive (FP)**  
  Model predicts **Spam**, but the email **isn’t** Spam.  
  *“False alarm”*: legitimate email wrongly filtered.

- **False Negative (FN)**  
  Model predicts **Not Spam**, but the email **is** Spam.  
  *“Miss”*: spam sneaks into the inbox.

- **True Negative (TN)**  
  Model predicts **Not Spam**, and the email **isn’t** Spam.  
  *Good*: puts spam into bin

### Imbalanced Dataset Example

In spam filtering, “Spam” is often much rarer than “Not Spam.”  
- Total emails: **10 000**  
  - **100** Spam (1%)  
  - **9 900** Not Spam (99%)  

A classifier that always predicts “Not Spam” would be 99% accurate but catch zero spam. The confusion matrix exposes this flaw by breaking down errors.

### Why It Matters

- **Accuracy illusion**: with 99% “Not Spam,” always predicting negative yields 99% accuracy—but zero TP.  
- **Imbalance-aware metrics**: use **precision** and **recall** instead of raw accuracy:  
  - Precision = TP / (TP + FP)  
  - Recall = TP / (TP + FN)  
- **Model adjustments**: consider resampling, threshold tuning, or cost‑sensitive training to handle class imbalance.

---

## Accuracy

**Accuracy** measures the overall fraction of correct predictions:

$$\text{Accuracy} = \frac{TP + TN}{TP + TN + FP + FN}$$

- **TP** (True Positive): correctly predicted Spam  
- **TN** (True Negative): correctly predicted Not Spam  
- **FP** (False Positive): non‑spam flagged as Spam  
- **FN** (False Negative): spam missed and marked Not Spam  

### When It Works

- **Balanced data** (similar counts of Spam and Not Spam):  
  Accuracy gives a quick, coarse‑grained view of performance.

### Caveats

- **Imbalanced data** (e.g., 1% spam, 99% not‑spam):  
  A dumb model that always predicts Not Spam scores 99% accuracy yet catches zero spam. So it is completely failing in the job it was designed to do yet it has 99% accuracy.
- **Unequal error costs**:  
  If missing spam (FN, spam missed and marked Not Spam) is costlier than a false alarm (FP, non‑spam flagged as Spam), accuracy alone won’t capture that trade‑off.

## Takeaways

- Use accuracy as a first check on **balanced** problems.  
- On **imbalanced** datasets or when one error type is more serious, complement or replace it with:
  - **Precision** (focus on FP)  
  - **Recall** (focus on FN)  
  - **F1 score** (harmonic mean of precision & recall)

