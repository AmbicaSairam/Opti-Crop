# Project Executable Files & Installation Guide

## 1. System Requirements
- **Python:** Python 3.9 or higher (Python 3.11 recommended).
- **RAM:** Minimum 2GB.
- **Disk Space:** 500MB free.

## 2. Local Installation Steps

### Step 1: Clone the Repository
Clone the Opti-Crop code repository locally.
```bash
git clone https://github.com/AmbicaSairam/Opti-Crop.git
cd Opti-Crop
```

### Step 2: Set Up Virtual Environment
Create a virtual environment to manage dependencies:
```bash
python -m venv venv
# Activate on Windows:
.\venv\Scripts\activate
# Activate on Linux/macOS:
source venv/bin/activate
```

### Step 3: Install Required Libraries
```bash
pip install -r "5. Project Development Phase/requirements.txt"
```

### Step 4: Initialize the SQLite Database
```bash
python "5. Project Development Phase/database.py"
```

### Step 5: Execute Model Training & Assets Generation
```bash
python "5. Project Development Phase/train_model.py"
```

### Step 6: Start the Application Server
```bash
python "5. Project Development Phase/app.py"
```
The application will launch on `http://127.0.0.1:5000/`.