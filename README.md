# WordPress Multi-Tenant Platform (DevOps Assignment)

## 🚀 Overview
This project implements a multi-tenant WordPress platform using Docker Compose with CI/CD, monitoring, and centralized logging.

> This implementation follows a shared-code, isolated-data multi-tenant architecture aligned with SaaS best practices.

---

## 🧱 Architecture

- Nginx → Reverse proxy
- Multiple WordPress containers (one per tenant)
- Separate MySQL databases per tenant
- Shared wp-content with tenant-specific customization
- Observability:
  - Prometheus → Metrics
  - Loki → Logs
  - Grafana → Visualization

---

## 📁 Project Structure

   - wp-content/
   - tenants/
   - nginx/
   - monitoring/
   - docker-compose.yml# wordpress-multi-tenant
