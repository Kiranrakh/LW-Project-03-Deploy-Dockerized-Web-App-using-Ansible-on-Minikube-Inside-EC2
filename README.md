
# 🚀 Deploy a Dockerized Web App on Minikube using Ansible (EC2-Based)

This project demonstrates how to **automate the deployment** of a simple **Dockerized web application** to a **Kubernetes cluster (Minikube)** using **Ansible**, all set up on a **single Ubuntu EC2 instance**.

---

## 📌 Project Objectives

✅ Manually set up:
- Minikube (Kubernetes) inside an EC2 Ubuntu instance  
- Docker for container image building  
- Ansible to automate image build and deployment  
- Kubernetes Deployment and Service for a web app  

---

## 🧱 Technologies Used

- 🐧 **Ubuntu EC2 Instance** (t2.medium or higher)
- 🐳 **Docker**
- ☸️ **Minikube** (Kubernetes)
- ⚙️ **Ansible**
- 🌐 **Nginx Web Server**

---

## 📁 Project Structure

```

ansible-k8s-app/
├── inventory.ini                # Ansible inventory
├── app/
│   ├── index.html               # Simple static web page
│   └── Dockerfile               # Dockerfile using nginx\:alpine
├── k8s/
│   └── k8s-deploy.yml           # Kubernetes Deployment & Service
└── playbooks/
├── build\_image.yml          # Ansible playbook to build Docker image
└── deploy\_k8s.yml           # Ansible playbook to deploy app on Kubernetes

````

---

## ⚙️ Setup Instructions

### 📍 Step 1: Launch EC2 Instance
- **AMI**: Ubuntu 22.04  
- **Instance Type**: t2.medium or larger  
- **Ports**: Open `22` (SSH) and `30000-32767` (NodePort range)

---

### 📍 Step 2: Install Required Packages

```bash
# Update OS
sudo apt update && sudo apt upgrade -y

# Install Docker
sudo apt install -y docker.io
sudo systemctl enable docker
sudo systemctl start docker
sudo usermod -aG docker $USER
````

👉 **Log out & log back in to apply Docker group changes.**

---

### 📍 Step 3: Install Minikube & kubectl

```bash
# Install kubectl
curl -LO https://dl.k8s.io/release/$(curl -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl
chmod +x kubectl
sudo mv kubectl /usr/local/bin/

# Install Minikube
curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
chmod +x minikube-linux-amd64
sudo mv minikube-linux-amd64 /usr/local/bin/minikube
```

---

### 📍 Step 4: Start Minikube

```bash
minikube start --driver=docker
kubectl get nodes
```

---

### 📍 Step 5: Install Ansible

```bash
sudo apt install -y software-properties-common
sudo add-apt-repository --yes --update ppa:ansible/ansible
sudo apt install -y ansible
ansible --version
```

---

## 🧪 Run the Project

### ▶ Build Docker Image

```bash
ansible-playbook -i inventory.ini playbooks/build_image.yml
```

### ▶ Deploy on Kubernetes

```bash
ansible-playbook -i inventory.ini playbooks/deploy_k8s.yml
```

---

## 🌐 Access the Web App

```bash
minikube service web-service --url
```

Or directly in browser:

```
http://<EC2_PUBLIC_IP>:30007
```

✅ Make sure to allow port `30007` in your EC2 security group.


---

## 🙌 Credits

Built with ❤️ by **Kiran Rakh** as part of real-time DevOps project learning using Ansible, Docker, and Kubernetes.

---

