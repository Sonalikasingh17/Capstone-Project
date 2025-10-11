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
```
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
```
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

</details>
<details> <summary>🧰 <b>1️⃣ Project Setup</b></summary>

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

</details> 

<details> <summary>📊 <b>2️⃣ Setup MLflow Tracking (Dagshub)</b></summary>

- Go to Dagshub Dashboard
- Create a new repo and connect your GitHub repository
- Copy the MLflow tracking URL & integrate it into your notebooks
- Install dependencies

```bash
pip install dagshub mlflow
```
</details> 

<details> <summary>🗃️ <b>3️⃣ Setup Data Version Control (DVC)</b></summary>
  
```bash
dvc init
mkdir local_s3
dvc remote add -d mylocal local_s3
```

Add these files:
- dvc.yaml
- params.yaml

Then run:

```bash
dvc repro
dvc status
git add .
git commit -m "DVC pipeline ready"
git push
```

</details>
<details> <summary>☁️ <b>4️⃣ Connect AWS S3 Storage</b></summary>
  
```bash
pip install dvc[s3] awscli
aws configure
dvc remote add -d myremote s3://<your-bucket-name>
dvc push
```

</details>
<details> <summary>🌐 <b>5️⃣ Flask App Setup</b></summary>

```bash
cd flask_app
pip install flask
python app.py
```

Your local app will be available at

```cpp
👉 http://127.0.0.1:5000
```

</details>
<details> <summary>🤖 <b>6️⃣ CI/CD Pipeline Setup</b></summary>

- Add .github/workflows/ci.yaml
- Generate a token from Dagshub → Settings → Tokens
- Save token in GitHub → Secrets → CAPSTONE_TEST
- Add testing directories:

```bash
tests/
scripts/
```

</details>
<details> <summary>🐳 <b>7️⃣ Dockerize the App</b></summary>

```bash
cd flask_app
pip install pipreqs
pipreqs . --force
cd ..
docker build -t capstone-app:latest .
docker run -p 8888:5000 -e CAPSTONE_TEST=<your_token> capstone-app:latest
```

</details>
<details> <summary>☁️ <b>8️⃣ AWS EKS Deployment</b></summary>

```bash
eksctl create cluster --name flask-app-cluster --region us-east-1 \
--nodegroup-name flask-app-nodes --node-type t3.small \
--nodes 1 --nodes-min 1 --nodes-max 1 --managed
```

Then check:

```bash
aws eks list-clusters
kubectl get nodes
kubectl get svc flask-app-service
```

Visit your deployed app via:

```cpp
http://<external-ip>:5000
```

</details>
<details> <summary>📈 <b>9️⃣ Monitoring with Prometheus & Grafana</b></summary>
  
🧭 Prometheus (Port 9090)

```bash
wget https://github.com/prometheus/prometheus/releases/download/v2.46.0/prometheus-2.46.0.linux-amd64.tar.gz
tar -xvzf prometheus-2.46.0.linux-amd64.tar.gz
sudo mv prometheus /etc/prometheus
sudo mv /etc/prometheus/prometheus /usr/local/bin/
```

Update config file:

```yaml
scrape_configs:
  - job_name: "flask-app"
    static_configs:
      - targets: ["<external-ip>:5000"]
```

Run:

```bash
/usr/local/bin/prometheus --config.file=/etc/prometheus/prometheus.yml
```

📊 Grafana (Port 3000)

```bash
wget https://dl.grafana.com/oss/release/grafana_10.1.5_amd64.deb
sudo apt install ./grafana_10.1.5_amd64.deb -y
sudo systemctl start grafana-server
sudo systemctl enable grafana-server
```

Access at:

```cpp
👉 http://<ec2-public-ip>:3000 (admin / admin)
```
</details>


---


## 🧹 AWS Resource Cleanup

Clean up resources after testing to avoid extra AWS costs 💸

```bash
# Delete Kubernetes deployment and service
kubectl delete deployment flask-app
kubectl delete service flask-app-service
kubectl delete secret capstone-secret

# Delete EKS Cluster
eksctl delete cluster --name flask-app-cluster --region us-east-1

# Verify deletion
eksctl get cluster --region us-east-1

```
Also:
- 🧹 Delete ECR images
- 🧺 Remove S3 buckets
- 📦 Check CloudFormation and delete remaining stacks if needed

---


## 🧩 Key Concepts

| Concept              | Description                            |
| -------------------- | -------------------------------------- |
| **MLflow**           | Track experiments, metrics, and models |
| **DVC**              | Data & model version control           |
| **Docker**           | Package and run app in containers      |
| **EKS (Kubernetes)** | Deploy containerized app on AWS        |
| **Prometheus**       | Collect and store metrics              |
| **Grafana**          | Visualize app health dashboards        |

---

## 🏁 Final Results

- ✅ Fully automated end-to-end ML pipeline
- ✅ Deployed on AWS with Docker & EKS
- ✅ CI/CD integration via GitHub Actions
- ✅ Real-time monitoring using Prometheus & Grafana

---

## 👩‍💻 Author
**Sonalika Singh**
- 📫[Medium Blogs](https://medium.com/@singhsonalika5)
- 🌐 [GitHub Profile](https://github.com/Sonalikasingh17)

---

## 🌟 Star This Repository

If you find this project helpful, please give it a ⭐ on [GitHub](https://github.com/Sonalikasingh17/Capstone-Project)
 — it keeps me motivated! 💪

---

## 🧭 Next Steps

 - Add unit testing for each pipeline stage
 - Integrate Kubernetes auto-scaling
 - Enhance Grafana dashboard visualizations

 ---

“Build once, automate forever.” 💡

— *Sonalika Singh*
