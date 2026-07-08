# Performance & Model Validation Testing

## 1. Model Validation (ML Performance)
The core Logistic Regression classifier was validated using an 80/20 train-test split on 2,200 dataset records. Outliers in the phosphorous parameter were cleaned using Interquartile Range (IQR) filtering.

### Validation Performance Summary:
- **Overall Model Accuracy:** 94.09%
- **Precision (Average):** 94.20%
- **Recall (Average):** 94.09%
- **F1-Score (Average):** 94.11%

### Classification Report snippet:
- Rice: Precision 1.00, Recall 0.95
- Maize: Precision 0.89, Recall 0.93
- Chickpea: Precision 1.00, Recall 1.00
- Pomegranate: Precision 1.00, Recall 0.98

## 2. Application Performance & Load Testing
The local Flask application was tested under multiple loads:
- **Average Page Load Time:** < 80ms (Home screen, About, and Login).
- **Prediction Request Processing Time:** < 120ms (Includes database write transactions and ML inference).
- **Concurrent Users Handling:** Verified stable handling of up to 50 concurrent simulation requests locally without database thread locking.