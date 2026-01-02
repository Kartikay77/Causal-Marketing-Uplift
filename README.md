# Causal Marketing Uplift Analysis 🚀

![Python](https://img.shields.io/badge/Python-3.9%2B-blue)
![Library](https://img.shields.io/badge/Library-XGBoost%20%7C%20SHAP%20%7C%20CausalML-orange)
![Status](https://img.shields.io/badge/Status-Complete-green)

## 📌 Executive Summary
This project applies **Causal Inference** and **Uplift Modeling** to optimize marketing campaign ROI. Unlike traditional propensity models that predict *who will buy*, this project predicts **who will buy ONLY if they receive an ad** (Individual Treatment Effect).

By training a **T-Learner (Two-Model Meta-learner)** using XGBoost on the [Kevin Hillstrom E-Mail Analytics Dataset](https://blog.minethatdata.com/2008/03/minethatdata-e-mail-analytics-and-data.html), I identified a "Persuadable" customer segment. Targeting this segment instead of mass-marketing resulted in a **17.2% increase in incremental profit**.

---

## 📊 Key Business Results
By simulating a counterfactual scenario ("What if we didn't email this user?"), the model optimized the targeting strategy:

* **Baseline Strategy (Mass Email):** $186,421.60 Profit
* **AI-Driven Strategy (Targeted):** $218,498.56 Profit
* **Incremental Value Generated:** **+$32,076.96 (+17.2%)** 📈

![Business Impact](https://github.com/Kartikay77/Causal-Marketing-Uplift/blob/main/Media/MC1.png)

---

## 🧠 Technical Methodology
### 1. The T-Learner Approach
Standard A/B testing gives the *average* treatment effect. To find the *individual* effect, I implemented a **T-Learner**:
* **Model 0 (Control):** Trained on users who did *not* receive an email.
* **Model 1 (Treatment):** Trained on users who *did* receive an email.
* **Uplift Calculation:** $\text{Uplift} = P(\text{Buy} | \text{Email}) - P(\text{Buy} | \text{No Email})$

### 2. Strategic Segmentation (The "Persuadables")
The model identified that not all users react positively to marketing. As shown in the histogram below, a significant portion of users have **near-zero or negative lift** (the "Sleeping Dogs" or "Lost Causes").

* **Strategy:** We filter out the middle of the bell curve and target only the tail on the right (High Uplift).

![Uplift Distribution](https://github.com/Kartikay77/Causal-Marketing-Uplift/blob/main/Media/MC3.png)

---

## 🔍 Model Explainability (SHAP)
Using **SHAP (Shapley Additive Explanations)**, I diagnosed *why* certain users were more responsive to the email campaign.

![Feature Importance](https://github.com/Kartikay77/Causal-Marketing-Uplift/blob/main/Media/MC2.png)

**Key Insights:**
1.  **History ($):** High-spending customers (Red dots on the right) are the most responsive. The email serves as a reminder to loyalists.
2.  **Newbies:** New customers (Red dots on the left) had a *negative* reaction to the email. This suggests that aggressive marketing to new sign-ups might be counterproductive (spam fatigue).
3.  **Recency:** Customers who visited recently were more persuadable.

---

## 📈 Model Validation (Qini Curve)
To validate the model's ability to rank users by lift, I plotted the **Qini Curve**. The model (Blue line) consistently outperforms random targeting (Orange line), proving that the Uplift Scores are successfully separating high-impact users from low-impact ones.

![Qini Curve](https://github.com/Kartikay77/Causal-Marketing-Uplift/blob/main/Media/MC4.png)

---

## 🛠️ Installation & Usage

1. **Clone the repository**
   ```bash
   git clone [https://github.com/Kartikay77/Causal-Marketing-Uplift.git](https://github.com/Kartikay77/Causal-Marketing-Uplift.git)
   cd Causal-Marketing-Uplift
   ```
   
2. **Install dependencies**
```
pip install pandas numpy scikit-learn xgboost shap matplotlib
```

3. **Run the Analysis**
Open the Jupyter Notebook (Causal_Analysis.ipynb) to replicate the training and evaluation pipeline.

---
## 📂 File Structure
Causal_Analysis.ipynb: Main notebook containing data loading, T-Learner implementation, and visualization.

Media/: Contains output images (SHAP plots, ROI analysis, etc.).

README.md: Project documentation.

---

## 📜 License
This project is open-source and available under the MIT License.
