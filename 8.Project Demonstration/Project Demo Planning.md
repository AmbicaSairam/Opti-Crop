# Project Demo Planning

## 1. Demo Execution Strategy
A successful project demonstration requires careful planning to prevent hardware, software, or network failures.

## 2. Pre-Demo Checklist
- [ ] **Database State:** Clear testing user records and seed initial data. Ensure the default 'admin' user profile is working.
- [ ] **Model Assets:** Verify `model.pkl` and `crop_ranges.pkl` are loaded in memory on startup.
- [ ] **Local Host Setup:** Verify app is running on port 5000 and accessible via local browsers.
- [ ] **Screen Resolution:** Adjust display scaling to 100% to keep glassmorphism styling aligned.
- [ ] **Offline Mode Check:** Verify prediction functionalities work without active internet access.

## 3. Risk Mitigation Table
- **Risk:** ML model fails to load. -> **Mitigation:** Fallback logic displays clear error alerts instead of raising 500 server crashes.
- **Risk:** Network drops during demo. -> **Mitigation:** The application is fully self-contained locally, using local SQLite and pickle files, ensuring 100% functionality offline.
- **Risk:** Inputs validation error. -> **Mitigation:** Frontend validation blocks negative values or characters, prompting user to input numbers.