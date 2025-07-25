# Project Setup and Monitoring

This project provides a Docker-based environment with Prometheus and Grafana for monitoring, plus an Ubuntu container for running stress tests.

## Project Structure

```
project/
│
├── docker-compose.yml         # Docker Compose configuration for all services
├── prometheus/
│   └── prometheus.yml         # Prometheus configuration file
├── ubuntu/
│   └── Dockerfile             # Dockerfile for custom Ubuntu container
└── grafana/
    ├── provisioning/
    │   ├── dashboards/        # Provisioned dashboards (auto-loaded)
    │   │   └── node-exporter-dashboard.json
    │   └── datasources/       # Provisioned datasources (auto-loaded)
    │       └── datasource.yaml
    └── ...                    # Persistent Grafana data
```

## Getting Started

### 1. Build and Start All Services

```sh
# Build images and start containers in the background
docker-compose up --build -d
```

### 2. Access the Ubuntu Container

```sh
# SSH into the Ubuntu container (default password: password)
ssh root@localhost -p 2222
# Password: root
```

### 3. Access Monitoring Tools in Your Browser

- **Prometheus:** [http://localhost:9090](http://localhost:9090)
- **Grafana:** [http://localhost:3000](http://localhost:3000)
  - Default credentials: `admin` / `admin` 

#### Grafana Setup (Automated)
- **Prometheus datasource** is automatically configured at `http://localhost:9090`.
- **Node Exporter Full dashboard** (ID 1860) is automatically imported and available on first login.
- All dashboards and datasources are persisted in the `grafana/` directory and survive container restarts.

##### Customizing Dashboards and Datasources
- To add or update dashboards, place JSON files in `grafana/provisioning/dashboards/`.
- To add or update datasources, edit `grafana/provisioning/datasources/datasource.yaml`.
- Changes require a Grafana container restart to take effect.

## Running Stress Tests

Inside the Ubuntu container:

```sh
# Update package lists and install stress-ng and ping
sudo apt update
sudo apt install -y stress-ng iputils-ping

# Run a CPU stress test (74% load, 60 seconds, show metrics)
stress-ng --cpu 0 --cpu-load 74 --timeout 60s --metrics-brief
```

---

Feel free to modify the configuration files to suit your needs. For more information, see the official documentation for [Prometheus](https://prometheus.io/docs/introduction/overview/) and [Grafana](https://grafana.com/docs/).

