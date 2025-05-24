# AWS Web Server Load Balancer Setup with SSL - triofrionter.click

This project sets up a high-availability web server infrastructure on AWS using:

- EC2 Instances (Ubuntu, NGINX)
- Application Load Balancer (ALB)
- Target Group with Health Checks
- Domain purchased via Route 53 (`triofrionter.click`)
- Free SSL/TLS Certificate via AWS Certificate Manager (ACM)

---

## 🌐 Architecture Overview

```
Internet
│
[ Route 53 - Domain: triofrionter.click ]
│
[ Application Load Balancer (HTTPS/HTTP) ]
│
[ Target Group ]
├── EC2 Web Server 1 (Nginx, Ubuntu)
└── EC2 Web Server 2 (Nginx, Ubuntu)

```



---

## ⚙️ Setup Steps

### 1. Provision Web Servers

- Launch 2 EC2 instances (`t3.micro`) in the same VPC and region.
- Use Ubuntu 22.04 AMI.
- SSH into each instance and install NGINX:

```bash
sudo apt update
sudo apt install nginx -y

```

---
- Replace default page with a custom HTML welcome page.

  
**📁 Demo Web Page HTML (Web Server 1)**

```

<!DOCTYPE html>
<html>
<head>
  <title>Web Server 1</title>
  <style>
    body {
      background: linear-gradient(to right, #83a4d4, #b6fbff);
      font-family: Arial, sans-serif;
      text-align: center;
      padding-top: 100px;
      color: white;
    }
    h1 {
      font-size: 3rem;
      animation: fadeIn 2s ease-in;
    }
    @keyframes fadeIn {
      from { opacity: 0; }
      to { opacity: 1; }
    }
  </style>
</head>
<body>
  <h1>🚀 Welcome to Web Server 1</h1>
  <p>Deployed on AWS EC2 with NGINX and Load Balancer</p>
</body>
</html>

```

---

**2. Create Target Group**

- Protocol: HTTP
- Port: 80
- Target Type: Instance
- Register both EC2 instances



**3. Create Application Load Balancer**

- Type: Application
- Scheme: Internet-facing
- Listener: Port 80 and 443
- Forward traffic to the target group

  

**4. Request SSL Certificate (ACM)**

- Go to AWS ACM
- Request certificate for
- triofrionter.click
- *.triofrionter.click
- Choose DNS validation
ACM automatically adds validation records if hosted in Route 53



**5. Route 53 Configuration**

- Go to Hosted Zone for triofrionter.click
- Create two A records (alias)
- @ → ALB (root domain)
- www → ALB


**6. Secure with HTTPS**

- Attach ACM certificate to ALB’s HTTPS (443) listener
- Optionally, redirect HTTP to HTTPS

  ---

**✅ Benefits**

- 🆓 Free SSL Certificate (ACM)
- ☁️ Highly Available & Scalable Web Hosting
- 📈 Health Checks for Better Uptime
- 🌍 Secure & Fast DNS with Route 53
- 🔄 Auto-renewing certificates and easy domain management

---


**🧪 Test**

- Visit: https://triofrionter.click      **# use your domain instead of this**
- Visit: https://www.triofrionter.click      **# use your domain instead of this**
- You should see the NGINX welcome page or custom animated HTML page.

---

**📎 Notes**

- Region used: ap-south-1 (Mumbai)
- Instance type: t3.micro (Free Tier eligible)
- Domain & SSL are managed entirely through AWS

  ---

**🛠 Built on**

- AWS EC2, ALB, ACM, Route 53
- Ubuntu + NGINX
- Free Tier friendly ✅
- VPC
