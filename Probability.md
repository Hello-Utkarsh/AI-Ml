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
