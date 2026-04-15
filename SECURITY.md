# 🔐 SECURITY – Multi-Tenant WordPress System

---

## 📌 Overview

This document outlines the **security practices, risks, and recommendations** for the multi-tenant WordPress architecture.

The system includes:
- Nginx (reverse proxy)
- WordPress tenants
- MySQL database
- Prometheus + Grafana (monitoring)
- Loki + Promtail (logging)

---

# 🔑 1. Secrets Management

- Store sensitive data in `.env` file
- Do NOT commit `.env` to version control
- Use strong passwords for:
  - MySQL root
  - WordPress admin
  - Grafana login

### Recommended:
- Use secret managers (AWS Secrets Manager / Vault)

---

# 🌐 2. Network Security

- Expose only required ports:
  - 80 (Nginx)
  - 3000 (Grafana)
  - 9090 (Prometheus)
- Restrict access using firewall rules (Security Groups)

### Recommended:
- Allow SSH (22) only from trusted IPs
- Block direct access to MySQL port (3306)

---

# 🔒 3. Database Security

- Avoid using root user in production
- Create dedicated DB users per tenant
- Use strong passwords
- Enable regular backups

### Risks:
- Shared MySQL instance → potential lateral access

---

# 🧱 4. Container Security

- Use official Docker images only
- Keep images updated
- Avoid running containers as root (if possible)

### Recommended:
- Scan images using:
```bash
docker scan <image>
```

---

# 🔐 5. WordPress Security

- Keep WordPress core updated
- Remove unused plugins/themes
- Use strong admin credentials
- Limit login attempts

### Recommended:
- Install security plugins (Wordfence, iThemes Security)

---

# 📊 6. Monitoring & Access Control

- Protect Grafana with strong credentials
- Disable anonymous access
- Restrict Prometheus access (internal use only)

---

# 📜 7. Logging Security

- Logs collected via Loki + Promtail
- Ensure logs do NOT expose:
  - Passwords
  - Tokens
  - Sensitive data

---

# 🔐 8. CI/CD Security

- Run static code analysis (PHPCS, linting)
- Avoid committing secrets in code
- Use secure GitHub Actions workflows

---

# ⚠️ 9. Known Risks

| Risk | Description |
|-----|------------|
| Shared Infrastructure | Tenants share same MySQL instance |
| Path-based Routing | Less secure than domain-based routing |
| Root DB Access | Using root user for all tenants |

---

# 🚀 10. Recommended Improvements

- Use HTTPS (Let's Encrypt)
- Use domain-based routing (tenant1.example.com)
- Implement RBAC (Role-Based Access Control)
- Use managed database (AWS RDS)
- Add Web Application Firewall (WAF)
- Use Kubernetes for isolation

---

# 🧠 11. Backup & Recovery

### Backup:
```bash
docker exec mysql mysqldump -uroot -prootpass --all-databases > backup.sql
```

### Restore:
```bash
docker exec -i mysql mysql -uroot -prootpass < backup.sql
```

---

# 🚨 12. Incident Response

If a security issue occurs:

1. Identify affected service
2. Check logs (Docker / Loki)
3. Stop affected container if needed
4. Restore from backup
5. Rotate credentials

---

# 🔍 13. Audit Checklist

- [ ] Strong passwords configured
- [ ] No secrets in Git repo
- [ ] Only required ports exposed
- [ ] Monitoring secured
- [ ] Regular backups enabled

---

# 🎯 Conclusion

This system follows **basic to intermediate security practices** suitable for a production-ready setup.

Further enhancements can improve:
- Isolation
- Access control
- Compliance readiness
