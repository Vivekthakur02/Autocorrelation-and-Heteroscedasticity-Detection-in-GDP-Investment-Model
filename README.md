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

### ⚙️ Model Framework

To represent the relationship, a simple linear regression model was used:

GDP_t = β_0 + β_1*GCF_t + ε_t


Where:

* ( β_0 ) = intercept, showing baseline GDP when investment is zero
* ( β_1 ) = slope coefficient, representing how much GDP changes for every unit increase in investment
* ( ε_t ) = random error term capturing factors not included in the model


### 📈 Exploratory Insights

Initial plots showed both GDP and GCF trending upward over the years, indicating long-term economic growth. However, such trends can also introduce potential issues like **autocorrelation** or **non-stationarity** in time-series data — which were later tested and corrected in subsequent steps of this project.

---
