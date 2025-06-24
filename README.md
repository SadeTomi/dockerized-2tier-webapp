# Dockerized 2-Tier Web App with GitHub CI/CD (GROUP 6)

**Project Title:** Dockerized 2-Tier Web App with GitHub CI/CD  
**Group:** 6  
**Team Member:** Folasade Coker  
**Platform:** Windows 11 using WSL2 (Ubuntu 20.04)  
**Repository:** https://github.com/SadeTomi/dockerized-2tier-webapp  
**Deployment:** http://13.51.109.236  
**Documentation Folder:** https://drive.google.com/drive/folders/1xIRMZeXDqTf6BAGK5zRVyXuSJ7YYKuQf?usp=sharing

---

## 🧠 Project Summary

This project showcases a Dockerized 2-tier application (frontend and backend) using Flask and HTML/CSS, integrated using Docker Compose, deployed on a Linux VM, and enhanced with GitHub Actions CI/CD workflow.

---

## 🖥️ System Setup

- Windows 11
- WSL2 (Ubuntu 20.04)
- Docker Desktop
- VS Code with Docker, WSL, Dev Containers extensions
- Git

---

## 🛠️ Project Structure

dockerized-2tier-app/
├── backend/
│ ├── app.py
│ └── Dockerfile
├── frontend/
│ ├── index.html
│ └── Dockerfile
├── docker-compose.yml
└── .github/workflows/
└── ci-cd.yml

yaml
Copy
Edit

---

## 🐍 Backend App (Flask)

```python
from flask import Flask
app = Flask(__name__)

@app.route('/')
def home():
    return "Hello from the Backend!"

if __name__ == "__main__":
    app.run(host='0.0.0.0', port=5000)
🎨 Frontend App (HTML)
html
Copy
Edit
<!DOCTYPE html>
<html>
  <head><title>Frontend</title></head>
  <body>
    <h1>Hello from the Frontend!</h1>
  </body>
</html>
🧩 Docker Compose
yaml
Copy
Edit
version: "3.8"
services:
  backend:
    build: ./backend
    ports:
      - "5000:5000"

  frontend:
    build: ./frontend
    ports:
      - "80:80"
Run locally:

bash
Copy
Edit
docker-compose up --build
☁️ Deployment to AWS EC2
bash
Copy
Edit
sudo apt update
sudo apt install docker.io docker-compose -y
git clone https://github.com/SadeTomi/dockerized-2tier-webapp.git
cd dockerized-2tier-webapp
docker-compose up -d
🐳 Docker Hub Push
bash
Copy
Edit
docker tag backend sadetomi/backend:latest
docker tag frontend sadetomi/frontend:latest
docker push sadetomi/backend:latest
docker push sadetomi/frontend:latest
🚀 GitHub Actions CI/CD
yaml
Copy
Edit
name: CI/CD

on:
  push:
    branches: [main]

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      - uses: actions/checkout@v2

      - name: Set up Docker
        uses: docker/setup-buildx-action@v2

      - name: Login to DockerHub
        run: echo "${{ secrets.DOCKER_PASSWORD }}" | docker login -u "${{ secrets.DOCKER_USERNAME }}" --password-stdin

      - name: Build and Push Backend
        run: |
          docker build -t sadetomi/backend:latest ./backend
          docker push sadetomi/backend:latest

      - name: Build and Push Frontend
        run: |
          docker build -t sadetomi/frontend:latest ./frontend
          docker push sadetomi/frontend:latest
😓 Challenges & Solutions
Challenge	What I Did
Docker not working on Windows 10	Switched to Windows 11
VS Code extensions missing	Reinstalled manually
Push failed	Used docker login
EC2 refused connection	Opened ports 22, 80, 5000
GitHub Actions errors	Set DOCKER_USERNAME & DOCKER_PASSWORD as secrets

✅ Conclusion
This capstone gave me hands-on experience with Docker, Linux, GitHub Actions, and deployment pipelines. It also taught me patience, problem-solving, and confidence in building from scratch.

Prepared by Folasade Coker — Group 6 Capstone Project

 `Final README update for capstone submission`







