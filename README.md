# A/B Testing — Cookie Cats Gate Placement Experiment

End-to-end experiment analysis on a real mobile game dataset, covering outlier handling, retention analysis, normality testing, and non-parametric statistical inference.

---

## 🎯 Business Problem

Tactile Entertainment ran an A/B test on their mobile game **Cookie Cats**, moving the first in-game purchase gate from **level 30 (control)** to **level 40 (treatment)**. The goal: understand whether this change improves player engagement (rounds played) and retention (day 1 and day 7).

This is a classic product experimentation problem — balancing monetization against player experience.

---

## 🧪 Experiment Design

| | Control (Gate 30) | Treatment (Gate 40) |
|---|---|---|
| **Gate position** | Level 30 | Level 40 |
| **Hypothesis** | Earlier friction reduces engagement | Later friction improves retention |
| **Primary metric** | Sum of game rounds played | |
| **Secondary metrics** | 1-day retention, 7-day retention | |

---

## 📐 Methodology

### 1. Exploratory Analysis
- Distribution analysis of game rounds across both groups
- Identification and removal of extreme outlier (single user with anomalous game rounds)
- Player drop-off analysis at key game milestones

### 2. Retention Analysis
- Computed 1-day and 7-day retention rates per group
- Analyzed combined retention (retained on both day 1 and day 7)
- Segmented by `NewRetention` categories across game versions

### 3. Statistical Hypothesis Testing

```
H₀: No significant difference in sum_gamerounds between gate_30 and gate_40
H₁: Significant difference exists between the two groups
```

**Testing pipeline:**
1. **Shapiro-Wilk test** → assess normality
2. Data found to be **non-parametric** → proceed to non-parametric test
3. **Mann-Whitney U test** → compare distributions without normality assumption
4. If parametric: **Levene's test** for variance homogeneity → **t-test** or **Welch's t-test**

The `AB_Test()` function automates this entire pipeline and returns a structured results DataFrame.

---

## 📊 Key Results

- Gate 30 shows **higher 1-day and 7-day retention** than gate 40
- Moving the gate later does **not** improve engagement — players disengage before reaching level 40
- Statistical test confirms the difference is significant
- **Recommendation:** Keep the gate at level 30

---

## 🛠 Stack

- **pandas, NumPy** — data manipulation
- **scipy.stats** — Shapiro-Wilk, Mann-Whitney U, Levene, t-tests
- **seaborn, matplotlib** — visualizations

---

## 📁 Structure

```
├── A_B_Testing_Step_by_Step.ipynb   # Full analysis notebook
├── cookie_cats.csv                   # Dataset
└── requirements.txt
```

---

## 🚀 Getting Started

```bash
pip install numpy pandas seaborn matplotlib scipy
jupyter notebook "A_B_Testing_Step_by_Step.ipynb"
```

---

## 📌 Related Projects

- [Customer Lifetime Value](https://github.com/Ajay-Deshpande/Customer-Lifetime-Value) — customer value modeling and segmentation
- [product-design-AB-testing](https://github.com/Ajay-Deshpande/product-design-AB-testing) — additional A/B testing analysis
