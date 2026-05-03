# **Stroke-Prediction-ML-Model-Comparison**

A practical comparison of three classification algorithms—Logistic Regression, Random Forest, and K-Nearest Neighbors—on a real medical dataset. This work goes beyond accuracy metrics to consider what actually matters in production: latency, interpretability, and recall trade-offs.

<img width="590" height="324" alt="تنزيل (8)" src="https://github.com/user-attachments/assets/6ffe938a-e06b-433c-849f-f75af4872a23" /> <img width="590" height="324" alt="تنزيل (7)" src="https://github.com/user-attachments/assets/be734380-5cfa-4973-918e-396f0ea61fde" />


----------------------------------------------------------------------------------------------------------------------------
___________________________________________________________________________________________________________________________

## Why This Matters
Not all correct predictions are created equal. In medical contexts, missing a stroke (false negative) is catastrophically worse than flagging a patient who doesn't have one (false positive). This notebook builds models that reflect that reality instead of just chasing accuracy numbers.

## What's Inside

###1. Data & Problem Setup

Stroke prediction dataset with real class imbalance (~5% positive cases)
Standard preprocessing pipeline: imputation, scaling, one-hot encoding
Train/test split with stratification to preserve class balance

###2. Model Comparison

Logistic Regression: Fast, interpretable baseline
K-Nearest Neighbors: Distance-based approach with tunable k
Random Forest: Ensemble method balancing accuracy and interpretability

###3. Production Considerations ⭐

#### Feature Importance
Random Forest reveals which risk factors actually matter. Not all features contribute equally to stroke prediction—this analysis shows the dominant signals.
<img width="796" height="547" alt="تنزيل (6)" src="https://github.com/user-attachments/assets/a34ac6df-c0df-45e1-8c75-f2edfb830098" />

#### Why Macro-Recall?
The standard accuracy metric is useless here. A naive model that predicts "no stroke" for everyone achieves ~95% accuracy while catching zero actual strokes.
Macro-recall = (recall_stroke + recall_no_stroke) / 2
It treats both classes equally, forcing the model to catch strokes without being rewarded for simply predicting the majority class. In medical contexts, this is closer to the real cost structure: missing diagnoses matters.

## The Recommendation
### **Random Forest wins**.
It's not the fastest (LogReg is), but it's fast enough (15-20ms is workable in clinical systems). It achieves the highest recall on actual stroke cases—which is the point. You get feature importance for validation. The model size is acceptable.
LogReg is interpretable but sacrifices recall. KNN is too slow and stores the entire dataset. Random Forest is the pragmatic choice.

----------------------------------------------------------------------------------------------------------------------------
___________________________________________________________________________________________________________________________
## Key Takeaway
The best model isn't always the most accurate—it's the one that works in your actual constraints (latency, interpretability, recall for the right class). This notebook shows why that distinction matters.

Dataset: Stroke prediction dataset (healthcare domain)
Tools: scikit-learn, pandas, matplotlib
