# Observability and Operation Tools
## Observability
- Used to understand the behavior, health, and performance of your apps

### Monitoring
- Collects metrics to help you understand how your apps are performing
- Dashboards and charts
- Agents are recommended to monitor VMs
- Works together with Cloud Logging
- Good for alerts

### Logging
- Central repo for log data from multiple sources
- Types of Logs:
    - Audit: who did what, where, when
    - Access Transparency: actions taken by Google
    - Agent: logs from agents installed on VMs

### Error Reporting
- Real time error monitoring and alerting

### Trace
- Collects latency data from App Engine, HTTP(S) Load Balancers, and Applications

## Operations
- used to build, operate and manage apps

### Profiler
- Continuously gathers CPU and memory usage info from applications
- Agents need to be installed (works with GCE, GKE, GAE, and non-GCP environments)