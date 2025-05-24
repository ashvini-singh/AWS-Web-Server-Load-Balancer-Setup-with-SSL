**📄 Documentation: High Availability Web Architecture with Load Balancer**

✅ Overview

This setup creates a high-availability, scalable web application using AWS infrastructure. It includes

- Two Ubuntu-based EC2 instances acting as web servers.
- NGINX installed for serving static web content.
- An Application Load Balancer (ALB) for distributing incoming traffic.
- A custom domain (triofrontier.click) hosted in Route 53.
- Deployed in a Virtual Private Cloud (VPC) with public subnets.

---

**🧩 Architecture Components**

| Component                     | Description                                                        |
| ----------------------------- | ------------------------------------------------------------------ |
| **VPC**                       | Isolated network environment where all resources are deployed.     |
| **Subnets**                   | Two public subnets in different Availability Zones for redundancy. |
| **EC2 Instances**             | Two `t2.micro` Ubuntu servers with NGINX installed.                |
| **NGINX**                     | Web server installed to serve HTML pages.                          |
| **Target Group**              | Group that includes both EC2 instances for load balancing.         |
| **Application Load Balancer** | Distributes traffic across web servers.                            |
| **Route 53 Domain**           | DNS service to map domain to the ALB.                              |


---

**⚙️ How It Works**

1. A user accesses http://www.triofrontier.click.    **# User your domain instead of this**
2. The request is routed by Route 53 to the Application Load Balancer (ALB).
3. ALB checks the health of targets in the target group.
4. ALB forwards the request to one of the EC2 web servers in a round-robin manner.
5. NGINX on the EC2 instance responds with a simple HTML message.
6. The user sees the output from either Web Server 1 or 2.

---

**📌 Why This Setup is Needed**

- **Redundancy:** If one instance fails, the other can still serve traffic.
- **Load Balancing:** Evenly distributes traffic to avoid overloading a single server.
- **Scalability:** Easily add more instances behind the load balancer.
- **Custom Domain:** Adds professionalism and makes the site easier to access.
- **Security:** With VPC and security groups, network access is tightly controlled.

---

**🌟 Benefits**


| Feature                      | Benefit                                                                      |
| ---------------------------- | ---------------------------------------------------------------------------- |
| **High Availability**        | Application remains available even if one server fails.                      |
| **Scalable Architecture**    | Easily add/remove servers based on demand.                                   |
| **Fault Tolerance**          | Deploying servers in multiple Availability Zones ensures better uptime.      |
| **Cost-Effective**           | Uses Free Tier eligible resources (t2.micro/t3.micro).                       |
| **Improved User Experience** | With load balancer and custom domain.                                        |
| **Easy Monitoring**          | ALB health checks automatically detect and reroute from unhealthy instances. |

---


**📎 Future Enhancements (Optional)**

- Add **SSL Certificate** using ACM for HTTPS.
- Use **Auto Scaling Group** for dynamic scaling.
- Install and configure **monitoring tools** like CloudWatch or third-party logging.
- Deploy an **application** instead of static HTML.
