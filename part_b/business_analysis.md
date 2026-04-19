# Business Case Analysis: Promotion Effectiveness at a Fashion Retail Chain

---

# B1. Problem Formulation

## (a) Machine Learning Problem Formulation

* **Target Variable:**
  `items_sold` (number of items sold per store per month)

* **Input Features:**

  * Store attributes: store_size, location_type, footfall, competition_density
  * Promotion details: promotion_type
  * Time features: month, festival, weekend
  * Customer behavior: basket size, visit frequency

* **Type of ML Problem:**
  This is a **Supervised Regression Problem** because we are predicting a continuous numerical value (items sold).

* **Justification:**
  The output is numeric and depends on multiple input variables, making regression the appropriate approach.

---

## (b) Why Items Sold is Better than Revenue

* Revenue can be influenced by:

  * Pricing strategies
  * Discounts
  * Product mix

* Items sold directly reflects:

  * Customer demand
  * Promotion effectiveness

* **Broader Principle:**
  The target variable should directly align with the **business objective**.
  Choosing the wrong target can lead to misleading model outcomes.

---

## (c) Alternative Modelling Strategy

Instead of a single global model:

* Use **segmented models** based on:

  * Location type (urban, semi-urban, rural)
  * Store size

* Or use a **hierarchical model (multi-level model)**

* **Justification:**
  Different stores respond differently to promotions, so segmentation improves prediction accuracy and personalization.

---

# B2. Data and EDA Strategy

## (a) Data Joining and Dataset Design

* **Tables:**

  * Transactions
  * Store attributes
  * Promotion details
  * Calendar

* **Joining Strategy:**

  * Join on `store_id` and `date`

* **Final Dataset Grain:**

  * One row = **one store per month**

* **Aggregations:**

  * Total items_sold per month
  * Average basket size
  * Total visits
  * Promotion applied in that month

---

## (b) Exploratory Data Analysis (EDA)

1. **Promotion vs Items Sold (Bar Chart)**

   * Identify which promotions perform best
   * Helps in feature importance understanding

2. **Time Trends (Line Plot)**

   * Monthly sales trends
   * Detect seasonality (festivals, holidays)

3. **Correlation Heatmap**

   * Identify relationships between features
   * Helps remove redundant variables

4. **Box Plot (Location Type vs Sales)**

   * Compare performance across regions
   * Helps decide segmentation strategy

---

## (c) Handling Imbalanced Promotions

* Issue: 80% data has no promotion

* Impact:

  * Model may ignore promotion effects
  * Bias toward “no promotion” prediction

* Solution:

  * Use **resampling techniques**
  * Add **promotion indicator features**
  * Ensure balanced representation during training

---

# B3. Model Evaluation and Deployment

## (a) Train-Test Split & Metrics

* **Split Strategy:**

  * Use **time-based split**
  * Train: first 2.5 years
  * Test: last 6 months

* **Why not random split?**

  * Causes **data leakage**
  * Future data may influence training

* **Evaluation Metrics:**

  * **RMSE:** Penalizes large errors
  * **MAE:** Average prediction error
  * **R² Score:** Model explanatory power

* **Interpretation:**

  * Lower RMSE/MAE = better predictions
  * Higher R² = better model fit

---

## (b) Explaining Model Decisions

* Use **feature importance from model**

* Analyze:

  * Month (seasonality)
  * Promotion type impact
  * Store-specific factors

* Example:

  * December → festivals → Loyalty Points work better
  * March → lower demand → Discounts perform better

* **Communication:**

  * Use simple visuals (charts)
  * Explain insights in business terms

---

## (c) Deployment Strategy

### 1. Model Saving

* Save model using:

  * `joblib` or `pickle`

### 2. Monthly Prediction Pipeline

* New data collected monthly
* Apply same preprocessing pipeline
* Generate predictions for all 50 stores

### 3. Automation

* Schedule predictions at start of each month
* Use scripts or workflow tools

### 4. Monitoring

* Track:

  * Prediction error (RMSE, MAE)
  * Data drift (changes in input patterns)
  * Business KPIs (actual vs predicted sales)

### 5. Retraining

* Retrain model when:

  * Performance drops
  * New trends emerge

---

# Conclusion

A well-designed ML system using proper feature engineering, segmentation, and time-aware evaluation can significantly improve promotion effectiveness and business decision-making.
