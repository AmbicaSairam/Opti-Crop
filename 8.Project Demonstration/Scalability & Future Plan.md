# Scalability & Future Plan

## 1. Architectural Scaling
To scale the application from a local research prototype to a regional service, the following advancements are planned:
- **Migration to Cloud Database:** Migrate local SQLite3 file engine to a hosted PostgreSQL database (e.g. Supabase, Amazon RDS) to support high concurrent writes.
- **Microservices Refactoring:** Separate the Flask app into two services:
  1. Frontend Client UI (built in React/NextJS).
  2. Backend Prediction API (FastAPI) executing Python ML inference.

## 2. Feature Additions Roadmap
- **Phase 2: IoT Sensor Integration:** Connect wireless NPK, pH, and soil moisture sensors to ESP32 microcontrollers. ESP32 will post parameters directly to the Opti-Crop API, updating recommendations automatically.
- **Phase 3: Real-Time Weather Integration:** Integrate OpenWeather API. Instead of prompting users for rainfall and temperature inputs, the app will read the user's GPS coordinates and fetch live weather variables.
- **Phase 4: Plant Disease Diagnosis (CNNs):** Introduce computer vision model allowing farmers to photograph crop leaves and receive pest diagnostics.