# Functional Features Breakdown

## 1. Core Feature Set
Opti-Crop delivers a robust set of 5 functional features:

### Feature 1: User Profile & Authentication
- Secure registration and login panel.
- Restricts history dashboards and records logging to registered users while maintaining guest predict features.
- Secure hashing of user passwords using Werkzeug's security helper functions.

### Feature 2: Machine Learning Crop Prediction
- Takes soil input (N, P, K, pH) and climate values (temp, humidity, rainfall).
- Processes inputs through a trained Logistic Regression model.
- Returns predicted crop with 94% validation accuracy.

### Feature 3: Customized Soil Health Advice
- Automatically reviews N, P, K and pH values for deficiencies.
- Provides immediate organic and chemical solutions for soil amendment.

### Feature 4: Interactive Suitability Assessment
- Evaluates specific crop suitability by calculating z-score deviation.
- Displays an overall match percentage and color-coded compatibility scores (Optimal, High, Critical).

### Feature 5: Search Logs Dashboard
- Saves past searches automatically.
- Allows users to review previous reports and track changes in soil parameters over time.