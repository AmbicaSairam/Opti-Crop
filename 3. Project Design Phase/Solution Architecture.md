# Solution Architecture

## 1. Three-Tier Architectural Layout
Opti-Crop is designed as a classic 3-tier web application, securing modularity, ease of testing, and clean separation of concerns.

```
+--------------------------------------------------------+
|                   PRESENTATION LAYER                   |
|  - HTML5, CSS3 (Glassmorphism), Vanilla JavaScript    |
|  - Bootstrap (Responsive Layout Grid)                  |
+---------------------------|----------------------------+
                            | HTTP Request / JSON response
+---------------------------v----------------------------+
|                    APPLICATION LAYER                   |
|  - Flask Application Server (app.py)                   |
|  - ML Inference Logic (scikit-learn)                   |
|  - Session & Session Validation Controller             |
+---------------------------|----------------------------+
                            | SQL Queries / Pickle Reads
+---------------------------v----------------------------+
|                       DATA LAYER                       |
|  - SQLite Database File (opticrop.db)                  |
|  - Serialized Model & Range Assets (.pkl files)        |
+--------------------------------------------------------+
```

## 2. Database Schema Relationships
The SQLite database (`opticrop.db`) maintains a structured schema with 7 interrelated tables to enable logging:
- **`users`:** Holds user profiles, hashed passwords, and access roles (Farmer vs Researcher).
- **`soil_data`:** Stores input soil properties, linked to the `users` table via foreign keys.
- **`crops`:** Stores optimal ph, season, water requirements, and crop categorization.
- **`datasets` & `ml_models`:** Stores model tracking information (model accuracy and datasets used).
- **`predictions`:** Links `soil_data`, `crops`, and `ml_models` with a timestamp and confidence score.
- **`reports`:** Stores generated summaries and chemical/organic recommendation text.