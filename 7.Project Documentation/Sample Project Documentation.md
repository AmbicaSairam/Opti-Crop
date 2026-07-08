# Opti-Crop: Comprehensive System Documentation & Technical Guide

Opti-Crop is an intelligent decision support platform designed to optimize agricultural yield and soil health. By combining soil chemical analysis with climatic data, Opti-Crop runs a 94%-accurate Logistic Regression machine learning model to recommend suitable crops, and employs K-Means clustering to discover soil-use categories.

---

## 1. System Abstract

Modern agriculture is highly vulnerable to climate variability, unpredictable rainfall, and nutrient depletion. Farmers often select crops based on historical intuition rather than scientific data, leading to suboptimal yields or total crop failure. 

**Opti-Crop** resolves these challenges by bridging data science and agronomy. The platform analyzes seven critical soil and meteorological features:
*   **Macronutrients:** Nitrogen (N), Phosphorous (P), and Potassium (K).
*   **Soil Chemistry:** pH level (pH).
*   **Meteorological Conditions:** Temperature (°C), relative humidity (%), and rainfall (mm).

With these features, Opti-Crop predicts the crop with the highest success rate, evaluates suitability for any specific target crop, and provides targeted organic and chemical soil correction guidelines to help farmers restore soil balance.

---

## 2. Solution Architecture

Opti-Crop is built as a client-server web application using a modern, lightweight technology stack that ensures rapid deployment and high reliability.

### Key Components:
1.  **Flask Web Server (`app.py`):** Coordinates all HTTP requests, authenticates users, manages sessions, queries the database, and loads the machine learning pipeline.
2.  **Database Layer (`database.py`):** Configures and initializes a relational SQLite database (`opticrop.db`) pre-populated with standard agronomic data for 22 different crop categories.
3.  **Machine Learning Engine (`train_model.py`):** Cleans raw dataset inputs, manages outliers, trains the classification model, performs K-Means clustering, and exports serial pickle files (`model.pkl`, `crop_ranges.pkl`, `cluster_insights.pkl`).
4.  **Frontend Templates (`templates/` & `static/`):** Implements a clean, responsive user interface styled with custom CSS (`style.css`) and responsive layout designs.

---

## 3. Database Schema Overview

Opti-Crop utilizes a relational SQLite database structure containing 7 tables. This architecture enforces referential integrity through foreign key constraints.

| Table Name | Primary Key | Columns & Data Types | Relationships & Foreign Keys |
| :--- | :--- | :--- | :--- |
| **`users`** | `user_id` | `username` (TEXT, Unique)<br>`email` (TEXT, Unique)<br>`password` (TEXT, Hashed)<br>`role` (TEXT) | Parent to `soil_data` |
| **`soil_data`** | `soil_id` | `nitrogen` (REAL)<br>`phosphorous` (REAL)<br>`potassium` (REAL)<br>`temperature` (REAL)<br>`humidity` (REAL)<br>`ph` (REAL)<br>`rainfall` (REAL)<br>`season` (TEXT)<br>`user_id` (INTEGER) | Foreign Key: `user_id` references `users(user_id)` |
| **`crops`** | `crop_id` | `crop_name` (TEXT, Unique)<br>`crop_type` (TEXT)<br>`season` (TEXT)<br>`optimal_ph` (REAL)<br>`water_requirement` (REAL) | Parent to `predictions` |
| **`datasets`** | `dataset_id` | `dataset_name` (TEXT)<br>`source` (TEXT)<br>`total_records` (INTEGER)<br>`last_updated` (TEXT) | Parent to `ml_models` |
| **`ml_models`** | `model_id` | `model_name` (TEXT)<br>`accuracy` (REAL)<br>`dataset_id` (INTEGER) | Foreign Key: `dataset_id` references `datasets(dataset_id)` |
| **`predictions`** | `prediction_id` | `soil_id` (INTEGER)<br>`crop_id` (INTEGER)<br>`model_id` (INTEGER)<br>`prediction_date` (TIMESTAMP)<br>`confidence_score` (REAL) | Foreign Keys:<br>- `soil_id` references `soil_data`<br>- `crop_id` references `crops`<br>- `model_id` references `ml_models` |
| **`reports`** | `report_id` | `prediction_id` (INTEGER)<br>`summary` (TEXT)<br>`recommendations` (TEXT) | Foreign Key: `prediction_id` references `predictions` |

