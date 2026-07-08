# Demonstration of Proposed Features

## 1. Purpose of Demonstration
This document acts as a step-by-step testing script for conducting the live application demonstration, ensuring all key functional features are showcased correctly.

## 2. Test Case Script

### Scenario 1: Basic Crop Recommendation
- **User Action:** Navigate to the "Find Your Crop" tab. Enter: N=90, P=42, K=43, Temp=20.8, Hum=82.0, pH=6.5, Rain=202.9. Click "Recommend".
- **Expected System Output:** The system returns **RICE** in large, clear typography. Water Requirement: "High". Fertilizer Advice: "Soil nutrient levels are highly optimal. Maintain soil health."
- **Verification:** Confirm database logs show a new prediction logged under `predictions` with confidence score.

### Scenario 2: Soil Corrective Advice
- **User Action:** Input N=20, P=15, K=15, Temp=28.0, Hum=70.0, pH=5.0, Rain=80.0. Click "Recommend".
- **Expected System Output:** The system predicts **MUNG-BEAN** or similar crop. Highlights pH deficiency (5.0 < 5.5) and N, P, K shortages. Advice output: "Soil is acidic. Application of agricultural lime (calcium carbonate) can help raise pH. Nitrogen level is low. Add nitrogen-rich organic compost or urea."

### Scenario 3: Suitability Matrix
- **User Action:** Navigate to "Suitability Matrix". Select target crop: "coffee". Input typical dry conditions: Rain=80. Click "Evaluate".
- **Expected System Output:** Display overall match percentage (e.g. 65%). Identifies rainfall as deficient (Coffee requires higher rain), showing a critical red alert.