# Observability & Incident Response System

Production-grade monitoring stack simulating real 24/7 NOC (Network Operations Center) environment.

## Live Demo
- **Grafana Dashboard:** http://18.199.150.120:3000 (admin/admin123)
- **Prometheus:** http://18.199.150.120:9090
- **Alertmanager:** http://18.199.150.120:9093

## Architecture

```
┌─────────────────────────────────────────┐
│             AWS EC2 t3.micro            │
│                                         │
│  Node Exporter :9100 ──► Prometheus     │
│  Blackbox Exporter :9115 ──► Prometheus │
│                                         │
│  Prometheus :9090 ──► Grafana :3000     │
│       │                                 │
│       └──► Alertmanager :9093           │
└─────────────────────────────────────────┘
```

## Tech Stack
- **Prometheus** - Metrics collection (15s scrape interval)
- **Grafana** - Visualization and dashboards
- **Alertmanager** - Alert routing and notifications
- **Node Exporter** - System metrics (CPU, RAM, Disk)
- **Blackbox Exporter** - Service availability checks
- **Docker Compose** - Container orchestration
- **AWS EC2** - Cloud hosting

## Monitored Metrics
- CPU Usage (alert threshold: 80%)
- Memory Usage (alert threshold: 80%)
- Disk Usage (alert threshold: 85%)
- Service availability for all stack components

## Alert Rules

| Alert | Condition | Severity |
|-------|-----------|----------|
| HighCPUUsage | CPU > 80% for 2min | Warning |
| HighMemoryUsage | Memory > 80% for 2min | Warning |
| DiskSpaceLow | Disk > 85% for 5min | Critical |
| ServiceDown | Service unreachable for 1min | Critical |

## Quick Start

```bash
git clone https://github.com/IvanLuketic2002/monitoring-stack.git
cd monitoring-stack
docker compose up -d
```

Services will be available at:
- Grafana: http://localhost:3000
- Prometheus: http://localhost:9090
- Alertmanager: http://localhost:9093

## Cost
$0 - Running on AWS EC2 t3.micro
