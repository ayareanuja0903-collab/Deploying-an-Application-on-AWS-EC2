# 🚀 Node.js Application Deployment on AWS EC2

This project demonstrates how to deploy a Node.js application on an AWS EC2 instance and make it live for users.

---

## 📌 Project Overview

- Deployed a Node.js app on AWS EC2
- Configured Ubuntu server
- Installed required dependencies (Node.js, npm, PM2, Nginx)
- Application is live and accessible via public IP

---

## 🛠️ Tech Stack

- Node.js
- Express.js
- AWS EC2
- Nginx (Reverse Proxy)
- PM2 (Process Manager)
- Ubuntu Linux

---
## Project overview 
-Deploying an Application on AWS EC2.pdf

## ⚙️ Deployment Steps

### 1. Launch EC2 Instance

- Choose Ubuntu Server
- Allow ports: 22 (SSH), 80 (HTTP), 443 (HTTPS)

---

### 2. Connect to EC2

```bash
ssh -i your-key.pem ubuntu@65.0.181.122
```

---

### 3. Install Node.js & npm

```bash
sudo apt update
sudo apt install -y nodejs npm
```

---

### 4. Install PM2

```bash
sudo npm install -g pm2
```

---

### 5. Clone Repository

```bash
git clone https://github.com/ayareanuja0903-collab/Node_application
cd Node_application
npm install
```

---

### 6. Start Application

```bash
pm2 start server.js
pm2 save
pm2 startup
```

---

### 7. Install & Configure Nginx

```bash
sudo apt install nginx -y
```

Edit config file:

```bash
sudo nano /etc/nginx/sites-available/default
```

Add:

```nginx
server {
    listen 80;
    server_name _;

    location / {
        proxy_pass http://localhost:3000;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection 'upgrade';
        proxy_set_header Host $host;
        proxy_cache_bypass $http_upgrade;
    }
}
```

Restart Nginx:

```bash
sudo systemctl restart nginx
```

---

## 🌐 Access Application

```
http://65.0.181.122:3000/
```

---

## 📈 Production Enhancements

- Use Elastic Load Balancer (ELB)
- Enable Auto Scaling
- Add Domain using Route 53
- Secure with SSL (Let's Encrypt)

---

## 📊 Monitoring

```bash
pm2 status
pm2 logs
pm2 monit
```

---

## 🧠 Key Learnings

- AWS EC2 deployment
- Process management using PM2
- Reverse proxy setup with Nginx
- Production-ready setup 
