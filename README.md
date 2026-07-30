# 🎓 Student Performance Prediction — End-to-End MLOps Project

[![Python](https://img.shields.io/badge/Python-3.8+-3776AB?style=for-the-badge&logo=python&logoColor=white)](https://www.python.org/)
[![Docker](https://img.shields.io/badge/Docker-Enabled-2496ED?style=for-the-badge&logo=docker&logoColor=white)](https://www.docker.com/)
[![AWS](https://img.shields.io/badge/AWS-EC2%20%7C%20ECR%20%7C%20ElasticBeanstalk-232F3E?style=for-the-badge&logo=amazon-aws&logoColor=white)](https://aws.amazon.com/)

> An end-to-end Machine Learning project designed to predict student academic performance. Built alongside the Udemy course *“Complete MLOps Bootcamp With 10+ End To End ML Projects”*, featuring custom architectural improvements and automated deployment pipelines.

---

## 📌 Disclaimer & Modifications

This repository is based on the original course curriculum. However, **all modifications, architectural adjustments, and custom deployment procedures** documented here are the sole responsibility of the author.

---

## 🏗️ Project Architecture & Features

- **Data Pipeline:** Modular ingestion, transformation, and model training/evaluation pipelines.
- **Model Training:** Automated selection and hyperparameter tuning for performance prediction.
- **Web Interface:** Interactive Flask application (`app.py`) for real-time predictions.
- **Containerization:** Fully dockerized application ready for CI/CD integrations.

---

## 🚀 Deployment Guide (AWS)

This project supports **two distinct strategies** for deploying to Amazon Web Services:

### Option 1: AWS Elastic Beanstalk
*Ideal for quick, managed web app deployment.*

1. **Configuration:** Ensure `.ebextensions` configuration files are present in your root directory.
2. **WSGI Setup:** **Important:** Elastic Beanstalk looks for `application.py` by default. Delete `app.py` to avoid deployment errors.
3. **Deployment:** Deploy the application via the AWS Console.

> ⚠️ **Hardware & Storage Notes:**  
> - **Instance Type:** Configured on a **`t3.small`** instance.
> - **Storage:** Requires increasing the default root volume size to **16–20 GB** to accommodate model dependencies, temporary build files, and Docker/Python environment caches.


### Option 2: Docker + AWS ECR + AWS EC2 (Automated via GitHub Actions)
*Ideal for full container control and automated CI/CD deployment.*

This option uses a **GitHub Actions workflow** to handle the entire deployment pipeline automatically on every push to the `main` branch:

1. **Continuous Integration & Delivery (CI/CD):** 
   - Automatically builds the Docker image upon pushing code.
   - Authenticates with AWS and pushes the new image to **AWS Elastic Container Registry (ECR)**.
   *(Note: `.ebextensions` configurations are ignored inside the Docker image).*
2. **Automated Deployment:** 
   - Connects to the **AWS EC2** instance, pulls the latest image from ECR, and spins up the updated container.

> ⚠️ **Hardware Recommendation:**  
> The EC2 setup was successfully tested on a **`c7i.flex.large`** instance (Compute Optimized, 16 GB RAM) to handle data transformations and inference efficiently.

---

## 🔮 Roadmap & Future Improvements

- [ ] **Automated Model Registry:** Automatically upload and version trained model artifacts directly to an **AWS S3** bucket.
- [ ] **Monitoring:** Set up basic drift detection and logging for production inference requests.

---

