# Probability
## Introduction

Probability measures how likely an event is to occur, on a scale from 0 (impossible) to 1 (certain). Below are the key concepts we have covered:

* **Sample space (S)**: the set of all possible outcomes.
* **Event (A)**: any subset of the sample space.
* **Probability of an event** (for equally likely outcomes):
  $P(A) = \frac{|A|}{|S|}$
* **Notation**:

  * $P(A)$ denotes the probability that event $A$ occurs.
  * For a random variable $X$, $P(X = x)$ is the probability that $X$ takes value $x$.
* **Complement of an event**: the event that $A$ does not occur, denoted $A^c$, with
  $P(A^c) = 1 - P(A) = \frac{|S| - |A|}{|S|}.$

**Example: Rolling a fair six-sided die**

* Sample space: $S = \{1,2,3,4,5,6\}$.
* Event "roll a 6": $A = \{6\}$, so $|A| = 1$ and $|S| = 6$.

Probability of rolling a 6:
$P(A) = \frac{1}{6} \approx 0.17$
Probability of not rolling a 6:
$P(A^c) = 1 - \tfrac{1}{6} = \tfrac{5}{6} \approx 0.83$

---

## Disjoint Events (Mutually Exclusive)

Two events are **disjoint** if they cannot occur at the same time. In other words, they have no outcomes in common.

### Definition:
$$A \cap B = \emptyset$$
$$P(A \cap B) = 0$$

### Rule:
If events A and B are disjoint:  
$$P(A \cup B) = P(A) + P(B)$$

### Example:
- Event A = {1, 2} (rolling a 1 or 2)  
- Event B = {5, 6} (rolling a 5 or 6)  
- These are disjoint because no outcome is shared.  
- So:  
  $$P(A \cup B) = P(A) + P(B) = \frac{2}{6} + \frac{2}{6} = \frac{4}{6} = 0.67$$

---

## Joint (Overlapping) Events

These are events that can both occur; they share some common outcomes.

#### Rule:
$$P(A \cup B) = P(A) + P(B) - P(A \cap B)$$

#### Example:
- Event A = {2, 4, 6} (even numbers)  
- Event $$B = {4, 5, 6} (greater than 3)  
- Overlap: $$A \cap B = \{4, 6\}$$  
- So:  
  $$P(A) = \frac{3}{6},\quad P(B) = \frac{3}{6},\quad P(A \cap B) = \frac{2}{6}$$  
  $$P(A \cup B) = \frac{3}{6} + \frac{3}{6} - \frac{2}{6} = \frac{4}{6}$$

---

## Independent Events

Two events are **independent** if the occurrence of one does **not affect** the probability of the other.

### Definition:
$$P(A \cap B) = P(A) \cdot P(B)$$

### Example: Rolling a die twice
- Let A = first roll is 6 → $$P(A) = \frac{1}{6}$$  
- Let B = "second roll is 6" → $$P(B) = \frac{1}{6}$$  
- The rolls are independent, so:  
  $$P(A \cap B) = \frac{1}{6} \cdot \frac{1}{6} = \frac{1}{36}$$

### Note:
- **Disjoint** events cannot occur together (if one happens, the other can't) → always dependent if P > 0.
- **Independent** events can occur together, but don’t influence each other.
