Here is your **final, polished, submission-ready `README.md`** 👇
(You can directly paste this into your repo)

---

# 🚀 Multi-Tenant WordPress with Observability (Docker-Based)

## 📌 Overview

This project implements a **production-grade multi-tenant WordPress architecture** using Docker.
Multiple tenants share infrastructure while maintaining **data isolation** and **independent environments**.

It also includes a complete **observability stack** using Prometheus and Grafana.

---

## 🏗️ Architecture

```
User → Nginx (Reverse Proxy) → WordPress Tenants → MySQL
                                  ↓
                   cAdvisor + Node Exporter
                                  ↓
                             Prometheus
                                  ↓
                              Grafana
```

---

## ⚙️ Features

* ✅ Multi-tenant WordPress (tenant1, tenant2, tenant3)
* ✅ Database isolation per tenant
* ✅ Containerized deployment using Docker Compose
* ✅ Reverse proxy routing via Nginx
* ✅ Monitoring with Prometheus + Grafana
* ✅ Logging with Loki + Promtail
* ✅ Production-ready structure

---

## 📂 Project Structure

```
wordpress-multitenant/
│
├── docker-compose.yml
├── .env
├── nginx/
│   └── default.conf
├── mysql-init/
│   └── init.sql
├── monitoring/
│   ├── prometheus.yml
│   └── promtail.yml
├── tenants/
│   ├── tenant1/
│   ├── tenant2/
│   └── tenant3/
```

---

## 🚀 Deployment

### 1. Clone the Repository

```bash
git clone <your-repo-url>
cd wordpress-multitenant
```

---

### 2. Setup Environment Variables

```bash
cp .env.example .env
```

Update `.env`:

```env
MYSQL_ROOT_PASSWORD=rootpass
TENANT1_DB=tenant1_db
TENANT2_DB=tenant2_db
TENANT3_DB=tenant3_db
```

---

### 3. Start the Application

```bash
docker-compose up -d
```

---

## 🌐 Access URLs

| Service    | URL                 |
| ---------- | ------------------- |
| Tenant 1   | http://<IP>/tenant1 |
| Tenant 2   | http://<IP>/tenant2 |
| Tenant 3   | http://<IP>/tenant3 |
| Grafana    | http://<IP>:3000    |
| Prometheus | http://<IP>:9090    |

---

## 🧠 Multi-Tenant Strategy

* Each tenant runs in a **separate container**
* Each tenant uses a **separate MySQL database**
* Each tenant has its own **wp-content directory**
* Shared infrastructure for **cost optimization**

---

## 📊 Monitoring Setup

### Tools Used:

* **Prometheus** → Metrics collection
* **Grafana** → Visualization
* **Node Exporter** → System metrics
* **cAdvisor** → Container metrics

---

### Grafana Dashboards

Import dashboards:

* Node Exporter → `1860`
* Docker Monitoring → `193`

---

### Key Prometheus Queries

```promql
# CPU Usage per Tenant
rate(container_cpu_usage_seconds_total{name=~".*tenant.*"}[5m])

# Memory Usage per Tenant
container_memory_usage_bytes{name=~".*tenant.*"}

# Running Containers
count(container_last_seen{name=~".*tenant.*"})
```

---

## 🐞 Common Issues & Fixes

| Issue                | Solution                       |
| -------------------- | ------------------------------ |
| 404 Not Found        | Fix Nginx routing              |
| DB Connection Error  | Verify MySQL init scripts      |
| Grafana shows N/A    | Fix Prometheus queries         |
| Containers unhealthy | Check logs using `docker logs` |

---

## 🔄 Useful Commands

```bash
# Start
docker-compose up -d

# Stop
docker-compose down

# Restart
docker-compose restart

# Logs
docker logs <container_id>

# Clean reset
docker-compose down -v
docker system prune -af
```

---

## 🔒 Security Considerations

* Use `.env` for secrets (do not commit)
* Restrict exposed ports
* Use strong passwords
* Enable HTTPS in production
* Keep containers updated

---

## 🚀 Future Enhancements

* Domain-based routing (tenant1.example.com)
* SSL with Let's Encrypt
* Auto tenant onboarding
* CI/CD pipeline integration
* Kubernetes deployment

---

## 🎯 Outcome

This project demonstrates:

* Multi-tenant architecture
* Container orchestration
* Observability (metrics + logs)
* Production-grade DevOps practices


<img width="1360" height="768" alt="Screenshot (42)" src="https://github.com/user-attachments/assets/d070b43f-bfd9-45b3-b0d4-381b68f5bb63" />
