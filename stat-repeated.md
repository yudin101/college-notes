# STA154 Basic Statistics: Exam-Ready Answers

Built from the 2078, 2079, 2080, 2081, 2082 papers and the model question, with the syllabus topics that haven't been asked yet at the end.

**How to use this:** Basic Statistics is a numerical subject. The same question types come back every year, so the plan is simple: learn the formula, work each past numerical by hand, then redo it without looking. Reading is not enough. A calculator is essential; bring a scientific calculator if your exam allows it (check the rules).

**Conventions used in this file**

- Descriptive problems (dispersion, moments) use the population formulas (divide by `n`). Estimation problems (confidence intervals) use the sample standard deviation `s` (divide by `n - 1`). Where it matters, I say so. The conclusion rarely changes.
- Normal table values are read to 2 decimal places of z. A mini z-table is in Section 4. **Check whether a normal table will be provided in your exam; if not, memorize that mini-table.**

## What repeats (2078-2082 + model)

| Topic                                                                       | Where it appeared                                                   |
| --------------------------------------------------------------------------- | ------------------------------------------------------------------- |
| **Dispersion, CV, consistency comparison**                                  | 2078 Q1, 2079 Q1, 2080 Q1, 2081 Q1, 2082 Q2, model Q1 (every paper) |
| **Regression line (fit, predict, interpret)**                               | 2078 Q2, 2079 Q2, 2080 Q2, 2081 Q3, 2082 Q3, model Q2 (every paper) |
| **Normal distribution**                                                     | 2078 Q3, 2079 Q3, 2080 Q3, 2081 Q8, 2082 Q1, model Q7 (every paper) |
| **Correlation (Pearson / Spearman)**                                        | 2078 Q6, 2079 Q6, 2080 Q6, 2081 Q3, 2082 Q3, model Q5               |
| **Probability (addition, conditional, Bayes)**                              | 2078 Q9, 2079 Q9, 2080 Q9, 2081 Q7, 2082 Q6-Q7, model Q9            |
| **Random variable: expectation and variance**                               | 2078 Q7, 2079 Q7, 2080 Q7, 2081 Q10, 2082 Q8, model Q6              |
| **Moments, skewness, kurtosis**                                             | 2078 Q10, 2079 Q10, 2080 Q10, 2081 Q2, 2082 Q11, model Q10          |
| **Binomial distribution**                                                   | 2078 Q8, 2079 Q8, 2080 Q8, 2082 Q10                                 |
| **Poisson distribution**                                                    | 2081 Q5, model Q8                                                   |
| **Confidence interval (mean / proportion)**                                 | 2079 Q11, 2080 Q11, 2081 Q6, 2082 Q9, model Q11                     |
| **Sampling (types, errors, parameter vs statistic, sampling distribution)** | 2078 Q11-12, 2079 Q12, 2081 Q12, 2082 Q12, model Q3                 |
| **Graphs** (pie, bar/Pareto, histogram, box plot)                           | 2078 Q5, 2079 Q5, 2080 Q5, 2081 Q4 & Q9, 2082 Q4, model Q12         |
| **Scales of measurement**                                                   | 2078 Q4, 2082 Q5, model Q4                                          |
| **Role of statistics in IT / data sources**                                 | 2079 Q4, 2080 Q4, 2081 Q11, 2082 Q12                                |

## Which long questions to attempt

Each paper has three long questions and you do two. Almost every year they come from: **(1) dispersion/consistency**, **(2) regression (with correlation)**, **(3) normal distribution** (or moments, as in 2081). Each is a fixed template, so these two or three are your safest long questions. Be able to do all of them; you then always have two to choose from.

## Problems in the papers (state your assumption in the exam)

- **2079 Q2 (pumpkins):** the weight row is garbled in the scan and has the wrong number of values, so I haven't solved it. Use the regression template in Section 2.
- **2082 Q3:** a handwritten "0.928" is next to part (a) on the scan. Working it out gives **r = 0.996**. Trust the calculation.
- **2079 Q7:** "P(K ≥ 0)" is almost certainly a misprint for **P(X ≥ 0)**. I answer that.
- **2081 Q7:** the paper doesn't give the chance that a failed server reports an error. I assume it always does (probability 1).
- **Model Q9:** the wording is ambiguous; I give both readings.
- **2078 Q8 / 2079 Q8:** the same binomial question appears in both.

## Contents

