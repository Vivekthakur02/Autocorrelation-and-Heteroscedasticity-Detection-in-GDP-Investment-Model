<p align="center">
  <img src="https://cdn-icons-png.freepik.com/512/7532/7532680.png" alt="Adidas Logo" width="180"/>
</p>

<h1 align="center">🏢 Autocorrelation and Heteroscedasticity Detection & Resolution </h1>

<p align="center">
  <b> Econometrics Term Project</b><br>
  <i>IIT Kharagpur</i>
</p>
Autocorrelation-and-Heteroscedasticity-Detection-in-GDP-Investment-Model
This project analyzes the relationship between India’s economic growth (GDP) and investment levels (GCF) using real data from the Reserve Bank of India (RBI) for the years 1951–2007.


##  Step 1: Data Collection and Model Specification

This project begins by exploring the relationship between **India’s GDP (Gross Domestic Product)** and **Gross Capital Formation (GCF)** — a key indicator of investment in the economy.
In simple terms, the goal was to understand whether higher investment levels are associated with higher national output over time.

###  Data Overview

* **Source:** Reserve Bank of India (RBI) – official annual time-series data.
* **Period:** 1951 – 2007
* **Variables Used:**

  * **GDP (Gross Domestic Product at Market Prices)** – measures total economic output.
  * **GCF (Gross Capital Formation)** – measures the total value of investments made in the economy.
* **Unit of Measurement:** Indian Rupees (INR crore)

Before running any model, the dataset was checked for:

* Missing or inconsistent values
* Outliers or extreme observations
* Overall trend patterns through **line charts** and **scatter plots**

##  Step 2 — OLS Estimation & Interpretation

### ⚙️ Model Framework

To represent the relationship, a simple linear regression model was used:

GDP_t = β₀ + β₁*GCF_t + ε_t

* **β₀** = Intercept – base level of GDP when GCF = 0
* **β₁** = Slope – average change in GDP for a one-unit change in GCF
* **ε** = Error term – captures other macroeconomic factors not included in the model

---

### 🧮 Estimated Regression Equation

Using RBI time-series data (1951 – 2008), the estimated equation was:

GDP_GCF = 293639.3+ 2.942763 GCF

**Key Results**

| Statistic              | Value  | Interpretation                                          |
| ---------------------- | ------ | ------------------------------------------------------- |
| **R²**                 | 0.9585 | GCF explains ~95.8 % of GDP variation                   |
| **β₁ (p-value)**       | < 0.01 | Investment’s impact on GDP is statistically significant |
| **Durbin–Watson (DW)** | 0.211  | Indicates strong positive autocorrelation in residuals  |

---
R² measures how much of the variation in the dependent variable is explained by the independent variable.

###  Interpretation

* **Positive relationship:** Every ₹ 1 crore increase in investment corresponds, on average, to a ₹ 2.94 crore increase in GDP.
* **High R²:** The model shows a strong fit, but time-series trends can inflate R²; diagnostic testing is required to confirm reliability.
* **Autocorrelation detected:** A DW ≈ 0.21 suggests residuals are positively correlated—violating OLS independence assumptions. This issue was addressed later using **Cochrane–Orcutt**, **Prais–Winsten**, and **First-Difference** corrections.

---

###  Stata Commands Used

```stata
reg gdp gcf
lfit gdp gcf
predict resid, residuals
dwstat
```

## 🧠 Step 3: Detection of Autocorrelation and Heteroscedasticity  

After estimating the initial regression model:  


GDP_GCF = 293639.3+ 2.942763 GCF

The residuals were examined to verify key **OLS assumptions** — independence and homoscedasticity of errors. Several diagnostic tests were conducted to ensure the model’s reliability and robustness.

---

### 🔍 1. Autocorrelation Tests  

Autocorrelation occurs when the error term in one period is correlated with errors in previous periods — a common issue in time-series data. It indicates that the model fails to fully capture temporal dependencies in GDP and GCF.

| **Test** | **Purpose** | **Result** | **Interpretation** |
|:--|:--|:--|:--|
| **Durbin–Watson (DW)** | Detects first-order serial correlation | DW = **0.211** | Strong **positive autocorrelation** (since DW < 2) |
| **Runs Test** | Checks randomness in residual signs | Non-random pattern | Confirms persistence of errors across years |
| **Breusch–Godfrey (BG)** | Detects higher-order autocorrelation | Significant result | Indicates multi-period autocorrelation |

**Insight:**  
A DW statistic of 0.211 suggests that residuals from consecutive years move in the same direction — when the model underpredicts GDP one year, it tends to underpredict again the next year.  
This violates the classical OLS assumption of independent errors.

---

### 📉 2. Heteroscedasticity Test  

Heteroscedasticity implies that the variance of residuals changes over time — the model errors are not constant across observations.  

| **Test** | **Purpose** | **Result** | **Interpretation** |
|:--|:--|:--|:--|
| **White’s Test** | Tests for non-constant variance in residuals | Test statistic = **7.09**, p < 0.05 | Presence of **heteroscedasticity** confirmed |

**Insight:**  
The residual spread increased in later years, likely due to rising macroeconomic volatility.  
This violates the homoscedasticity assumption of OLS, leading to unreliable standard errors and biased inference.

Both diagnostic sets confirm violations of OLS assumptions:

- **Autocorrelation** → model errors follow a time-dependent pattern.  
- **Heteroscedasticity** → error variance is not constant across years.

To correct these issues, the model was re-estimated using the following transformation techniques (explained in **Step 4**):

