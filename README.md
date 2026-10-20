# 🚀 Axion Intelligence Platform
![image alt](https://github.com/saba-codes/Axion-Intelligence-Platform/blob/9926f080516bb780a417f19812b9a4071e7e4e76/Axion-Architecture.jpeg)

An industrial telemetry monitoring platform built using **Microsoft Azure, Docker, Kubernetes, React, Python, and PostgreSQL**. The project simulates refinery sensor data, ingests and stores telemetry, provides APIs to query the data, and presents it through a web-based dashboard.

## 📌 Project Overview

The Axion Intelligence Platform demonstrates how multiple containerized services can work together to collect, process, store, and visualize simulated industrial telemetry data.

The platform includes a data simulator, an ingestion service, a PostgreSQL database, a telemetry query service, and a React-based frontend. The services are deployed on Azure Kubernetes Service (AKS) and exposed through NGINX Ingress and custom DNS records.

## 🛠️ Technologies Used

- **Cloud:** Microsoft Azure
- **Container Orchestration:** Azure Kubernetes Service (AKS)
- **Containerization:** Docker
- **Container Registry:** Azure Container Registry (ACR)
- **Frontend:** React
- **Backend:** Python, FastAPI
- **Database:** PostgreSQL
- **Database Management:** pgAdmin
- **Ingress and Web Server:** NGINX Ingress Controller, NGINX
- **DNS and Domain Management:** Hostinger
- **Deployment Configuration:** Kubernetes YAML manifests

## 🏗️ Architecture

```text
             Simulated Industrial Devices
                        |
                        v
                Axion Data Simulator
                        |
                        v
                 Ingestion Service
                        |
                        v
                  PostgreSQL DB
                        |
                        v
               Telemetry Query Service
                        |
                        v
                    Axion UI
                 (React + NGINX)
                        |
                        v
                  Web Dashboard
```

**Request routing:** External browser requests reach the NGINX Ingress Controller through the configured domain. Ingress routes requests to the appropriate Kubernetes Service, which forwards traffic to the corresponding application Pod.

## 📂 Project Structure

```text
Axion-Project/
│
├── axion-database-schema/
│   └── Database schema and SQL scripts
│
├── axion-ingestion-service/
│   ├── Dockerfile
│   └── Kubernetes manifests
│
├── axion-data-simulator/
│   ├── Dockerfile
│   └── Kubernetes manifests
│
├── axion-telemetry-query-service/
│   ├── Dockerfile
│   └── Kubernetes manifests
│
└── axion-ui/
    ├── Dockerfile
    ├── nginx.conf
    └── Kubernetes manifests
```

## ⚙️ Key Components

### 1. Axion Data Simulator

- Simulates industrial sensor telemetry.
- Generates data such as temperature, vibration, current, device ID, device type, and refinery region.
- Sends telemetry data to the ingestion API.

### 2. Axion Ingestion Service

- Built using Python and FastAPI.
- Receives telemetry data from the simulator.
- Connects to PostgreSQL and stores incoming records.

### 3. PostgreSQL Database

- Stores telemetry records.
- Uses UUIDs as unique record identifiers.
- Includes timestamps and sensor measurements.
- Uses database indexes to support queries by device and timestamp.

### 4. Telemetry Query Service

- Built using Python and FastAPI.
- Queries telemetry data stored in PostgreSQL.
- Exposes data to the frontend through API endpoints.

### 5. Axion UI

- Built using React.
- Provides a web interface for telemetry monitoring.
- Packaged using a multi-stage Docker build.
- Uses NGINX to serve the production frontend files.

## ☁️ Azure and Kubernetes Deployment

The application components are deployed to **Azure Kubernetes Service (AKS)**.

Key deployment activities include:

1. Building Docker images for the application components.
2. Pushing images to Azure Container Registry.
3. Deploying workloads using Kubernetes Deployment manifests.
4. Creating ClusterIP Services for internal communication.
5. Configuring NGINX Ingress rules to route domain requests.
6. Configuring Hostinger DNS A records to point the domains to the Ingress Controller's external IP.
7. Testing services locally using Kubernetes port forwarding and validating the application through the browser.

The Kubernetes resources are deployed in the `saba` namespace.

## 🌐 Domain Configuration

The following domains were configured for the project:

| Component | Domain |
|---|---|
| Axion UI | `dabbewale.shop` |
| pgAdmin | `pgadminui.dabbewale.shop` |
| Ingestion Service | `ingestionservice.dabbewale.shop` |
| Telemetry Query Service | `query-service.dabbewale.shop` |

Hostinger DNS A records route the domains to the NGINX Ingress Controller's external IP address.

## 🔄 End-to-End Data Flow

1. The simulator generates simulated industrial telemetry.
2. The simulator sends the data to the Ingestion Service.
3. The Ingestion Service stores the telemetry in PostgreSQL.
4. The Telemetry Query Service retrieves stored telemetry through API requests.
5. The Axion UI communicates with the Query Service to retrieve data for display.
6. Users access the dashboard through the main domain.

## 🚀 Useful Kubernetes Commands

Check workloads:

```bash
kubectl get pods -n saba
kubectl get deployments -n saba
kubectl get services -n saba
kubectl get ingress -n saba
```

Apply a Deployment manifest:

```bash
kubectl apply -f <deployment-file>.yaml -n saba
```

Apply a Service manifest:

```bash
kubectl apply -f <service-file>.yaml -n saba
```

Apply an Ingress manifest:

```bash
kubectl apply -f <ingress-file>.yaml -n saba
```

Test the Axion UI locally using port forwarding:

```bash
kubectl port-forward svc/axion-ui-svc 7878:80 -n saba
```

Then open `http://localhost:7878` in your browser.

## 🎯 Project Objectives

- Demonstrate containerization using Docker.
- Deploy and manage multiple application components using Kubernetes.
- Use Azure AKS and ACR for cloud deployment and image management.
- Implement service-to-service communication within Kubernetes.
- Configure NGINX Ingress and custom DNS for external access.
- Build an end-to-end telemetry pipeline from data simulation to dashboard visualization.

## 📚 Key Learnings

- Docker image building and publishing.
- Kubernetes Deployments, Services, and Ingress.
- Azure Kubernetes Service and Azure Container Registry.
- PostgreSQL configuration and database connectivity.
- FastAPI-based ingestion and query services.
- React production builds and NGINX web serving.
- DNS configuration and domain-based application access.
- Troubleshooting deployments and validating application connectivity.

## 👨‍💻 Author

**Saba**

GitHub: [saba-codes](https://github.com/saba-codes)

---

⭐ If you find this project interesting, feel free to explore the repository and share your feedback.
