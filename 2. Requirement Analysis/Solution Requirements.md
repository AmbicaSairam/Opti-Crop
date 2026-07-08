# Solution Requirements

## 1. Functional Requirements (FR)
- **FR-1: User Authentication:** Users must be able to register, log in, and log out. Passwords must be hashed using secure cryptographical hashes before database insertion.
- **FR-2: Crop Predictor:** The system must accept inputs for Nitrogen (N), Phosphorous (P), Potassium (K), Temperature, Humidity, pH, and Rainfall, and output the recommended crop.
- **FR-3: Suitability Evaluator:** Users must be able to select a specific crop and input soil data to receive a detailed suitability score and metric-by-metric compatibility analysis.
- **FR-4: Historical Logs:** Registered users must have a persistent dashboard showing their past crop predictions and generated soil reports.
- **FR-5: Database Logging:** All predictions must be logged in SQLite tables (`soil_data`, `predictions`, `reports`) linking back to the user ID.

## 2. Non-Functional Requirements (NFR)
- **NFR-1: Prediction Speed:** The ML model inference and DB transaction time combined must not exceed 1.0 second per request.
- **NFR-2: Accuracy:** The core recommendation model must achieve an overall classification accuracy of at least 94% on test datasets.
- **NFR-3: Device Responsiveness:** The web interface must display correctly on both mobile browsers (Chrome/Safari on iOS and Android) and desktop screens.
- **NFR-4: Security:** SQL injection must be prevented via parameterized queries. User sessions must be secured using cryptographically signed cookies.
- **NFR-5: Local Deployability:** The system must not rely on external cloud APIs for core prediction, allowing offline operations in remote agricultural offices.