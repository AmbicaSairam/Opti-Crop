# Brainstorming & Idea Prioritization

## 1. Project Background
Opti-Crop is a machine-learning powered agricultural decision support system designed to recommend optimal crops based on soil nutrient levels and climatic conditions. The project aims to empower farmers, agricultural researchers, and extension workers with data-driven insights to maximize yields and promote sustainable farming practices.

## 2. Brainstorming Session Insights
During the initial project scoping phase, the team brainstormed multiple approaches to address the crop recommendation problem:
- **Idea A: Rule-Based Expert System:** A database of hardcoded rules based on agricultural textbooks. (Discarded: Lacks adaptability to climate variations, too rigid for complex non-linear parameters).
- **Idea B: ML-Based Classifier using Soil and Weather Data:** Using a Logistic Regression or Random Forest model trained on historical soil datasets. (Selected: Highly accurate, handles multi-dimensional parameters, generalizable across regions).
- **Idea C: IoT Real-Time Monitoring and Irrigation Integration:** Real-time sensor inputs automatically controlling farm irrigation systems. (Deferred to Future Scope: High upfront hardware costs for smallholder farmers).

## 3. Idea Prioritization Matrix
To select the core feature set, the ideas were evaluated against key criteria:

| Feature / Idea | Feasibility (1-5) | Impact (1-5) | Cost (1-5) | Overall Score | Decision |
| :--- | :---: | :---: | :---: | :---: | :---: |
| ML-Based Crop Prediction | 5 | 5 | 5 (Low Cost) | 15 / 15 | **Priority 1 (Core)** |
| Soil Suitability Matrix | 4 | 4 | 5 (Low Cost) | 13 / 15 | **Priority 1 (Core)** |
| User Profile & Search History | 5 | 3 | 4 (Low Cost) | 12 / 15 | **Priority 2 (Extension)** |
| IoT Soil Sensor Integration | 2 | 5 | 2 (High Cost) | 9 / 15 | **Priority 3 (Future)** |
| Automated Fertilizer Ordering | 3 | 3 | 3 (Moderate) | 9 / 15 | **Priority 3 (Future)** |

## 4. Prioritized Project Focus
For the primary release, we chose to focus on building a robust, locally deployable web application that implements the ML-Based Crop Prediction and Soil Suitability Matrix, supported by User Authentication and Search Logging for a personalized farmer dashboard.