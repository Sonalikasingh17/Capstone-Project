# 🚀 Capstone Project – End-to-End MLOps Pipeline

![Python](https://img.shields.io/badge/Python-3.10-blue?logo=python)
![MLflow](https://img.shields.io/badge/MLflow-Tracking-orange?logo=mlflow)
![AWS](https://img.shields.io/badge/AWS-EKS%20|%20S3%20|%20ECR-orange?logo=amazonaws)
![Docker](https://img.shields.io/badge/Docker-Containerization-blue?logo=docker)
![GitHub Actions](https://img.shields.io/badge/CI/CD-GitHub%20Actions-2088FF?logo=githubactions)
![Prometheus](https://img.shields.io/badge/Prometheus-Monitoring-red?logo=prometheus)
![Grafana](https://img.shields.io/badge/Grafana-Dashboard-orange?logo=grafana)

> 🧠 A complete **Machine Learning Operations (MLOps)** pipeline — from local development to cloud deployment and monitoring.

---

## 🧩 Project Overview

This Capstone Project automates the **end-to-end ML lifecycle** using modern DevOps and MLOps tools.  
You’ll learn how to build, version, deploy, and monitor a machine learning model in production 🌐⚙️

**Key Features:**
- 🧮 Data pipeline: Ingestion → Preprocessing → Feature Engineering  
- 🤖 Model lifecycle: Training → Evaluation → Registration  
- 📊 Experiment tracking using **MLflow (Dagshub)**  
- 💾 Dataset versioning using **DVC + AWS S3**  
- 🐳 Containerization using **Docker**  
- 🔁 Deployment automation using **GitHub Actions + AWS ECR + EKS**  
- 📈 Monitoring using **Prometheus + Grafana**

---

## 🏗️ Project Structure


Capstone-Project/
│
├── src/
│ ├── logger/
│ ├── data_ingestion.py
│ ├── data_preprocessing.py
│ ├── feature_engineering.py
│ ├── model_building.py
│ ├── model_evaluation.py
│ ├── register_model.py
│
├── flask_app/
│ ├── app.py
│ ├── templates/
│ ├── static/
│
├── tests/
├── scripts/
├── params.yaml
├── dvc.yaml
├── requirements.txt
├── Dockerfile
├── .github/workflows/ci.yaml
└── README.md

---

## ⚙️ Tech Stack

| Category | Tools |
|-----------|--------|
| 🧠 **ML Frameworks** | Scikit-learn, Pandas, NumPy |
| 💾 **Versioning & Tracking** | DVC, MLflow, Dagshub |
| 🐳 **Containerization** | Docker |
| ☁️ **Cloud Services** | AWS S3, ECR, EKS |
| 🔁 **Automation** | GitHub Actions |
| 📊 **Monitoring** | Prometheus, Grafana |
| 🧰 **Environment** | Conda, Python 3.10 |

---

<details>
<summary>🧰 <b>1️⃣ Project Setup</b></summary>

```bash
# Create virtual environment
conda create -n atlas python=3.10
conda activate atlas

# Install template
pip install cookiecutter
cookiecutter -c v1 https://github.com/drivendata/cookiecutter-data-science

# Rename and initialize repo
mv src.models src.model
git add .
git commit -m "Initial setup"
git push
```

<details> 

<details> <summary>📊 <b>2️⃣ Setup MLflow Tracking (Dagshub)</b></summary>

Go to Dagshub Dashboard

Create a new repo and connect your GitHub repository

Copy the MLflow tracking URL & integrate it into your notebooks

Install dependencies
```bash
pip install dagshub mlflow
```

<details> 
