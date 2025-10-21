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


###  Methodology

1. **Model Building:**
   We built a simple linear regression model:

   GDP = β₀ + β₁* GCF + ε
   
   Here, GDP represents total output, GCF represents investment, and (ε) is the error term capturing other unobserved factors.

2. **OLS Estimation:**
   Using **Ordinary Least Squares (OLS)**, we estimated the parameters of the model.
   The regression showed a strong positive relationship between GDP and GCF with an **R² ≈ 0.96**, meaning that investment explained about 96% of GDP variation during the period.

3. **Model Diagnostics:**
   To check if our model assumptions were valid, we performed several statistical tests:

   * **Autocorrelation Tests:** Durbin–Watson, Runs Test, and Breusch–Godfrey tests.
   * **Heteroscedasticity Test:** White’s Test.
   * **Normality Test:** Jarque–Bera test.

4. **Corrections Applied:**
   When autocorrelation was detected, we applied corrective methods — **Cochrane–Orcutt**, **Prais–Winsten**, and **First-Difference transformations** — to stabilize the residuals.
   After correction, the **Durbin–Watson statistic approached 2**, indicating the absence of serial correlation.

###  Key Findings

* Investment (GCF) has a **significant positive impact** on GDP growth.
* After statistical corrections, the model satisfied key regression assumptions, making it more **robust and reliable**.
* The study demonstrates how **econometric techniques** ensure that regression results are not misleading due to data issues like autocorrelation or heteroscedasticity.

###  Tools & Techniques

* **Software:** Stata / R
* **Methods:** OLS Regression, Durbin–Watson, Breusch–Godfrey, White’s Test, Cochrane–Orcutt, Prais–Winsten
* **Data Source:** Reserve Bank of India (RBI) Database

###  Learning Outcome

This project strengthened my understanding of **time-series econometrics**, particularly how to detect and fix violations in regression assumptions to produce valid and reliable results — a crucial skill for **data analysis, finance, and machine learning** applications.

---

Would you like me to make it look even more “GitHub-professional” — i.e., with emojis, section dividers, and markdown tables (like a portfolio-style README)?
I can give you that polished version next.
