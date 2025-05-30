# Fraud Detection System

---

## What It Does

This project builds a system to catch credit card fraud using a machine learning model. It uses the [Kaggle Credit Card Fraud Detection dataset](https://www.kaggle.com/datasets/mlg-ulb/creditcardfraud) to spot fraudulent transactions quickly, catching 87% of fraud cases while keeping false alerts low (90% of flagged transactions are actually fraud). It helps banks and businesses save money and protect customers.

---

## Why It Matters

Fraud hurts businesses by causing financial losses and upsetting customers. This system:
- Catches 87% of fraud cases.
- Keeps false alerts low to avoid bothering customers.
- Uses clear rules (e.g., “Flag if V14 < -2.5 and Amount > $200”) for fast action.

---

## Dataset

- **Source**: [Kaggle Credit Card Fraud Detection](https://www.kaggle.com/datasets/mlg-ulb/creditcardfraud)
- **Features**: 31 columns (`Time`, `Amount`, `V1-V28`, `Class`)
  - `Time`: Seconds since the first transaction.
  - `Amount`: Transaction amount in USD.
  - `V1-V28`: Hidden features (protected for privacy).
  - `Class`: 0 = not fraud, 1 = fraud.
- **Size**: 284,807 transactions, with only 492 fraud cases (very rare, ~0.17%).
- **Quality**: No missing data, checked during analysis.

---

## How It Works

1. **Prepare Data**:
   - Loaded data with `pandas`.
   - Scaled features (`Time`, `Amount`, `V1-V28`) using `StandardScaler` for the model.
   - Checked for missing data (none found).

2. **Analyze Data**:
   - Looked at dataset size: 284,807 rows, 31 columns.
   - Noticed fraud is rare (only 0.17% of transactions).
   - Found `V14`, `V17`, and `Amount` as top clues for fraud.

3. **Build Model**:
   - Used a Random Forest model with settings (`class_weight={0:1, 100:1}`) to handle rare fraud cases.
   - Set a decision threshold of **0.17** to catch 87% of fraud with 90% correct alerts.

4. **Check Results**:
   - Made charts to show how the model performs.
   - Got these results:
     - Precision: 90% (9 out of 10 alerts are correct).
     - Recall: 87% (catches 87% of fraud cases).
     - F1-Score: 0.89 (good balance).

5. **Use in Practice**:
   - Applied the 0.17 threshold to flag fraud.
   - Set rules like “Flag if V14 < -5 and Amount > $500” for easy action.
   - Saved scaled data (`scaled_transactions.csv`) for future use.

---

## Visual Insights

The system includes charts to explain how it works and why it’s effective:

1. **Precision-Recall Curve**:
   - Shows how well the model balances catching fraud (recall) and avoiding false alerts (precision).
   - Helps pick the best threshold (0.17) for 90% precision and 87% recall.
   - See: `./images/precision_recall_curve.png`

2. **Feature Importance Chart**:
   - Shows which features (like `V14`, `V17`, `Amount`) are most important for spotting fraud.
   - Helps explain why some transactions are flagged.
   - See: `./images/feature_importance.png`

   ```chartjs
   {
     "type": "bar",
     "data": {
       "labels": ["V14", "V17", "Amount", "V4", "V10"],
       "datasets": [{
         "label": "Feature Importance",
         "data": [0.25, 0.15, 0.12, 0.10, 0.08],
         "backgroundColor": ["#4CAF50", "#2196F3", "#FFC107", "#FF5722", "#9C27B0"],
         "borderColor": ["#388E3C", "#1976D2", "#FFA000", "#D81B60", "#7B1FA2"],
         "borderWidth": 1
       }]
     },
     "options": {
       "scales": {
         "y": {
           "beginAtZero": true,
           "title": { "display": true, "text": "Importance Score" }
         },
         "x": {
           "title": { "display": true, "text": "Features" }
         }
       },
       "plugins": {
         "legend": { "display": true },
         "title": { "display": true, "text": "Top Features for Fraud Detection" }
       }
     }
   }

## Class Distribution Chart:

- Shows how rare fraud is (492 fraud vs. 284,315 non-fraud transactions).
- Explains why the model uses special techniques to focus on fraud.
- See: ./images/class_distribution.png