- 🔸 **Cochrane–Orcutt Transformation**  
- 🔸 **Prais–Winsten Transformation**  
- 🔸 **First-Difference Method**

These approaches eliminated serial correlation and stabilised variance, leading to a more efficient and reliable econometric model.

## **Step 4 – Remedies for Autocorrelation**

After detecting strong positive autocorrelation in the OLS residuals *(Durbin–Watson = 0.211)*,  
the model was corrected using three standard econometric transformation methods to restore the validity of OLS assumptions.

---

### **1️⃣ Cochrane–Orcutt (C–O) Transformation**

**Idea:**  
Assumes the error term follows an AR(1) process  
ε_t = 𝜌ε_t-1 + u_t

**Procedure:**  
Estimate \( \rho \approx 1 - \tfrac{DW}{2} \), then transform variables as  
Y_t - 𝜌Y_t-1 = β_0(1-𝜌) + β_1(X_t - 𝜌 X_t-1) + u_t

**Result:**  
Durbin–Watson increased from 0.21 to ≈ 2.0, indicating that serial correlation was effectively removed.

---

### **2️⃣ Prais–Winsten (P–W) Transformation**

**Purpose:**  
A refined version of Cochrane–Orcutt that retains the first observation, improving efficiency.

**Implementation:**  
Transforms variables similarly while adjusting the first observation using √(1 − ρ²).

**Result:**  
DW ≈ 1.95 → residuals became independent and OLS efficiency was restored.

---

### **3️⃣ First-Difference Model**

**Concept:**  
By differencing the variables,
 ΔY_t = β_1 *  ΔX_t +  Δ u_t
any serial dependence in levels is removed.

**Interpretation:**  
The model now captures how *changes* in investment (GCF) influence *changes* in GDP.

**Outcome:**  
DW ≈ 2.0 → autocorrelation eliminated.

---

Sure, Vivek 👍 — here’s your **Step 5 (Remedies for Heteroscedasticity)** written in a clean, professional tone for your **GitHub README.md** file — consistent with your earlier steps’ format and project language style 👇

---

### 🧮 **Step 5: Remedies for Heteroscedasticity**

After detecting heteroscedasticity through **White’s Test (p < 0.05)**, the variance of residuals was found to be non-constant, violating the homoscedasticity assumption of OLS. To address this issue, two corrective approaches were implemented:

1. **Weighted Least Squares (WLS):**

   * Assigned weights inversely proportional to the error variance, giving less importance to high-variance observations.
   * This transformation stabilized the residual variance and improved the efficiency of coefficient estimates.
   * *(Stata Command: `reg gdp gcf [aw=1/gcf]`)*

2. **Robust Standard Errors (White/Huber Correction):**

   * Applied heteroscedasticity-consistent standard errors to ensure valid inference without altering coefficient estimates.
   * *(Stata Command: `reg gdp gcf, robust`)*

After correction, **White’s Test yielded p > 0.05**, confirming that **heteroscedasticity had been successfully eliminated**. The final model satisfied all Classical Linear Model (CLM) assumptions, with stable coefficients and reliable statistical inference.

---
GDP = 264825 + 2.88 × GCF
R^2 ≈ 0.94
DW≈1.97
p<0.01 for β₁
→ Clean, efficient, and statistically valid model.

##  Step 6 – Model Comparison & Policy Interpretation

After detecting and correcting for both autocorrelation and heteroscedasticity, all models were compared to evaluate improvements in model efficiency and reliability.

| Model | Method Used | DW Statistic | R² | Key Observation |
|:--|:--|:--|:--|:--|
| Model 1 | OLS (Baseline) | 0.211 | 0.9585 | Strong autocorrelation present |
| Model 2 | Cochrane–Orcutt | ≈ 2.01 | 0.942 | Autocorrelation removed |
| Model 3 | Prais–Winsten | ≈ 1.95 | 0.943 | Autocorrelation removed, stable coefficients |
| Model 4 | First Difference | ≈ 2.03 | 0.91 | Trend eliminated, independence achieved |
| Model 5 | Weighted Least Squares | ≈ 1.97 | 0.94 | Variance stabilized (no heteroscedasticity) |

### 📊 Key Findings
- Post-correction DW ≈ 2 → Residuals are random and independent.  
- White’s Test p > 0.05 → Error variance is constant.  
- Coefficients remain stable (β₁ ≈ 2.88 vs 2.94 in OLS) → robust relationship.

### 💡 Economic Interpretation
The final refined model:

GDP = 264825 + 2.88 * GCF

Each ₹1 crore increase in **Gross Capital Formation (GCF)** results in an average ₹2.88 crore rise in **GDP**.  
This supports the **Investment-Led Growth Hypothesis** for India (1951 – 2008).

### 🧭 Policy Implication
Encouraging capital formation through infrastructure development, fiscal incentives, and ease-of-doing-business reforms can significantly enhance India’s GDP growth trajectory.

###  Summary
| Aspect | Before Correction | After Correction | Result |
|:--|:--|:--|:--|
| DW Statistic | 0.21 | ≈ 2.0 | Autocorrelation removed |
| White’s Test p-value | < 0.05 | > 0.05 | Homoscedasticity restored |
| R² | 0.96 | 0.94 | Model more realistic |
| β₁ (Investment Impact) | 2.94 | 2.88 | Stable & significant |

> **Final Insight:**  
> Investment significantly drives GDP growth in India — policies that enhance Gross Capital Formation can effectively stimulate economic development.

