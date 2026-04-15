# 🚀 Multi-Tenant WordPress with Observability (Docker-based)

## 📌 Overview
This project implements a **multi-tenant WordPress architecture** using Docker, where multiple tenants share infrastructure but maintain isolated data.

It includes:
- Multi-tenant WordPress deployment
- Nginx reverse proxy routing
- MySQL with separate databases
- Monitoring using Prometheus + Grafana
- Logging using Loki + Promtail

---

## 🏗️ Architecture


User → Nginx → Tenant Containers → MySQL
↓
cAdvisor + Node Exporter
↓
Prometheus
↓
Grafana


---

## ⚙️ Features

- ✅ Multi-tenant WordPress (tenant1, tenant2, tenant3)
- ✅ Database isolation per tenant
- ✅ Containerized deployment (Docker Compose)
- ✅ Reverse proxy routing via Nginx
- ✅ Monitoring (Prometheus + Grafana)
- ✅ Logging (Loki + Promtail)
- ✅ Production-ready structure

---

## 📂 Project Structure


wordpress-multitenant/
│
├── docker-compose.yml
├── .env
├── nginx/
│ └── default.conf
├── mysql-init/
│ └── init.sql
├── monitoring/
│ ├── prometheus.yml
│ └── promtail.yml
├── tenants/
│ ├── tenant1/
│ ├── tenant2/
│ └── tenant3/


---

## 🚀 Deployment

### 1. Clone repo
```bash
git clone <repo-url>
cd wordpress-multitenant

2. Setup environment
cp .env.example .env

Edit:

MYSQL_ROOT_PASSWORD=rootpass
TENANT1_DB=tenant1_db
TENANT2_DB=tenant2_db
TENANT3_DB=tenant3_db

3. Start services

docker-compose up -d

🌐 Access

Service	URL
Tenant1	http://<IP>/tenant1
Tenant2	http://<IP>/tenant2
Tenant3	http://<IP>/tenant3
Grafana	http://<IP>:3000
Prometheus	http://<IP>:9090

📊 Monitoring

Grafana Dashboards
Node Exporter Dashboard (ID: 1860)
Docker Monitoring Dashboard (ID: 193)
Prometheus Queries

# CPU per tenant
rate(container_cpu_usage_seconds_total{name=~".*tenant.*"}[5m])

# Memory per tenant
container_memory_usage_bytes{name=~".*tenant.*"}

🧠 Multi-Tenant Strategy
Separate containers per tenant
Separate databases per tenant
Shared infrastructure (cost optimized)

🐞 Common Issues
Issue	Fix
404 error	Fix Nginx config
DB error	Check MySQL init
Grafana N/A	Fix Prometheus queries