1. [Dispersion and Consistency](#1-dispersion-and-consistency)
2. [Regression](#2-regression)
3. [Correlation](#3-correlation)
4. [Normal Distribution](#4-normal-distribution)
5. [Probability and Bayes' Theorem](#5-probability-and-bayes-theorem)
6. [Random Variables and Expectation](#6-random-variables-and-expectation)
7. [Binomial and Poisson Distributions](#7-binomial-and-poisson-distributions)
8. [Moments, Skewness and Kurtosis](#8-moments-skewness-and-kurtosis)
9. [Confidence Intervals](#9-confidence-intervals)
10. [Sampling and Sampling Distribution](#10-sampling-and-sampling-distribution)
11. [Central Tendency and Exploratory Data Analysis](#11-central-tendency-and-exploratory-data-analysis)
12. [Diagrams and Graphs](#12-diagrams-and-graphs)
13. [Introduction: Scales, Data, Role of Statistics](#13-introduction-scales-data-role-of-statistics)
14. [Formula Sheet](#14-formula-sheet)

---

## 1. Dispersion and Consistency

### Definition and need

**Dispersion** is the extent to which observations are scattered around a central value. It is needed because an average alone hides the spread: two datasets can have the same mean but very different spread. Dispersion shows how reliable the average is, lets us compare variability, and helps control variation.

### Methods of measuring dispersion (2078 Q1)

| Absolute measure        | Formula                | Relative measure                  | Formula                 |
| ----------------------- | ---------------------- | --------------------------------- | ----------------------- |
| Range                   | `L - S`                | Coefficient of range              | `(L - S) / (L + S)`     |
| Quartile deviation (QD) | `(Q3 - Q1) / 2`        | Coefficient of QD                 | `(Q3 - Q1) / (Q3 + Q1)` |
| Mean deviation (MD)     | `Σ                     | x - x̄                             | / n`                    | Coefficient of MD | `MD / average` |
| Standard deviation (SD) | `σ = √(Σ(x - x̄)² / n)` | **Coefficient of variation (CV)** | `(σ / x̄) × 100%`        |
| Variance                | `σ²`                   |                                   |                         |

Shortcut: `σ² = Σx²/n - x̄²`.

### Absolute vs relative measure (2079 Q1)

| Point    | Absolute                       | Relative                                                                    |
| -------- | ------------------------------ | --------------------------------------------------------------------------- |
| Units    | Has the units of the data      | Unit-free (pure number or %)                                                |
| Use      | Describe spread of one dataset | **Compare** variability of datasets with different units or different means |
| Examples | Range, QD, MD, SD              | Coefficient of range, of QD, of MD, CV                                      |

### Consistency questions: the template

1. Compute the mean of each series.
2. Compute the SD of each series.
3. Compute `CV = (σ / x̄) × 100`.
4. **The series with the smaller CV is more consistent (more homogeneous, more uniform).**
5. If asked "who is better", compare the means (higher mean = better performance).

### 2078 Q1: students A and B in 10 tests

A: 44 80 76 48 52 72 68 56 60 54. B: 48 75 54 60 63 69 72 51 57 66.

|                 | Student A                   | Student B                    |
| --------------- | --------------------------- | ---------------------------- |
| Σx              | 610                         | 615                          |
| Mean            | 61                          | 61.5                         |
| Σx²             | 38,580                      | 38,565                       |
| σ² = Σx²/n - x̄² | 3,858 - 3,721 = 137         | 3,856.5 - 3,782.25 = 74.25   |
| σ               | 11.70                       | 8.62                         |
| CV              | 11.70/61 × 100 = **19.19%** | 8.62/61.5 × 100 = **14.01%** |

- **(i) Who is better?** B has the higher average (61.5 > 61), so B is slightly better.
- **(ii) Prize for consistency:** B, because CV(B) = 14.01% < CV(A) = 19.19%.

### 2079 Q1: Tube I vs Tube II (which is more homogeneous?)

Tube I: 0.57 0.34 0.43 0.32 0.48 0.40 0.40. Tube II: 0.53 0.47 0.47 0.51 0.63 0.61 0.48. (n = 7)

|      | Tube I                   | Tube II                     |
| ---- | ------------------------ | --------------------------- |
| Σx   | 2.94                     | 3.70                        |
| Mean | 0.42                     | 0.5286                      |
| Σx²  | 1.2782                   | 1.9822                      |
| σ²   | 0.1826 - 0.1764 = 0.0062 | 0.28317 - 0.27939 = 0.00378 |
| σ    | 0.0787                   | 0.0615                      |
| CV   | **18.75%**               | **11.64%**                  |

**Tube II is more homogeneous** (smaller CV).

### 2080 Q1: Basic Statistics vs Computer Science marks (which subject is more consistent?)

BS: 53 55 52 32 30 60 47 46 35 58. CS: 57 45 24 31 25 84 43 80 32 72. (n = 10)

|      | Basic Statistics            | Computer Science            |
| ---- | --------------------------- | --------------------------- |
| Σx   | 468                         | 493                         |
| Mean | 46.8                        | 49.3                        |
| Σx²  | 22,976                      | 28,949                      |
| σ²   | 2,297.6 - 2,190.24 = 107.36 | 2,894.9 - 2,430.49 = 464.41 |
| σ    | 10.36                       | 21.55                       |
| CV   | **22.14%**                  | **43.71%**                  |

**Basic Statistics marks are more consistent** (smaller CV).

_Also write:_ descriptive statistics only summarize and describe the data in hand (mean, tables, graphs); **inferential statistics** uses a sample to draw conclusions about a population (estimation, hypothesis testing), with a measure of uncertainty.

### 2081 Q1 and 2082 Q2: Cluster/Build System A vs B

A: 88 92 94 85 90 95 89 87 91 86. B: 130 135 132 140 128 133 137 131 129 138. (n = 10)

|      | A                          | B                            |
| ---- | -------------------------- | ---------------------------- |
| Σx   | 897                        | 1,333                        |
| Mean | 89.7                       | 133.3                        |
| Σx²  | 80,561                     | 177,837                      |
| σ²   | 8,056.1 - 8,046.09 = 10.01 | 17,783.7 - 17,768.89 = 14.81 |
| σ    | 3.16                       | 3.85                         |
| CV   | **3.53%**                  | **2.89%**                    |

**B is more consistent** (CV 2.89% < 3.53%). Note the trap: A has the smaller SD (3.16 vs 3.85), but the means are very different (90 vs 133), so you must compare the CV, not the SD.

---

## 2. Regression

### Definition and need

**Regression analysis** estimates the average relationship between a dependent variable Y and an independent variable X so that Y can be predicted from X. The **line of regression of Y on X** is `Y = a + bX`, fitted by the **method of least squares** (the line that minimizes the sum of squared vertical deviations).

### Formulas (Y on X)

```
b = (nΣXY - ΣX·ΣY) / (nΣX² - (ΣX)²)  =  Sxy / Sxx
a = Ȳ - b·X̄
```

where `Sxy = ΣXY - ΣX·ΣY/n` and `Sxx = ΣX² - (ΣX)²/n`.

### Interpretation

- **b (regression coefficient):** the average change in Y for a one-unit increase in X. Its sign gives the direction.
- **a (intercept):** the value of Y when X = 0. It often has no real meaning if X = 0 is outside the data.
- **R² (coefficient of determination) = r²:** the proportion of the variation in Y explained by X.
- **Residual plot:** plot residuals (`y - ŷ`) against fitted values. Random scatter around zero means a linear model is suitable; a curve or pattern means a non-linear relationship; a funnel shape means unequal variance.
- **Extrapolation warning:** predicting for X values outside the range of the data (e.g., 80 cm when the data run 37-55 cm) is unreliable.

### 2078 Q2: performance on experience

X (experience): 16 12 18 4 3 10 5 12. Y (performance): 87 88 89 68 78 80 75 83. n = 8.

ΣX = 80, ΣY = 648, X̄ = 10, Ȳ = 81, ΣXY = 6,727, ΣX² = 1,018.

```
b = (6727 - 8·10·81) / (1018 - 8·10²) = (6727 - 6480) / (1018 - 800) = 247/218 = 1.133
a = 81 - 1.133 × 10 = 69.67
```

**(a) Regression line: Y = 69.67 + 1.133X**

**(b) At X = 8:** Y = 69.67 + 1.133 × 8 = **78.73**, about 79 good parts per 100 pieces.
**Interpretation:** each additional year of experience raises performance by about 1.13 good parts per 100 pieces, on average.

### 2080 Q2: blood pressure on age

X (age): 56 42 72 36 63 47. Y (BP): 147 125 160 118 149 128. n = 6.

ΣX = 316, ΣY = 827, ΣXY = 44,653, ΣX² = 17,558. X̄ = 52.67, Ȳ = 137.83.

```
b = (6·44653 - 316·827) / (6·17558 - 316²) = (267918 - 261332) / (105348 - 99856)
  = 6586 / 5492 = 1.199
a = 137.83 - 1.199 × 52.67 = 74.68
```

- **(i) Line: Y = 74.68 + 1.199X**
- **(ii) At age 50:** Y = 74.68 + 1.199 × 50 = **134.64** (about 135 mmHg).
- **(iii) Interpretation:** blood pressure increases by about 1.2 units for each additional year of age.

### 2081 Q3: bugs on coding hours

X (hours): 20 25 30 35 40 45 50 55 60 65. Y (bugs): 5 7 8 12 15 13 17 18 20 25. n = 10.

ΣX = 425, ΣY = 140, ΣXY = 6,785, ΣX² = 20,125, ΣY² = 2,314. X̄ = 42.5, Ȳ = 14.
`Sxy = 6785 - 10·42.5·14 = 835`, `Sxx = 20125 - 10·42.5² = 2,062.5`, `Syy = 2314 - 10·14² = 354`.

- **(a) r = 835 / √(2062.5 × 354) = 835 / 854.47 = 0.977** (very strong positive linear relationship).
- **(b)** `b = 835 / 2062.5 = 0.4048`, `a = 14 - 0.4048 × 42.5 = -3.21`. **Bugs = -3.21 + 0.4048 × Hours.**
- **(c) At 48 hours:** -3.21 + 0.4048 × 48 = **16.2**, about 16 bugs.
- R² = 0.955: about 95.5% of the variation in bugs is explained by coding hours.

### 2082 Q3: issues resolved on debugging hours

X (hours): 15 20 25 30 35 40 45 50 55 60. Y (issues): 3 6 8 11 12 14 16 19 21 22. n = 10.

ΣX = 375, ΣY = 132, ΣXY = 5,820, ΣX² = 16,125, ΣY² = 2,112. X̄ = 37.5, Ȳ = 13.2.
`Sxy = 5820 - 10·37.5·13.2 = 870`, `Sxx = 16125 - 10·37.5² = 2,062.5`, `Syy = 2112 - 10·13.2² = 369.6`.

- **(a) r = 870 / √(2062.5 × 369.6) = 870 / 873.1 = 0.996** (almost perfect positive).
- **(b)** `b = 870 / 2062.5 = 0.4218`, `a = 13.2 - 0.4218 × 37.5 = -2.62`. **Issues = -2.62 + 0.4218 × Hours.**
- **(c) At 38 hours:** -2.62 + 0.4218 × 38 = **13.41**, about 13 issues.

### Model Q2: sales on advertisement

X (ad expenditure, lakh Rs): 40 50 38 60 65 50 35. Y (sales, crore Rs): 38 60 55 70 60 48 30. n = 7.

ΣX = 338, ΣY = 361, ΣXY = 18,160, ΣX² = 17,094, ΣY² = 19,773.

```
b = (7·18160 - 338·361) / (7·17094 - 338²) = (127120 - 122018) / (119658 - 114244)
  = 5102 / 5414 = 0.9424
a = 361/7 - 0.9424 × 338/7 = 51.571 - 45.503 = 6.07
```

- **(a) Y = 6.07 + 0.942X.** Each additional lakh rupees of advertising is associated with about 0.94 crore rupees more sales, on average. `r = 5102 / √(5414 × 8090) = 0.771` (strong positive), and R² = 0.594: about 59% of the variation in sales is explained by advertising.
- **(b) At X = 45:** Y = 6.07 + 0.942 × 45 = **48.47 crore rupees**.

### 2079 Q2: pumpkin weight on circumference

The data in the paper are garbled, so use this template: compute ΣX, ΣY, ΣXY, ΣX² and apply `b = (nΣXY - ΣXΣY)/(nΣX² - (ΣX)²)`, `a = Ȳ - bX̄`; then substitute X = 40.

**Can we predict the weight at 80 cm?** No, or at least not reliably. The sample circumferences range from about 37 to 55 cm, so 80 cm is far outside the observed range (**extrapolation**). The linear relationship may not continue (weight usually grows faster than linearly with size), so the prediction would be unreliable.

---

## 3. Correlation

### Definition

**Correlation** measures the strength and direction of the linear relationship between two variables. The **Karl Pearson coefficient of correlation r** is

```
r = Sxy / √(Sxx · Syy)
  = (nΣXY - ΣXΣY) / √[(nΣX² - (ΣX)²)(nΣY² - (ΣY)²)]
```

### Interpretation of r

| r                  | Meaning                                         |
| ------------------ | ----------------------------------------------- |
| +1 / -1            | Perfect positive / negative linear relationship |
| 0.7 to 1 (in size) | Strong                                          |
| 0.4 to 0.7         | Moderate                                        |
| below 0.4          | Weak                                            |
| 0                  | No linear relationship                          |

Positive r: both variables move in the same direction. Negative r: they move in opposite directions.

### Properties of the correlation coefficient (2080 Q6)

1. `-1 <= r <= +1`.
2. It is **independent of change of origin and scale** (for positive scale changes).
3. It is **symmetric**: `r_xy = r_yx`.
4. It is a **pure number**, with no units.
5. `r = ±√(b_xy · b_yx)`; it is the geometric mean of the two regression coefficients and has their sign.
6. Independent variables have r = 0, but r = 0 does not imply independence (the relationship could be non-linear).
7. It measures only **linear** relationship and does **not** imply causation.

### Assumptions of Pearson's r

Both variables are quantitative (interval/ratio); the relationship is linear; the pairs are approximately bivariate normal; there are no extreme outliers; the spread of one variable is similar across the values of the other.

### 2078 Q6: husbands' and wives' ages

X: 23 27 28 28 29 30 31 33 35 36. Y: 18 20 27 21 29 27 27 29 28 29. n = 10.

ΣX = 300, ΣY = 255, ΣXY = 7,767, ΣX² = 9,138, ΣY² = 6,659.
`Sxy = 7767 - 10·30·25.5 = 117`, `Sxx = 9138 - 9000 = 138`, `Syy = 6659 - 6502.5 = 156.5`.

`r = 117 / √(138 × 156.5) = 117 / 146.96 = 0.796`

**Interpretation:** strong positive correlation. Older husbands tend to have older wives.

### 2080 Q6: aptitude score and productivity index

X: 9 18 18 20 20 23. Y: 12 33 23 42 29 30. n = 6.

ΣX = 108, ΣY = 169, ΣXY = 3,226, ΣX² = 2,058, ΣY² = 5,267. X̄ = 18, Ȳ = 28.17.
`Sxy = 3226 - 108·169/6 = 184`, `Sxx = 2058 - 108²/6 = 114`, `Syy = 5267 - 169²/6 = 506.83`.

`r = 184 / √(114 × 506.83) = 184 / 240.37 = 0.766`

**Comment:** strong positive correlation; workers with higher aptitude scores tend to have higher productivity.

**Coefficient of variation:**

- X: `σx = √(114/6) = √19 = 4.36`, `CV = 4.36/18 × 100 = 24.2%`
- Y: `σy = √(506.83/6) = 9.19`, `CV = 9.19/28.17 × 100 = 32.6%`

### Spearman's rank correlation (2079 Q6)

Used when data are ranks or ordinal.

```
rs = 1 - 6Σd² / (n(n² - 1))
```

d = difference between the ranks of each pair. If ranks are tied, add `m(m² - 1)/12` to Σd² for each group of m tied values.

**2079 Q6:** DELL ranks: 5 2 9 8 1 10 3 4 6 7. HP ranks: 10 5 1 3 8 6 2 7 9 4. n = 10.

| d = R1 - R2 | -5  | -3  | 8   | 5   | -7  | 4   | 1   | -3  | -3  | 3   |
| ----------- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| d²          | 25  | 9   | 64  | 25  | 49  | 16  | 1   | 9   | 9   | 9   |

Σd² = 216.
`rs = 1 - 6 × 216 / (10 × 99) = 1 - 1296/990 = 1 - 1.309 = -0.309`

**Interpretation:** a weak negative rank correlation. Students' preferences for DELL and HP are slightly opposite, but the relationship is weak.

### Model Q5: correlation from two regression lines

Lines: `3X + 2Y = 26` and `6X + 3Y = 31`.

Assume the first is Y on X: `Y = 13 - 1.5X`, so `b_yx = -1.5`.
Assume the second is X on Y: `X = (31 - 3Y)/6`, so `b_xy = -0.5`.
`r² = b_yx × b_xy = 0.75`, so `r = -√0.75 = -0.866`. (Valid since r² <= 1.)

_Check the other assignment:_ `b_xy = -2/3`, `b_yx = -2`, product = 4/3 > 1, impossible. So the first assignment is right.

**Interpretation:** r = -0.866, a strong negative correlation: as X increases, Y tends to decrease.

---

## 4. Normal Distribution

### Definition

A continuous random variable X has a **normal distribution** with mean μ and standard deviation σ if its pdf is
`f(x) = (1 / (σ√(2π))) · e^(-(x-μ)²/(2σ²))`, `-∞ < x < ∞`.

**Properties:** bell-shaped and symmetric about μ; mean = median = mode = μ; total area = 1; the curve is asymptotic to the x-axis; about **68.3%** of values lie within μ ± σ, **95.4%** within μ ± 2σ, **99.7%** within μ ± 3σ.

### Standard normal distribution (2078 Q3)

A normal distribution with **μ = 0 and σ = 1**. Any normal X is converted using `Z = (X - μ) / σ`.

### When is it used? (2080 Q3)

When the variable is continuous and its distribution is symmetric and bell-shaped, with values clustering around the mean (e.g., heights, marks, measurement errors, response times, salaries). It also approximates binomial and Poisson distributions for large samples, and it underlies the central limit theorem and confidence intervals.

### Mini z-table: P(Z <= z)

| z    | Φ(z)   | z     | Φ(z)   |
| ---- | ------ | ----- | ------ |
| 0.25 | 0.5987 | 1.33  | 0.9082 |
| 0.33 | 0.6293 | 1.645 | 0.9500 |
| 0.50 | 0.6915 | 1.96  | 0.9750 |
| 0.67 | 0.7486 | 2.00  | 0.9772 |
| 0.75 | 0.7734 | 2.33  | 0.9901 |
| 0.84 | 0.7995 | 2.50  | 0.9938 |
| 1.00 | 0.8413 | 2.576 | 0.9950 |
| 1.28 | 0.8997 |       |        |

For negative z: `Φ(-z) = 1 - Φ(z)` (e.g., Φ(-1) = 0.1587).

### 2078 Q3: battery life, μ = 50, σ = 15

- **(i) P(50 < X < 70):** z from 0 to (70-50)/15 = 1.33. `Φ(1.33) - 0.5 = 0.9082 - 0.5 =` **0.4082**
- **(ii) P(X > 60):** z = 10/15 = 0.67. `1 - 0.7486 =` **0.2514**
- **(iii) P(X < 45):** z = -5/15 = -0.33. `Φ(-0.33) = 1 - 0.6293 =` **0.3707**

### 2080 Q3: salaries, μ = $50,000, σ = $20,000

- **(a) P(X < 40,000):** z = -0.5 → **0.3085**
- **(b) P(45,000 < X < 65,000):** z = -0.25 and 0.75 → `0.7734 - 0.4013 =` **0.3721**
- **(c) P(X > 70,000):** z = 1 → `1 - 0.8413 =` **0.1587**

### 2081 Q8: resolution time, μ = 30, σ = 5

- **(a) P(X < 25):** z = -1 → 0.1587 → **15.87%**
- **(b) P(25 < X < 35):** z from -1 to +1 → `0.8413 - 0.1587 = 0.6826` → **68.26%**

### Model Q7: grades, μ = 73, σ = 8

- **(a) P(X < 93):** z = 2.5 → **0.9938**
- **(b) P(65 < X < 89):** z = -1 and 2 → `0.9772 - 0.1587 =` **0.8185**

### 2079 Q3: find μ and σ from percentiles

10% scored below 20 and 95% scored below 75.
From the table: z for 10% is **-1.28**; z for 95% is **1.645**.

```
(20 - μ)/σ = -1.28      →  μ - 1.28σ = 20
(75 - μ)/σ =  1.645     →  μ + 1.645σ = 75
Subtract:  2.925σ = 55  →  σ = 18.80
μ = 20 + 1.28 × 18.80 = 44.07
```

**Mean ≈ 44.07, standard deviation ≈ 18.80.**

### 2082 Q1: incomes, N = 5,000, μ = Rs 2,000, σ = Rs 200

- **(i) Middle 60%:** 30% on each side of the mean, so the central area 0.60 leaves 0.20 in each tail; z = ±0.84. Range = 2000 ± 0.84 × 200 = **Rs 1,832 to Rs 2,168** (about 3,000 employees).
- **(ii) Lowest income of the richest 10%:** upper 10% means z = 1.28. X = 2000 + 1.28 × 200 = **Rs 2,256** (about 500 employees earn at least this).
- **(iii) Highest income of the poorest 10%:** z = -1.28. X = 2000 - 256 = **Rs 1,744**.

---

## 5. Probability and Bayes' Theorem

### Concepts

- **Experiment:** a process with uncertain outcome. **Sample space S:** all possible outcomes. **Event:** a subset of S.
- **Mutually exclusive events:** cannot occur together. **Exhaustive events:** together cover S. **Independent events:** the occurrence of one does not change the probability of the other.

### Definitions of probability

- **Classical (mathematical):** `P(A) = m / n` (favourable outcomes / total equally likely outcomes).
- **Statistical (relative frequency):** the limit of the relative frequency of A as the number of trials grows.
- **Subjective:** a personal degree of belief based on judgement or experience.

### Laws of probability

- **Complement:** `P(A') = 1 - P(A)`.
- **Addition law:** `P(A ∪ B) = P(A) + P(B) - P(A ∩ B)`. For mutually exclusive events: `P(A ∪ B) = P(A) + P(B)`.
- **Multiplication law:** `P(A ∩ B) = P(A) · P(B given A)`. For independent events: `P(A ∩ B) = P(A) · P(B)`.
- **Conditional probability:** `P(A given B) = P(A ∩ B) / P(B)`, for `P(B) > 0`.
- **Total probability:** if `A1, ..., An` are mutually exclusive and exhaustive, `P(B) = Σ P(Ai) · P(B given Ai)`.
- **Bayes' theorem:** `P(Ai given B) = P(Ai) · P(B given Ai) / Σ P(Aj) · P(B given Aj)`.
  `P(Ai)` is the **prior** probability; `P(Ai given B)` is the **posterior** probability (updated after seeing evidence B).

### 2078 Q9: computers with MB / HD problems

`P(MB) = 0.40`, `P(HD) = 0.30`, `P(MB ∩ HD) = 0.15`.
`P(MB ∪ HD) = 0.40 + 0.30 - 0.15 = 0.55`.
**P(both functioning) = 1 - 0.55 = 0.45.**

### 2079 Q9: virus through e-mail / internet

`P(E) = 0.30`, `P(I) = 0.40`, `P(E ∩ I) = 0.15`.
`P(E ∪ I) = 0.30 + 0.40 - 0.15 = 0.55`.
**P(virus does not enter) = 1 - 0.55 = 0.45.**

### 2080 Q9: etching / crack defects

`P(E) = 0.12`, `P(C) = 0.29`, `P(E ∩ C) = 0.07`.
**P(either defect) = 0.12 + 0.29 - 0.07 = 0.34.**

### 2082 Q6: equipment works only if A, B, C all work

Failure probabilities: A 0.15, B 0.05, C 0.10. Assuming the components fail independently:
`P(not fail) = (1 - 0.15)(1 - 0.05)(1 - 0.10) = 0.85 × 0.95 × 0.90 =` **0.72675**.

### 2082 Q7: Vice-Chancellor appointment (total probability)

Chances of selection are in the ratio 4 : 2 : 3, so `P(A) = 4/9`, `P(B) = 2/9`, `P(C) = 3/9`.
Let D = democratization is introduced: `P(D given A) = 0.3`, `P(D given B) = 0.5`, `P(D given C) = 0.8`.

```
P(D) = (4/9)(0.3) + (2/9)(0.5) + (3/9)(0.8) = (1.2 + 1.0 + 2.4) / 9 = 4.6 / 9 = 0.511
```

### 2081 Q7: server failure (Bayes)

Let F = server has failed, E = server reports an error.
`P(F) = 0.05`, `P(F') = 0.95`. A working server gives a false error with probability `P(E given F') = 0.05`. Assume a failed server always reports an error: `P(E given F) = 1`.

```
P(F given E) = P(F)P(E given F) / [P(F)P(E given F) + P(F')P(E given F')]
             = (0.05)(1) / [(0.05)(1) + (0.95)(0.05)]
             = 0.05 / 0.0975 = 0.513
```

**About a 51% chance that the server has actually failed.**

### Model Q9: junk e-mail from Harish (Bayes)

Rajesh receives 50 messages with 1% junk; Harish receives 90 messages with 2% junk.

**Reading 1 (a random message is chosen, so weight by volume):**
`P(R) = 50/140`, `P(H) = 90/140`, `P(J given R) = 0.01`, `P(J given H) = 0.02`.

```
P(H given J) = (90/140)(0.02) / [(50/140)(0.01) + (90/140)(0.02)] = 1.8 / (0.5 + 1.8) = 0.783
```

**Reading 2 (a person is chosen with equal probability):**
`P(H given J) = (0.5)(0.02) / [(0.5)(0.01) + (0.5)(0.02)] = 0.02 / 0.03 = 0.667`

Because the question gives the message counts, Reading 1 (0.783) is likely the intended answer. State the assumption you use.

---

## 6. Random Variables and Expectation

### Definition

A **random variable** is a function that assigns a real number to each outcome of an experiment. A **discrete** random variable takes countable values (number of crashes); a **continuous** random variable takes any value in an interval (time, weight).

**Probability distribution of a discrete random variable:** the list of values x with their probabilities `P(x)`, where `P(x) >= 0` and `ΣP(x) = 1`.

### Formulas

```
E(X)   = Σ x·P(x)                 (continuous: ∫ x·f(x) dx)
E(X²)  = Σ x²·P(x)
Var(X) = E(X²) - [E(X)]²
SD     = √Var(X)
E(aX + b)   = a·E(X) + b
Var(aX + b) = a²·Var(X)
```

### 2078 Q7: continuous density f(x) = k(1 - x)², 0 < x < 1

- **(i) k:** `∫₀¹ k(1 - x)² dx = k/3 = 1`, so **k = 3**.
- **(ii) P(0 < X < 0.5):** `∫₀^0.5 3(1 - x)² dx = [-(1 - x)³]₀^0.5 = 1 - 0.5³ =` **0.875**.
- **(iii) E(X):** `∫₀¹ x · 3(1 - x)² dx = 3∫₀¹ (x - 2x² + x³) dx = 3(1/2 - 2/3 + 1/4) = 3(1/12) =` **0.25**.
- **(iv) E(2X + 4)** = 2(0.25) + 4 = **4.5**.

### 2079 Q7: X = -2, -1, 0, 1, 2; P = 0.2, K, 0.4, 2K, K

- **(i)** `0.2 + K + 0.4 + 2K + K = 1`, so `4K = 0.4`, **K = 0.1**. The probabilities are 0.2, 0.1, 0.4, 0.2, 0.1.
- **(ii) P(X ≥ 0)** = 0.4 + 0.2 + 0.1 = **0.7**. (If it literally means K ≥ 0, that is trivially true since K = 0.1.)
- **(iii) E(X)** = (-2)(0.2) + (-1)(0.1) + 0 + (1)(0.2) + (2)(0.1) = -0.4 - 0.1 + 0.2 + 0.2 = **-0.1**.
- **(iv) E(4X + 5)** = 4(-0.1) + 5 = **4.6**.

### 2080 Q7: X = 0 to 5; P = 0.1, C, 0.2, 2C, 0.3, C

- **(i)** `0.1 + C + 0.2 + 2C + 0.3 + C = 1`, so `4C = 0.4`, **C = 0.1**.
- **(ii)** `P(X < 3) = 0.1 + 0.1 + 0.2 =` **0.4**. `P(X ≥ 1) = 1 - 0.1 =` **0.9**.
- **(iii)** Probabilities: 0.1, 0.1, 0.2, 0.2, 0.3, 0.1.
  `E(X) = 0 + 0.1 + 0.4 + 0.6 + 1.2 + 0.5 =` **2.8**.
  `E(X²) = 0 + 0.1 + 0.8 + 1.8 + 4.8 + 2.5 = 10.0`.
  **Var(X) = 10 - 2.8² = 10 - 7.84 = 2.16.**

### 2081 Q10: queries per hour (0, 1, 2, 3, 4 with 0.10, 0.20, 0.30, 0.25, 0.15)

`E(X) = 0 + 0.20 + 0.60 + 0.75 + 0.60 =` **2.15 queries per hour**.
`E(X²) = 0 + 0.20 + 1.20 + 2.25 + 2.40 = 6.05`.
**Var(X) = 6.05 - 2.15² = 6.05 - 4.6225 = 1.4275.**

### 2082 Q8: bug reports closed (0, 1, 2, 3, 4 with 0.10, 0.18, 0.32, 0.30, 0.10)

`E(Y) = 0 + 0.18 + 0.64 + 0.90 + 0.40 =` **2.12 per hour**.
`E(Y²) = 0 + 0.18 + 1.28 + 2.70 + 1.60 = 5.76`.
**Var(Y) = 5.76 - 2.12² = 5.76 - 4.4944 = 1.2656.**

### Model Q6: computer crashes (0 to 5 with 0.10, 0.20, 0.45, 0.15, 0.05, 0.05)

`E(X) = 0 + 0.2 + 0.9 + 0.45 + 0.2 + 0.25 =` **2.0**.
`E(X²) = 0 + 0.2 + 1.8 + 1.35 + 0.8 + 1.25 = 5.4`.
`Var = 5.4 - 4 = 1.4`, `SD = √1.4 =` **1.18**.
**Interpretation:** on average 2 crashes occur per month, and the number typically varies by about 1.2 crashes around that average.

---

## 7. Binomial and Poisson Distributions

### Binomial distribution

**Definition:** the distribution of the number of successes X in `n` independent trials, each with two outcomes (success/failure) and the same success probability p.

**Conditions:** fixed number of trials n; each trial has two outcomes; the trials are independent; p is constant.

```
P(X = x) = C(n, x) · p^x · q^(n-x),   x = 0, 1, ..., n,   q = 1 - p
Mean = np     Variance = npq
```

### 2078 Q8 / 2079 Q8: n = 15, p = 0.7, q = 0.3

- **At least 12:** `P(X>=12) = P(12) + P(13) + P(14) + P(15)`
  `P(12) = C(15,12)(0.7)^12(0.3)^3 = 455 × 0.013841 × 0.027 = 0.1700`
  `P(13) = 105 × (0.7)^13 × (0.3)^2 = 0.0916`
  `P(14) = 15 × (0.7)^14 × 0.3 = 0.0305`
  `P(15) = (0.7)^15 = 0.0047`
  **P(X >= 12) = 0.2969**
- **At most 2 (2079):** `P(0) + P(1) + P(2) ≈ 0.0000000143 + 0.0000005 + 0.0000082 ≈` **0.0000087** (essentially 0).
- **Exactly 10:** `P(10) = C(15,10)(0.7)^10(0.3)^5 = 3003 × 0.028248 × 0.00243 =` **0.2061**.

### 2082 Q10: at least 80% of 5 viewers watch (p = 0.8)

"At least 80% of 5" means at least 4 of 5.
`P(X=4) = 5(0.8)^4(0.2) = 0.4096`; `P(X=5) = (0.8)^5 = 0.32768`.
**P(X >= 4) = 0.4096 + 0.3277 = 0.7373.**

### 2080 Q8: fitting a binomial distribution

Data: x = 0, 1, 2, 3, 4 with f = 28, 62, 46, 10, 4. Here `n = 4`, `N = Σf = 150`.

**Steps:**

1. Mean = `Σfx / N = (0 + 62 + 92 + 30 + 16)/150 = 200/150 = 1.333`.
2. `np = 1.333`, so `p = 1.333/4 = 1/3`, `q = 2/3`.
3. Expected frequency `= N × C(4,x) × p^x × q^(4-x)`.

| x     | P(x)                           | Expected frequency (150 × P) | Rounded | Observed |
| ----- | ------------------------------ | ---------------------------- | ------- | -------- |
| 0     | (2/3)⁴ = 16/81 = 0.1975        | 29.63                        | 30      | 28       |
| 1     | 4(1/3)(2/3)³ = 32/81 = 0.3951  | 59.26                        | 59      | 62       |
| 2     | 6(1/3)²(2/3)² = 24/81 = 0.2963 | 44.44                        | 44      | 46       |
| 3     | 4(1/3)³(2/3) = 8/81 = 0.0988   | 14.81                        | 15      | 10       |
| 4     | (1/3)⁴ = 1/81 = 0.0123         | 1.85                         | 2       | 4        |
| Total | 1                              | 150                          | 150     | 150      |

### Poisson distribution

**Definition:** the distribution of the number of times a rare event occurs in a fixed interval of time or space, when events occur independently at a constant average rate λ.

```
P(X = x) = e^(-λ) · λ^x / x!,   x = 0, 1, 2, ...
Mean = Variance = λ
```

**Characteristics:** a discrete distribution; mean equals variance; used for rare events (server requests per minute, defects per metre, arrivals per hour). It is the limit of the binomial when n is large and p is small.

### 2081 Q5: server requests, λ = 5 per minute

- **(a) P(X = 3)** = `e^(-5) × 5³ / 3! = 0.006738 × 125/6 =` **0.1404**.
- **(b) P(X > 2)** = `1 - [P(0) + P(1) + P(2)]`
  `= 1 - e^(-5)(1 + 5 + 12.5) = 1 - 0.006738 × 18.5 = 1 - 0.1247 =` **0.8753**.

### Model Q8: vaccine refusal, λ = 0.45 per 10,000 people

`e^(-0.45) = 0.6376`.

- **(a) No one denies:** `P(0) =` **0.6376**.
- **(b) At least two:** `1 - P(0) - P(1) = 1 - 0.6376 - (0.45 × 0.6376) = 1 - 0.6376 - 0.2869 =` **0.0754**.

---

## 8. Moments, Skewness and Kurtosis

### Definitions

- **Raw moments (about origin or any point A):** `μr' = Σ(x - A)^r / n`.
- **Central moments (about the mean):** `μr = Σ(x - x̄)^r / n`. So `μ1 = 0` and `μ2 = σ²`.

### Relations: central moments from moments about any point

```
μ2 = μ2' - (μ1')²
μ3 = μ3' - 3μ2'μ1' + 2(μ1')³
μ4 = μ4' - 4μ3'μ1' + 6μ2'(μ1')² - 3(μ1')⁴
mean = A + μ1'
```

### Skewness

**Skewness** is the lack of symmetry of a distribution.

- **Positive skew:** long tail to the right; mean > median > mode.
- **Negative skew:** long tail to the left; mean < median < mode.
- **Symmetric:** mean = median = mode.

Measures:

- **Pearson:** `Sk = (mean - mode) / SD`, or `3(mean - median) / SD`.
- **Bowley:** `Sk = (Q3 + Q1 - 2·median) / (Q3 - Q1)`, which lies between -1 and +1.
- **Moment-based:** `β1 = μ3² / μ2³`, `γ1 = √β1` (take the sign of μ3). γ1 = 0 symmetric, > 0 positive skew, < 0 negative skew.

### Kurtosis

**Kurtosis** measures the peakedness of a distribution compared to the normal curve.

- `β2 = μ4 / μ2²`, `γ2 = β2 - 3`.
- **β2 = 3 (γ2 = 0): mesokurtic** (normal peak).
- **β2 < 3 (γ2 < 0): platykurtic** (flatter than normal).
- **β2 > 3 (γ2 > 0): leptokurtic** (more peaked than normal).
- **Percentile coefficient:** `κ = QD / (P90 - P10)`; for the normal curve κ = 0.263.

### 2078 Q10 / 2079 Q10 / model Q10: fourth central moment for a symmetric distribution

For a symmetric distribution μ3 = 0, so only kurtosis matters: `β2 = μ4/σ⁴`.

**SD = 7 (σ⁴ = 7⁴ = 2,401):**

- **Mesokurtic:** μ4 = 3σ⁴ = **7,203**.
- **Platykurtic:** μ4 < 7,203.
- **Leptokurtic:** μ4 > 7,203.

**SD = 9 (σ⁴ = 9⁴ = 6,561):**

- **Mesokurtic:** μ4 = **19,683**; platykurtic if μ4 < 19,683; leptokurtic if μ4 > 19,683.

### 2080 Q10: first four moments about the mean: 0, 2.8, -2, 24.5

`μ2 = 2.8`, `μ3 = -2`, `μ4 = 24.5`.

- `β1 = μ3²/μ2³ = 4 / 21.952 = 0.182`, so `γ1 = -√0.182 =` **-0.427**
- `β2 = μ4/μ2² = 24.5 / 7.84 =` **3.125**, so `γ2 = 0.125`

**Comment:** γ1 is negative, so the distribution is moderately negatively skewed (tail to the left). β2 = 3.125 is slightly above 3, so it is slightly leptokurtic (almost mesokurtic, very close to normal peakedness).

### 2082 Q11: moments about 5 are 3, 10, 40, 500

`μ1' = 3`, `μ2' = 10`, `μ3' = 40`, `μ4' = 500`.

```
μ1 = 0
μ2 = 10 - 3² = 1
μ3 = 40 - 3(10)(3) + 2(3)³ = 40 - 90 + 54 = 4
μ4 = 500 - 4(40)(3) + 6(10)(3²) - 3(3)⁴ = 500 - 480 + 540 - 243 = 317
```

**Central moments: μ1 = 0, μ2 = 1, μ3 = 4, μ4 = 317.** (Mean = 5 + 3 = 8.)

### 2081 Q2: server latencies, four central moments

Data: 120, 135, 150, 125, 140, 160, 170, 155, 165, 150 (n = 10).
Mean = 1,470/10 = **147**. Deviations `d = x - 147`:

| x     | d   | d²    | d³      | d⁴        |
| ----- | --- | ----- | ------- | --------- |
| 120   | -27 | 729   | -19,683 | 531,441   |
| 135   | -12 | 144   | -1,728  | 20,736    |
| 150   | 3   | 9     | 27      | 81        |
| 125   | -22 | 484   | -10,648 | 234,256   |
| 140   | -7  | 49    | -343    | 2,401     |
| 160   | 13  | 169   | 2,197   | 28,561    |
| 170   | 23  | 529   | 12,167  | 279,841   |
| 155   | 8   | 64    | 512     | 4,096     |
| 165   | 18  | 324   | 5,832   | 104,976   |
| 150   | 3   | 9     | 27      | 81        |
| **Σ** | 0   | 2,510 | -11,640 | 1,206,470 |

- `μ1 = 0`, `μ2 = 2510/10 = 251`, `μ3 = -11640/10 = -1,164`, `μ4 = 1206470/10 = 120,647`.
- **Mean = 147 ms. SD = √251 = 15.84 ms.**
- **Skewness:** `β1 = 1164² / 251³ = 1,354,896 / 15,813,251 = 0.0857`, `γ1 = -0.293`.
- **Kurtosis:** `β2 = 120647 / 251² = 120647 / 63001 = 1.915`, `γ2 = -1.085`.

**Nature of the data:** slightly negatively skewed (γ1 = -0.29, a longer tail to the lower latencies) and **platykurtic** (β2 = 1.92 < 3), meaning flatter than the normal curve, with a wide spread and no sharp peak.

---

## 9. Confidence Intervals

### Concepts

- **Point estimate:** a single value estimating a parameter (x̄ for μ, p̂ for p).
- **Interval estimate (confidence interval):** a range of values likely to contain the parameter, at a stated confidence level (95%, 99%).
- **Standard error (SE):** the SD of the sampling distribution of a statistic: `SE(x̄) = σ/√n`, `SE(p̂) = √(pq/n)`.

### Formulas

| Case                       | Interval                                          |
| -------------------------- | ------------------------------------------------- |
| Mean, σ known (or n large) | `x̄ ± z · σ/√n` (use `s` if σ unknown and n >= 30) |
| Mean, σ unknown, n small   | `x̄ ± t(n-1) · s/√n`                               |
| Proportion                 | `p̂ ± z · √(p̂ q̂ / n)`                              |

Critical values: **z = 1.645 (90%), 1.96 (95%), 2.576 (99%)**. Sample SD: `s = √[(Σx² - n·x̄²)/(n - 1)]`.

### Interpretation

"We are 95% confident that the true population mean lies between L and U." It does **not** mean there is a 95% probability that the mean lies in this particular interval; it means that if we repeated the sampling many times, about 95% of such intervals would contain the true value.

### 2079 Q11: vitamin E, σ = 0.042, n = 36, x̄ = 5.12

`SE = 0.042/√36 = 0.007`. Margin = 1.96 × 0.007 = 0.0137.
**95% CI = 5.12 ± 0.0137 = (5.106, 5.134) mg.**

### 2080 Q11: petrol consumption, n = 50, Σx = 525, Σx² = 5,625

`x̄ = 525/50 = 10.5`.
`s² = (5625 - 50 × 10.5²)/49 = (5625 - 5512.5)/49 = 2.296`, `s = 1.515`.
`SE = 1.515/√50 = 0.2143`. n is large, so use z = 2.576: margin = 2.576 × 0.2143 = 0.552.
**99% CI = 10.5 ± 0.552 = (9.95, 11.05) km per litre.**
**Interpretation:** we are 99% confident that the true mean fuel consumption of this car model lies between about 9.95 and 11.05 km per litre.

### 2081 Q6: proportion satisfied, n = 80, x = 56

`p̂ = 56/80 = 0.70`, `q̂ = 0.30`. `SE = √(0.7 × 0.3/80) = 0.0512`.
Margin = 1.96 × 0.0512 = 0.1004.
**95% CI = 0.70 ± 0.100 = (0.60, 0.80).** We are 95% confident that between 60% and 80% of all customers are satisfied.

### 2082 Q9: proportion satisfied, n = 400, x = 350

`p̂ = 0.875`, `q̂ = 0.125`. `SE = √(0.875 × 0.125/400) = 0.01654`.

- **95% CI:** 0.875 ± 1.96 × 0.01654 = 0.875 ± 0.0324 = **(0.8426, 0.9074)**
- **99% CI:** 0.875 ± 2.576 × 0.01654 = 0.875 ± 0.0426 = **(0.8324, 0.9176)**

The 99% interval is wider: more confidence requires a wider interval.

### Model Q11: data 1, 2, 3, 4, 5, 20 (n = 6; population assumed normal)

σ is unknown and n is small, so use the **t distribution** with 5 degrees of freedom: `t(0.025, 5) = 2.571`.

**Original data:** `x̄ = 35/6 = 5.83`; `Σx² = 455`, `s² = (455 - 6 × 5.83²)/5 = 50.17`, `s = 7.08`.
`SE = 7.08/√6 = 2.89`; margin = 2.571 × 2.89 = 7.43.
**95% CI = 5.83 ± 7.43 = (-1.60, 13.27).**

**After replacing 20 by 6** (data 1, 2, 3, 4, 5, 6): `x̄ = 3.5`, `s² = 3.5`, `s = 1.871`.
`SE = 1.871/√6 = 0.764`; margin = 2.571 × 0.764 = 1.96.
**95% CI = 3.5 ± 1.96 = (1.54, 5.46).**

**Why the large difference:** the value 20 is an outlier. It pulls the mean up and inflates the sample SD (7.08 vs 1.87), which makes the standard error and the interval much wider. The mean and SD are not robust to outliers.

---

## 10. Sampling and Sampling Distribution

### Basic terms

- **Population:** the entire group of interest. **Sample:** a part of the population selected for study.
- **Parameter:** a numerical characteristic of a **population** (μ, σ, p). **Statistic:** a numerical characteristic of a **sample** (x̄, s, p̂); it is used to estimate the parameter and varies from sample to sample.

### Census vs sample survey

| Point         | Census survey                                           | Sample survey                                            |
| ------------- | ------------------------------------------------------- | -------------------------------------------------------- |
| Coverage      | Every unit of the population                            | Only a selected part                                     |
| Cost / time   | High / long                                             | Low / short                                              |
| Accuracy      | No sampling error, but non-sampling errors can be large | Has sampling error                                       |
| Suitable when | Population is small, or complete information is needed  | Population is large, infinite, or testing is destructive |
| Example       | Population census                                       | Opinion poll                                             |

### Sampling error vs non-sampling error (2078 Q11)

|                         | Sampling error                                                                                                      | Non-sampling error                                                                                                                          |
| ----------------------- | ------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------- |
| Meaning                 | Difference between a sample statistic and the true population parameter, arising because only a sample was observed | Errors from causes other than sampling: faulty data collection, measurement, non-response, recording and processing mistakes, poor coverage |
| Occurs in               | Sample surveys only                                                                                                 | Both census and sample surveys                                                                                                              |
| Effect of larger sample | **Decreases**                                                                                                       | Does **not** decrease (may even increase)                                                                                                   |
| Controlled by           | Larger sample, better design                                                                                        | Careful questionnaire design, training, checking                                                                                            |

### Types of sampling

- **Probability sampling:**
  - **Simple random sampling (SRS):** every unit has an equal chance of selection (lottery or random numbers).
  - **Systematic sampling:** select every k-th unit (`k = N/n`) after a random start.
  - **Stratified sampling (2081 Q12):** divide the population into homogeneous, non-overlapping groups (**strata**), then take a random sample from every stratum (often proportional: `n_i = n × N_i/N`). It improves precision and ensures every group is represented. Example: sampling BIT students by year.
  - **Cluster sampling (2082 Q12):** divide the population into naturally formed groups (**clusters**, each a mini-population: wards, schools, villages), randomly select some clusters, and survey **all** units in the chosen clusters. It is cheaper and practical when a list of units is not available, but is usually less precise than SRS.
- **Non-probability sampling** (no known chance of selection): convenience, judgement (purposive), quota, snowball.

### Standard error, sampling distribution, central limit theorem

- **Sampling distribution:** the probability distribution of a statistic over all possible samples of the same size.
- **Standard error:** `SE(x̄) = σ/√n`; `SE(p̂) = √(pq/n)`.
- **Central limit theorem (CLT):** for large n (about 30 or more), the sampling distribution of the sample mean is approximately normal with mean μ and SD σ/√n, whatever the shape of the population.
- **Need for inferential statistics:** studying a whole population is often impossible or costly, so we use samples to estimate parameters and test claims.

### Model Q3: sampling distribution of the mean

Population: 1, 3, 6, 7 (N = 4). `μ = 17/4 = 4.25`. `σ² = (1 + 9 + 36 + 49)/4 - 4.25² = 23.75 - 18.0625 = 5.6875`, `σ = 2.385`.

**(a) All 16 samples of size 2 with replacement, and their means:**

```
(1,1)=1    (1,3)=2    (1,6)=3.5   (1,7)=4
(3,1)=2    (3,3)=3    (3,6)=4.5   (3,7)=5
(6,1)=3.5  (6,3)=4.5  (6,6)=6     (6,7)=6.5
(7,1)=4    (7,3)=5    (7,6)=6.5   (7,7)=7
```

| x̄    | 1    | 2    | 3    | 3.5  | 4    | 4.5  | 5    | 6    | 6.5  | 7    | Total |
| ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ----- |
| f    | 1    | 2    | 1    | 2    | 2    | 2    | 2    | 1    | 2    | 1    | 16    |
| P(x̄) | 1/16 | 2/16 | 1/16 | 2/16 | 2/16 | 2/16 | 2/16 | 1/16 | 2/16 | 1/16 | 1     |

**(b)** Mean of all sample means = `68/16 = 4.25` = population mean. **Yes, they are equal** (the sample mean is an unbiased estimator: `E(x̄) = μ`).

**(c) Shape:** the population values 1, 3, 6, 7 each occur once (flat, roughly uniform, not bell-shaped). The sampling distribution of the mean is concentrated near the centre, with fewer values at the extremes, and looks closer to a bell shape. This illustrates the CLT: sample means tend toward a normal shape even when the population isn't normal.

**(d) SD:** the SD of sample means = `√2.84375 = 1.686`. This equals `σ/√n = 2.385/√2 = 1.686`. The sampling distribution is **less spread out** than the population (1.69 vs 2.39), and the spread shrinks as n grows.

---

## 11. Central Tendency and Exploratory Data Analysis

### Measures of central tendency

| Measure                | Formula (ungrouped / grouped)                                     |
| ---------------------- | ----------------------------------------------------------------- |
| **Arithmetic mean**    | `x̄ = Σx/n`; grouped: `Σfx/Σf`                                     |
| **Weighted mean**      | `Σwx / Σw`                                                        |
| **Median**             | Middle value of ordered data; grouped: `L + (N/2 - cf)/f × h`     |
| **Mode**               | Most frequent value; grouped: `L + (f1 - f0)/(2f1 - f0 - f2) × h` |
| **Empirical relation** | `Mode = 3 Median - 2 Mean`                                        |

Properties of the mean: the sum of deviations from the mean is zero; `Σ(x - x̄)²` is a minimum; the mean is affected by every value (including outliers); if every value is changed by `ax + b`, the mean becomes `a·x̄ + b`.

### Choice of an appropriate measure of central tendency (2078 Q12a, 2080 Q12b, model Q12b)

- **Mean:** for quantitative data that is roughly symmetric with no extreme values (interval/ratio scale). It uses all the data and is the base of further statistics.
- **Median:** when the data are **skewed or have outliers** (income, house prices), for open-ended classes, and for ordinal data.
- **Mode:** for **nominal/categorical** data (most popular brand) and when the most common value is wanted.
- **Geometric mean:** for growth rates and ratios. **Harmonic mean:** for averaging speeds or rates.

### Exploratory data analysis: five-number summary and box plot

**Five-number summary:** minimum, Q1, median (Q2), Q3, maximum.
`IQR = Q3 - Q1`. **Outlier fences:** lower = `Q1 - 1.5 × IQR`, upper = `Q3 + 1.5 × IQR`; values outside the fences are outliers.

**Box-and-whisker plot:** a box from Q1 to Q3 with a line at the median, and whiskers extending to the smallest and largest values within the fences (outliers plotted as separate points).

**Uses (2079 Q12a, 2080 Q12a):** shows the centre, spread and shape in one picture; detects outliers; compares several groups side by side; assesses skewness.
**Skewness from a box plot:** median in the middle of the box with equal whiskers means symmetric; median nearer Q1 with a longer upper whisker means positive skew; median nearer Q3 with a longer lower whisker means negative skew.

### 2081 Q9: file transfer times, five-number summary

Data (11 sessions): 100, 120, 110, 115, 130, 105, 125, 122, 112, 108, 135.
Sorted: 100, 105, 108, 110, 112, **115**, 120, 122, 125, 130, 135.

- Minimum = **100**; maximum = **135**
- Median = 6th value = **115**
- Q1 = median of the lower five (100, 105, 108, 110, 112) = **108**
- Q3 = median of the upper five (120, 122, 125, 130, 135) = **125**
- IQR = 125 - 108 = 17. Fences: 108 - 25.5 = 82.5 and 125 + 25.5 = 150.5. **No outliers.**

**Box plot:** draw a number line from 100 to 135; the box runs from 108 to 125 with a line at 115; the whiskers go to 100 and 135. The median (115) is a bit closer to Q1 (distance 7) than Q3 (distance 10), so the data are slightly positively skewed.

---

## 12. Diagrams and Graphs

### Pie chart (2078 Q5, 2081 Q4)

Each category's angle = `(value / total) × 360°`.

**2078 Q5** (total = 24 hours):

| Activity | Hours | Angle |
| -------- | ----- | ----- |
| School   | 6     | 90°   |
| Sleep    | 8     | 120°  |
| Playing  | 2     | 30°   |
| Study    | 4     | 60°   |
| T.V.     | 1     | 15°   |
| Others   | 3     | 45°   |
| Total    | 24    | 360°  |

**2081 Q4** (total = 50 students):

| Language   | Students | Percent | Angle |
| ---------- | -------- | ------- | ----- |
| Python     | 20       | 40%     | 144°  |
| Java       | 15       | 30%     | 108°  |
| C++        | 10       | 20%     | 72°   |
| JavaScript | 5        | 10%     | 36°   |

Draw a circle, divide it using a protractor in these angles, and label each sector with its name and value.

### Bar diagram and Pareto chart (2080 Q5, 2082 Q4)

| Point      | Bar diagram        | Pareto chart                                                                                         |
| ---------- | ------------------ | ---------------------------------------------------------------------------------------------------- |
| Bar order  | Any order          | **Descending** order of frequency                                                                    |
| Extra line | None               | **Cumulative percentage line** on a second axis                                                      |
| Purpose    | Compare categories | Identify the "vital few" categories causing most of the effect (80/20 rule); used in quality control |

**2080 Q5** (total 400):

| Mode    | Students | %   | Cumulative % |
| ------- | -------- | --- | ------------ |
| Bus     | 200      | 50% | 50%          |
| Bicycle | 100      | 25% | 75%          |
| On foot | 80       | 20% | 95%          |
| By car  | 20       | 5%  | 100%         |

_Bar diagram:_ draw separate bars with heights 200, 100, 80, 20 and gaps between them. _Pareto diagram:_ the same bars in descending order (already so), plus a line through the cumulative percentage points (50, 75, 95, 100). Bus and bicycle together account for 75% of the students.

### Histogram, frequency polygon, frequency curve (2079 Q5)

Data: classes 0-20, 20-40, 40-60, 60-80, 80-100 with frequencies 10, 22, 35, 28, 5. (The paper's "80-11" is read as 80-100, class width 20.)

- **Histogram:** adjacent rectangles (no gaps) with class boundaries on the x-axis and heights equal to the frequencies 10, 22, 35, 28, 5.
- **Frequency polygon:** plot frequencies against class **mid-points** 10, 30, 50, 70, 90 and join them with straight lines. Close the polygon by adding mid-points -10 and 110 with frequency 0.
- **Frequency curve:** smooth the polygon into a curve without sharp corners.

```
Freq
 35 |            ███
 28 |            ███ ███
 22 |        ███ ███ ███
 10 |    ███ ███ ███ ███
  5 |    ███ ███ ███ ███ ███
    +-----------------------------
      0   20  40  60  80  100  Marks
```

**Interpretation:** most students scored 40-60 (the modal class); the distribution is roughly symmetric, with few very low or very high scorers.

### Ogive (cumulative frequency curves)

For the same data:

| Class limit | Less-than cumulative | More-than cumulative |
| ----------- | -------------------- | -------------------- |
| 0           | 0                    | 100                  |
| 20          | 10                   | 90                   |
| 40          | 32                   | 68                   |
| 60          | 67                   | 33                   |
| 80          | 95                   | 5                    |
| 100         | 100                  | 0                    |

Plot less-than values against upper limits (rising curve) and more-than values against lower limits (falling curve). The two curves cross at the median (about 50.3 marks).

### Stem-and-leaf display

Split each value into a stem (leading digits) and leaf (last digit). Example for 32, 35, 41, 47, 48, 53:

```
3 | 2 5
4 | 1 7 8
5 | 3
```

It keeps the raw data while showing the distribution's shape.

---

## 13. Introduction: Scales, Data, Role of Statistics

### Basics

- **Statistics:** the science of collecting, organizing, presenting, analysing and interpreting data to support decisions.
- **Descriptive statistics:** methods that organize and summarize the data (tables, graphs, averages, spread).
- **Inferential statistics:** methods that use sample data to draw conclusions about a population (estimation, hypothesis testing).
- **Limitations:** it deals with groups, not individuals; it is true only on average; it studies only quantifiable facts; results can be misused or misinterpreted; results depend on data quality.

### Scales of measurement (2078 Q4, 2082 Q5, model Q4)

**Measurement scale:** the system used to assign numbers or labels to characteristics, determining which operations and statistics are meaningful.

| Scale        | Property                                                     | Example                              | Suitable average  |
| ------------ | ------------------------------------------------------------ | ------------------------------------ | ----------------- |
| **Nominal**  | Categories only, no order                                    | Blood group, gender, brand           | Mode              |
| **Ordinal**  | Categories with a meaningful order, but unequal/unknown gaps | Rank, grade, Likert scale, age group | Median (and mode) |
| **Interval** | Equal gaps, **no true zero**                                 | Temperature in °C, calendar year, IQ | Mean              |
| **Ratio**    | Equal gaps and a **true zero**                               | Height, weight, income, time         | Mean (and GM, CV) |

**Ordinal vs interval (model Q4):** in an ordinal scale the order is known but the distance between values is not equal or meaningful (the gap between "good" and "excellent" is not measurable); in an interval scale the distances are equal and meaningful (the difference between 20°C and 30°C equals that between 30°C and 40°C), but there is no true zero (0°C is not "no temperature"), so ratios such as "twice as hot" are meaningless.

### 2082 Q5: fill the table

| Variable                                | Measurement scale | Best statistical method |
| --------------------------------------- | ----------------- | ----------------------- |
| Blood group                             | Nominal           | Mode                    |
| Students' satisfaction (5-point Likert) | Ordinal           | Median (or mode)        |
| Annual income                           | Ratio             | Mean (median if skewed) |
| Age group (18-25, 26-35, 36-45, 46+)    | Ordinal           | Median / mode           |
| Lifetime of an electronic device        | Ratio             | Mean                    |

_Note:_ some courses treat a Likert scale as interval and use the mean. The standard textbook answer is ordinal with the median or mode.

### Variables and data

- **Variables:** _discrete_ (countable: number of students), _continuous_ (any value in a range: time), _categorical_ (labels: gender).
- **Types of data:** _cross-sectional_ (collected at one point in time from many units) and _longitudinal_ (collected on the same units over time).
- **Data preparation:** _editing_ (checking for errors and inconsistencies), _coding_ (assigning numeric codes to responses), _transcribing_ (entering the data into a computer file).

### Primary vs secondary data (2082 Q12b, 2079 Q4)

- **Primary data:** collected **first-hand** by the researcher for the specific purpose (surveys, interviews, observation, experiments). It is original and specific but costly and time-consuming.
- **Secondary data:** already collected by someone else and available for use. It is cheaper and quicker, but may be outdated or not fit the purpose exactly.

**Sources of secondary data in Nepal:**

- Central Bureau of Statistics (now the National Statistics Office): population census, national surveys, Nepal Living Standards Survey.
- Ministry of Finance: Economic Survey. Nepal Rastra Bank: economic and financial reports.
- Ministry of Health: Nepal Demographic and Health Survey. Ministry of Education: education statistics.
- Nepal Telecommunications Authority: telecom and internet usage data.
- Published sources: government reports, journals, newspapers, research papers, and international bodies such as the World Bank and UN agencies.

### Role of statistics in information technology (2080 Q4, 2081 Q11)

- **Data analysis and machine learning:** regression, classification, probability models.
- **Performance evaluation:** response time, latency and throughput summarized with mean, SD, percentiles.
- **Quality assurance and testing:** defect rates, sampling inspection, reliability and failure analysis.
- **Network and server modelling:** traffic, queues and request arrivals use the Poisson distribution.
- **Data mining and big data:** pattern detection, correlation analysis, anomaly detection (e.g., in cybersecurity).
- **Software engineering:** effort and cost estimation (regression), A/B testing.
- **Databases and search:** query optimization, sampling for large datasets.
- **Decision-making:** capacity planning, risk assessment, forecasting.

---

## 14. Formula Sheet

```
DESCRIPTIVE
  Mean = Σx/n        Variance σ² = Σx²/n - x̄²       CV = σ/x̄ × 100
  Mode = 3 Median - 2 Mean
  IQR = Q3 - Q1       Outlier fences: Q1 - 1.5 IQR, Q3 + 1.5 IQR
  Pearson Sk = (mean - mode)/SD    Bowley Sk = (Q3 + Q1 - 2 Med)/(Q3 - Q1)

MOMENTS
  μ2 = μ2' - μ1'²
  μ3 = μ3' - 3μ2'μ1' + 2μ1'³
  μ4 = μ4' - 4μ3'μ1' + 6μ2'μ1'² - 3μ1'⁴
  β1 = μ3²/μ2³   γ1 = ±√β1      β2 = μ4/μ2²   γ2 = β2 - 3
  Mesokurtic β2 = 3 (μ4 = 3σ⁴)   Platykurtic β2 < 3   Leptokurtic β2 > 3

CORRELATION AND REGRESSION
  Sxy = ΣXY - ΣXΣY/n    Sxx = ΣX² - (ΣX)²/n    Syy = ΣY² - (ΣY)²/n
  r = Sxy/√(Sxx·Syy)      R² = r²
  b = Sxy/Sxx    a = Ȳ - bX̄    Ŷ = a + bX
  r = ±√(b_xy · b_yx)
  Spearman rs = 1 - 6Σd²/(n(n² - 1))

PROBABILITY
  P(A∪B) = P(A) + P(B) - P(A∩B)
  P(A∩B) = P(A)P(B|A)       P(A|B) = P(A∩B)/P(B)
  Bayes: P(Ai|B) = P(Ai)P(B|Ai) / ΣP(Aj)P(B|Aj)

RANDOM VARIABLES
  E(X) = Σx·P(x)    Var(X) = E(X²) - [E(X)]²
  E(aX+b) = aE(X) + b    Var(aX+b) = a²Var(X)

DISTRIBUTIONS
  Binomial: P(x) = C(n,x) p^x q^(n-x)   mean np   var npq
  Poisson:  P(x) = e^(-λ) λ^x / x!      mean = var = λ
  Normal:   Z = (X - μ)/σ

ESTIMATION
  Mean (σ known):    x̄ ± z σ/√n
  Mean (σ unknown):  x̄ ± t s/√n
  Proportion:        p̂ ± z √(p̂q̂/n)
  z: 1.645 (90%)   1.96 (95%)   2.576 (99%)
  SE(x̄) = σ/√n     SE(p̂) = √(pq/n)
```

---

**Final advice:** Every paper so far gave two or three guaranteed template numericals: a CV comparison, a regression line and a normal-distribution problem. Practise those until you can do each in under 15 minutes, then work on probability, expectation, the binomial/Poisson problems, and confidence intervals. Show every step in your working: marks are awarded for the formula, the substitution and the interpretation, not just the final number.
