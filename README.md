
# Chi-Square Test in Statistics

---

## What is the Chi-Square Test?

The **Chi-Square Test (χ² test)** is a statistical test used to determine whether there is a **significant association between two categorical variables** or whether a **categorical variable follows an expected distribution**.

There are **two main types**:

1. **Chi-Square Test of Independence** – tests if two categorical variables are related.
2. **Chi-Square Goodness-of-Fit Test** – tests if a single categorical variable fits an expected distribution.

---

## Why Is It Called "Chi-Square"?

"Chi" (pronounced "kai") is a Greek letter: **χ**. The test statistic calculated follows a **Chi-Square distribution** under the null hypothesis, hence the name.

---

## Real-Life Analogy

Imagine you're in charge of hiring in a company. You suspect that the department someone works in affects whether they get promoted. You survey data on promotions and departments.

* If **promotion and department are related**, then promotions are **not independent** of departments.
* If **they're unrelated**, then promotions happen **independently** of department.

To test your suspicion, you use a **Chi-Square Test of Independence**.

---

## 1. Chi-Square Test of Independence

### Goal:

Check if **two categorical variables** are **associated** or **independent**.

### Hypotheses:

* **H₀ (Null)**: The two variables are independent (no relationship)
* **H₁ (Alt.)**: The two variables are dependent (there is a relationship)

---

### Example Problem

You survey 30 people on their **gender** and whether they **prefer tea or coffee**:

|           | Tea | Coffee | Total |
| --------- | --- | ------ | ----- |
| Male      | 10  | 5      | 15    |
| Female    | 5   | 10     | 15    |
| **Total** | 15  | 15     | 30    |

Is there a relationship between **gender** and **beverage preference**?

---

### Python Code Example

```python
import pandas as pd
from scipy.stats import chi2_contingency

# Creating the contingency table
data = [[10, 5], [5, 10]]
table = pd.DataFrame(data, columns=['Tea', 'Coffee'], index=['Male', 'Female'])

# Chi-square test of independence
chi2, p, dof, expected = chi2_contingency(table)

print("Chi-square Statistic:", chi2)
print("Degrees of Freedom:", dof)
print("Expected Frequencies:\n", expected)
print("P-value:", p)

if p < 0.05:
    print("Reject the null hypothesis: There is a relationship between gender and beverage preference.")
else:
    print("Fail to reject the null: No significant relationship between gender and beverage preference.")
```

---

### Explanation:

* `chi2`: the test statistic
* `p`: the p-value
* `dof`: degrees of freedom
* `expected`: what the counts would be if there was **no** relationship

---

## 2. Chi-Square Goodness-of-Fit Test

### Goal:

Check if a **single categorical variable** fits an **expected distribution**.

### Hypotheses:

* **H₀**: Observed frequencies match expected frequencies
* **H₁**: Observed frequencies differ from expected

---

### Real-World Analogy

You're rolling a die 60 times. You expect each number (1–6) to appear 10 times. But your results are:

* \[1: 8, 2: 9, 3: 12, 4: 11, 5: 13, 6: 7]

Are these differences just random, or is your die biased?

---

### Python Code Example

```python
from scipy.stats import chisquare

# Observed frequencies from the dice rolls
observed = [8, 9, 12, 11, 13, 7]

# Expected frequencies (uniform distribution for 6 sides)
expected = [10] * 6

# Chi-square goodness-of-fit test
chi2_stat, p_val = chisquare(f_obs=observed, f_exp=expected)

print("Chi-square Statistic:", chi2_stat)
print("P-value:", p_val)

if p_val < 0.05:
    print("Reject the null: The die is likely biased.")
else:
    print("Fail to reject the null: The die seems fair.")
```

---

## Key Assumptions

1. **Categories must be mutually exclusive** (no overlap)
2. **Expected frequency in each cell should be ≥ 5**
3. Observations should be **independent**

---

## Degrees of Freedom (df)

* For **independence**:
  `df = (rows - 1) * (columns - 1)`

* For **goodness of fit**:
  `df = (number of categories - 1)`

---

## When to Use Chi-Square vs Other Tests

| Scenario                             | Use            |
| ------------------------------------ | -------------- |
| Compare means between groups         | t-test / ANOVA |
| Test independence between categories | Chi-Square     |
| Test frequency match to expectation  | Chi-Square     |
| Paired categorical comparison        | McNemar's test |

---

## Limitations

* Only for **categorical data**
* Does **not show strength or direction** of association
* Assumes **large sample sizes**

---

## Visualizing Contingency Tables

```python
import seaborn as sns
import matplotlib.pyplot as plt

# Heatmap of observed values
sns.heatmap(table, annot=True, cmap="YlGnBu")
plt.title("Observed Frequencies")
plt.show()

# Heatmap of expected values
expected_df = pd.DataFrame(expected, columns=['Tea', 'Coffee'], index=['Male', 'Female'])
sns.heatmap(expected_df, annot=True, cmap="coolwarm")
plt.title("Expected Frequencies Under H₀")
plt.show()
```

---

## Summary

| Term                  | Meaning                                          |
| --------------------- | ------------------------------------------------ |
| **Observed**          | Actual counts from your data                     |
| **Expected**          | What you'd expect if H₀ is true                  |
| **Chi-square**        | A measure of how far observed is from expected   |
| **p-value**           | Probability of observing this data if H₀ is true |
| **Reject H₀**         | There's evidence of association/difference       |
| **Fail to Reject H₀** | No evidence of association/difference            |

