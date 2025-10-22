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



