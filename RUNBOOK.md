🛠️ RUNBOOK – Multi-Tenant WordPress System

📌 Overview

This runbook provides operational steps to deploy, manage, monitor, and troubleshoot the multi-tenant WordPress system.

The system includes:

Nginx (reverse proxy)

WordPress tenants (tenant1, tenant2, tenant3)

MySQL

Prometheus + Grafana (monitoring)

Loki + Promtail (logging)

🚀 1. Starting the System

docker-compose up -d

👉 This will start:

All tenant containers
Database
Monitoring stack
🛑 2. Stopping the System
docker-compose down
🔄 3. Restarting Services
Restart all:
docker-compose restart
Restart specific service:
docker-compose restart nginx
📊 4. Check System Status
docker ps

👉 Verify:

All containers are Up
No container is restarting
📜 5. View Logs
Specific container:
docker logs <container_id>
Follow logs:
docker logs -f <container_id>
🌐 6. Access Services
Service	URL
Tenant1	http://<IP>/tenant1
Tenant2	http://<IP>/tenant2
Tenant3	http://<IP>/tenant3
Grafana	http://<IP>:3000
Prometheus	http://<IP>:9090
🗄️ 7. Database Operations
Access MySQL:
docker exec -it wordpress-multitenant_mysql_1 mysql -uroot -prootpass
Backup Database:
docker exec wordpress-multitenant_mysql_1 \
mysqldump -uroot -prootpass --all-databases > backup.sql
Restore Database:
docker exec -i wordpress-multitenant_mysql_1 \
mysql -uroot -prootpass < backup.sql
📊 8. Monitoring Checks
🔍 Prometheus Targets

Open:

http://<IP>:9090/targets

👉 All targets must be:

UP
📈 Grafana Dashboard
URL: http://<IP>:3000
Login: admin / admin

Verify:

CPU usage visible
Memory usage visible
Tenant containers visible
⚠️ 9. Troubleshooting Guide
❌ Issue: WordPress not loading
Check:
docker logs wordpress-multitenant_tenant1_1
Possible fixes:
DB not ready
Nginx misconfiguration
❌ Issue: Database connection error
Check MySQL logs:
docker logs wordpress-multitenant_mysql_1
Fix:
Verify DB exists
Check credentials
❌ Issue: 404 Not Found
Fix:
Check nginx/default.conf
Restart nginx
docker-compose restart nginx
❌ Issue: Grafana shows "No Data"
Check:
Prometheus targets
Queries
Fix:

Use correct query:

container_memory_usage_bytes{name=~".*tenant.*"}
❌ Issue: Prometheus not starting
Check config:
cat monitoring/prometheus.yml
Restart:
docker-compose restart prometheus
❌ Issue: Container unhealthy
Check:
docker ps
docker logs <container>
🔁 10. Full Reset (Clean State)
docker-compose down -v --remove-orphans
docker system prune -af
docker-compose up -d
📌 11. Health Check Checklist

Before declaring system healthy:

 All containers running
 No restart loops
 Tenants accessible
 Prometheus targets UP
 Grafana dashboards working
 Metrics visible
🔐 12. Operational Best Practices
Monitor container health regularly
Take DB backups daily
Use logs for debugging
Avoid manual changes inside containers
Keep configs version-controlled
🚀 13. Scaling (Optional)

To scale tenants:

docker-compose up -d --scale tenant1=2
📞 14. Escalation

If issue persists:

Check logs (Docker / Prometheus / Grafana)
Restart affected service
Perform full reset if needed
🎯 Conclusion

This runbook ensures:

Smooth operations
Quick troubleshooting
Reliable monitoring
Production-ready handling
