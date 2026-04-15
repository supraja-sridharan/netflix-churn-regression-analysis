# Netflix Content Quality & User Churn — Regression Analysis

> **Course:** GSBA 545 — Data-Driven Decision Making | USC Marshall School of Business | Fall 2025  
> **Team B9:** Yuhan (Wynter) Zhu, Vinish Dhir, Supraja Sridharan, Pin-Sheng Chen (Kyro), Haewon Kim (Hanna), Yan Yang (Claire), Alexei Orlov  
> **Professor:** Dawn Porter

---

## 📌 Project Overview

This project investigates whether the availability of **higher-rated Netflix content** in a user's region is associated with a **lower likelihood of churn**. Using multivariate linear regression, we examined whether content quality plays a significant role in subscriber retention — a question increasingly relevant as streaming platforms compete through original content investment.

---

## 🔍 Research Question

> **Does the average IMDb rating of Netflix content available in a user's country predict lower user churn?**

---

## 📂 Data Sources

All datasets were sourced from **Kaggle**:

| Dataset | Description |
|---|---|
| Netflix Titles | Shows, movies, and country availability |
| IMDb Ratings | Numerical content rating scores (1–10) |
| IMDb AKAs | Alternate titles for accurate title matching |
| Netflix Users | User watch time, age, subscription type, and favorite genre |

---

## 🧮 Model

**OLS Multivariate Linear Regression:**

```
churn_i = β0 + β1 * avg_rating_available_i + β2 * Age_i
        + β3 * sub_Premium_i + β4 * sub_Standard_i
        + Σ γ_g * GenreDummy_ig + ε_i
```

### Variables

- **Dependent Variable:** `churn` — defined as being in the bottom 25% of watch time hours
- **Key Independent Variable:** `avg_rating_available` — average IMDb rating of content available in the user's country
- **Controls:** Age, Subscription Type (Basic / Standard / Premium), Favorite Genre

---

## 📊 Key Results

| Variable | Coefficient | Interpretation |
|---|---|---|
| `avg_rating_available` | **−0.038** | A 1-point increase in avg. rating → ~3.8pp decrease in churn |
| `genre_Drama` | −0.021 | Strongest genre effect on reducing churn |
| `genre_Comedy` | −0.009 | Moderate negative effect on churn |
| `sub_Standard` | +0.012 | Standard users churn slightly more than Basic |
| `Age` | −0.0001 | Minimal effect |

- **p-value (avg_rating_available):** 0.029 *(statistically significant at α = 0.05)*
- **R²:** 0.00065 *(modest — churn is influenced by many unobserved factors)*

---

## 💡 Key Insights

- Higher-rated regional content is **statistically significantly associated with lower churn**, supporting the hypothesis.
- **Drama** is the genre most strongly linked to subscriber retention.
- **Younger users (under 20)** exhibit the highest churn; users in their 50s–60s churn least.
- **Standard-plan subscribers** churn more than Basic or Premium users, suggesting weakest value perception at the mid-tier.
- The model's low R² indicates churn is driven by many **unobserved behavioral factors** (e.g., engagement frequency, recency, personalized recommendations).

---

## 🔧 Tools & Methods

- **Language:** Python
- **Libraries:** `numpy`, `pandas`, `statsmodels`
- **Regression Method:** Ordinary Least Squares (OLS) via `numpy.linalg.lstsq`
- **Data Wrangling:** Title normalization, multi-dataset merging, dummy variable encoding
- **Churn Definition:** Bottom 25th percentile of `Watch_Time_Hours`

---

## 📋 Limitations & Future Work

- **Low R²** — many behavioral drivers of churn (recency, session patterns) were not available
- IMDb ratings are a **proxy** for content quality; individual preferences vary widely
- A **logistic regression model** would be more appropriate for a binary churn outcome
- Future work could incorporate richer engagement data and user-level behavioral signals

---

## 📄 Report

The full project report is available in the [`report/`](./report/) folder.
