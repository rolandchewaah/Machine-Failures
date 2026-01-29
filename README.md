# 🏭 Machine Failure Prediction Pipeline (Databricks CE)

An end-to-end machine learning pipeline for **predicting machine failures** using the **Medallion Architecture** on **Databricks Community Edition**.

---

## 🧱 Architecture

Implements a **Bronze → Silver → Gold** Delta Lake pipeline with a downstream ML model:

Raw CSV
↓
Bronze Layer (Raw Ingest)
↓
Silver Layer (Cleaned & Labeled)
↓
Gold Layer (Feature Engineered)
↓
ML: Random Forest for Failure Prediction


---

## 📁 Folder Structure

machine_failure_pipeline/
├── notebooks/
│ └── machine_failure_pipeline_databricks.ipynb # Complete notebook
├── data/
│ └── machine_failure_data.csv # Input data (uploaded to /FileStore/)
├── delta/
│ ├── bronze/
│ ├── silver/
│ └── gold/ # Delta tables created in pipeline
├── models/
│ └── (Optional) Exported trained models
└── README.md


---

## 🚀 Features

- Built with **PySpark** on Databricks CE
- Stores data using **Delta Lake** format
- Rolling window statistics for sensor features
- Trains **Random Forest classifier** using Spark MLlib
- Evaluates model using AUC metric

---

## 🛠️ How to Use

### 1. Upload Dataset
- Go to **Data → Upload File**
- Upload `machine_failure_data.csv` to `/FileStore/`

### 2. Import & Run Notebook
- Open `notebooks/machine_failure_pipeline_databricks.ipynb` in Databricks
- Run each cell sequentially:
  - Bronze: Load and store raw data
  - Silver: Clean + derive labels
  - Gold: Feature engineering
  - ML: Train model and evaluate

---

## 📊 ML Model Info

- **Model**: RandomForestClassifier
- **Features**:
  - temperature, pressure, vibration, rpm
  - Rolling averages and deltas
- **Label**: `is_failure` (derived from `error_code`)
- **Metric**: AUC (Area Under Curve)

---

## 📌 Notes for Databricks CE

- Delta files are saved under `/delta/` in **DBFS**
- Model inference is batch-only (CE doesn't support model serving)
- No job scheduling — run notebooks manually or use Jobs (basic UI)

---

## ✅ Future Improvements

- Add MLflow model tracking
- Serve predictions via FastAPI or Databricks Model Serving (Pro version)
- Integrate with Airflow or other orchestrators (Pro version)

---

## 🧑‍💻 Author

Rolland Cruz