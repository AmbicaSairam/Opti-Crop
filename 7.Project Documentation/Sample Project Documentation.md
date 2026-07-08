# Sample Project Documentation (Comprehensive Guide)

## 1. System Abstract
Opti-Crop is an advanced machine learning-driven web application designed to optimize crop production. By integrating multi-layered soil parameter models with climatic indicators, the solution resolves crop selection uncertainties, mitigates weather-based crop failure risks, and supports organic and chemical soil correction procedures.

## 2. Functional Architecture
Opti-Crop separates client and server code, keeping logic self-contained. The flask server routes requests to specific endpoints:
- `/predict`: Accepts soil values, runs Logistic Regression model, logs data, and generates soil recommendations.
- `/evaluate_suitability`: Accepts target crop name and checks compatibility against database thresholds.
- `/register` & `/login`: Manages credentials, hashing passwords securely, and establishing local cookies.

## 3. Database Schema Overview
The SQLite database contains 7 relational tables:
- **`users`**: ID, Username, Email, Password, Role.
- **`soil_data`**: Soil ID, N, P, K, Temp, Hum, pH, Rainfall, Season, User ID.
- **`crops`**: Crop ID, Name, Type, Season, Optimal pH, Water Requirement.
- **`datasets`**: Dataset ID, Name, Source, Total Records, Date Updated.
- **`ml_models`**: Model ID, Name, Accuracy, Dataset ID.
- **`predictions`**: Prediction ID, Soil ID, Crop ID, Model ID, Timestamp, Confidence Score.
- **`reports`**: Report ID, Prediction ID, Summary, Soil Advice text.

## 4. Operation and Administration Runbook
- **Model Retraining:** Retrain models when fresh soil readings are added to `Crop_recommendation.csv` by executing `train_model.py`.
- **Database Backup:** Copy `opticrop.db` file to a secure directory.
- **Application Deployment:** The root `render.yaml` specifies deployment on Render, pointing to the `5. Project Development Phase` folder as its root directory.