---

## 4. API Endpoints Reference

The Flask application exposes a series of RESTful endpoints and page routes:

### Web Page Routes (GET)
*   **`/`**: The platform landing page containing an interactive dashboard overview.
*   **`/about`**: Mission statement, agricultural methodologies, and system developer details.
*   **`/register`**: User registration portal with role-based field forms (Farmer vs. Researcher).
*   **`/login`**: User session authentication screen.
*   **`/findyourcrop`**: Input form interface for entering soil parameters to run crop prediction.
*   **`/suitability`**: Form to assess suitability of a particular target crop against soil metrics.
*   **`/insights`**: Visual dashboards showcasing analytical insights and model metrics.
*   **`/logout`**: Terminates the active session and clears cookies.

### Logic & Processing Routes
*   **`/predict` [POST]**:
    *   **Input:** Soil parameters (N, P, K, pH, temperature, humidity, rainfall).
    *   **Process:** Loads `model.pkl`, executes inference, logs inputs into `soil_data` table, records predictions, generates organic and chemical recommendations, and displays results.
*   **`/evaluate_suitability` [POST]**:
    *   **Input:** Chosen crop name and current soil values.
    *   **Process:** Calculates variance of input values against the historical standard deviations stored in `crop_ranges.pkl` to render a detailed suitability score and advice card.

---

## 5. Machine Learning Methodology

The intelligence of Opti-Crop is driven by rigorous statistical training.

### Data Preprocessing & Outlier Mitigation
Agricultural datasets often contain noise or extreme entries. In the training script `train_model.py`, outliers in the Phosphorous parameter are filtered using the Interquartile Range (IQR) method:
$$IQR = Q_3 - Q_1$$
Any record where Phosphorous falls outside $[Q_1 - 1.5 \times IQR, Q_3 + 1.5 \times IQR]$ is removed to avoid skewing predictions.

### Classification Engine
A **Logistic Regression** classifier is trained using an 80/20 train/test split. The model converges within 200 iterations and achieves an overall validation accuracy of **94%**. The resulting weights and configurations are serialized into `model.pkl` for low-latency web inference.

### Unsupervised Clustering
To discover structural groupings among crop environments, **K-Means Clustering** (K=4) is trained on the preprocessed soil parameters. The optimal number of clusters is verified via the WCSS Elbow Method, plotted and saved under `static/images/elbow_graph.png`. The group associations are saved to `cluster_insights.pkl` to offer cross-crop recommendations.

---

## 6. Administration & Runbook

### Local Development Setup

To configure and execute the Opti-Crop server locally, execute the following steps in sequence:

1.  **Clone code repository:**
    ```bash
    git clone https://github.com/AmbicaSairam/Opti-Crop.git
    cd Opti-Crop
    ```
2.  **Set up virtual environment:**
    ```bash
    python -m venv venv
    # Windows:
    .\venv\Scripts\activate
    # macOS/Linux:
    source venv/bin/activate
    ```
3.  **Install dependencies:**
    ```bash
    pip install -r "5. Project Development Phase/requirements.txt"
    ```
4.  **Initialize Database:**
    ```bash
    python "5. Project Development Phase/database.py"
    ```
5.  **Train Models & Generate Visuals:**
    ```bash
    python "5. Project Development Phase/train_model.py"
    ```
6.  **Launch Web Server:**
    ```bash
    python "5. Project Development Phase/app.py"
    ```
    Open `http://127.0.0.1:5000/` in your browser.

### Cloud Deployment
The repository includes a `render.yaml` configuration for seamless deployment on Render. The configuration launches the application using Gunicorn:
```yaml
services:
  - type: web
    name: opticrop
    env: python
    buildCommand: pip install -r "5. Project Development Phase/requirements.txt" && python "5. Project Development Phase/database.py" && python "5. Project Development Phase/train_model.py"
    startCommand: gunicorn "5. Project Development Phase.app:app"
```
Ensure that `opticrop.db` is maintained in persistent storage if state retention across restarts is required.
