# DevOps Website — End-to-End CI/CD and Kubernetes Monitoring

An end-to-end DevOps project demonstrating automated application deployment using GitHub, Jenkins, Docker, Kubernetes, Prometheus, and Grafana.

This project focuses on automating the deployment process, managing application workloads in Kubernetes, and monitoring CPU and memory utilization through Grafana dashboards.

## Project Overview

The DevOps Website project demonstrates how a web application can be deployed and monitored using a containerized deployment workflow.

The application is deployed to a local Kubernetes cluster using Minikube. Jenkins automates the deployment pipeline, while Prometheus collects monitoring metrics and Grafana visualizes application resource utilization.

### Project Objectives

- Automate application deployment using Jenkins.
- Use Docker to containerize the application.
- Deploy and manage application workloads using Kubernetes.
- Implement Kubernetes deployment verification.
- Monitor application CPU and memory utilization.
- Visualize monitoring metrics using Grafana.
- Understand the integration of CI/CD and container orchestration.

## Technologies and Tools Used

| Tool | Purpose |
|---|---|
| Git | Version control |
| GitHub | Source code repository |
| Jenkins | CI/CD pipeline automation |
| Docker | Application containerization |
| Kubernetes | Container orchestration |
| Minikube | Local Kubernetes cluster |
| kubectl | Kubernetes resource management |
| Prometheus | Metrics collection and monitoring |
| Grafana | Monitoring dashboards and visualization |

## Architecture

The project follows this deployment workflow:

```text
        Developer
            |
            v
         GitHub
            |
            v
         Jenkins
            |
            v
      Build Docker Image
            |
            v
        Minikube
            |
            v
        Kubernetes
            |
            v
     Application Pods
            |
            v
       Prometheus
            |
            v
         Grafana
            |
            v
     CPU & Memory Metrics
```


## CI/CD Workflow

### 1. Source Code Management — GitHub

The application source code and deployment configuration files are maintained in GitHub.

GitHub provides version control and acts as the source repository for the Jenkins pipeline.

### 2. CI/CD Automation — Jenkins

Jenkins executes the deployment pipeline using a Jenkinsfile.

The pipeline performs the following stages:

1. Checkout SCM
2. Checkout source code
3. Build Docker image
4. Check Minikube access
5. Load Docker image into Minikube
6. Deploy application to Kubernetes
7. Restart Kubernetes deployment
8. Verify deployment
9. Execute post-build actions

The pipeline automates the deployment process and reduces manual intervention.

### 3. Containerization — Docker

Docker packages the application and its required runtime into a container image.

The image is used by Kubernetes to run the application inside the cluster.

### 4. Kubernetes Deployment — Minikube

Minikube provides the local Kubernetes environment.

The application is deployed using Kubernetes Deployments and Pods.

The project uses the following deployments:

- `devops-app-myapp` — Main website deployment.
- `devops-flow` — DevOps Flow application deployment with two replicas.

Kubernetes manages the application containers and maintains the desired number of replicas.

The application can be accessed locally through the configured service and port forwarding.

### 5. Deployment Verification

After deployment, Jenkins verifies the Kubernetes deployment.

The following command can be used to check the application pods:

```bash
kubectl get pods
```

To check the deployments:

```bash
kubectl get deployments
```

To check the services:

```bash
kubectl get svc
```

The expected result is that the application pods are running and ready.

## Monitoring and Observability

Monitoring is implemented using Prometheus and Grafana.

### Prometheus

Prometheus collects metrics from the Kubernetes environment and monitoring components.

It is used to:

- Collect monitoring metrics.
- Query application resource utilization.
- Monitor Kubernetes infrastructure components.
- Provide metrics for Grafana dashboards.

Example Prometheus query for CPU utilization:

```promql
rate(container_cpu_usage_seconds_total{
  namespace="default",
  pod=~"devops-app-myapp.*",
  container!="",
  image!=""
}[5m])
```

Example Prometheus query for memory utilization:

```promql
container_memory_working_set_bytes{
  namespace="default",
  pod=~"devops-app-myapp.*",
  container!="",
  image!=""
}
```

### Grafana

Grafana is used to visualize the metrics collected by Prometheus.

A custom Grafana dashboard was created with two panels:

**1. CPU Usage**
- Displays CPU utilization of the website pod.
- Shows resource usage over time.
- Helps observe changes in CPU consumption.

**2. Memory Usage**
- Displays memory consumption of the website pod.
- Shows memory utilization over time.
- Helps observe changes in application memory usage.

The dashboard provides a visual representation of application resource utilization.

## Kubernetes Monitoring Stack

The monitoring components are deployed in the `monitoring` namespace.

The monitoring stack includes:

- Prometheus
- Grafana
- Alertmanager
- Prometheus Operator
- Kube State Metrics
- Node Exporter

These components support monitoring and visualization of Kubernetes infrastructure metrics.

## Project Implementation

The project was implemented in the following sequence:

1. Created and maintained the application source code in GitHub.
2. Configured Jenkins to retrieve the source code.
3. Created a Jenkins pipeline using a Jenkinsfile.
4. Built the application Docker image.
5. Configured Minikube as the Kubernetes environment.
6. Loaded the Docker image into Minikube.
7. Deployed the application using Kubernetes.
8. Verified the application pods and deployment status.
9. Installed the Prometheus and Grafana monitoring stack.
10. Configured Prometheus as the Grafana data source.
11. Created a custom Grafana dashboard for CPU and memory monitoring.
12. Verified the deployment and monitoring workflow.

## Project Results

The project successfully demonstrates:

- Automated deployment through Jenkins.
- Docker-based application containerization.
- Kubernetes application deployment and management.
- Running application pods and deployment verification.
- Prometheus metrics collection.
- Grafana visualization of CPU and memory utilization.
- Integration of CI/CD, container orchestration, and monitoring.

## Screenshots

### 1. Application Frontend

The deployed DevOps Website displaying the end-to-end deployment workflow.

<img width="1221" height="686" alt="image" src="https://github.com/user-attachments/assets/53bf45e1-71fd-4d8c-b942-5ac0d50072a9" />

### 2. Jenkins Pipeline

The Jenkins pipeline showing the successful execution of the deployment stages.
<img width="1482" height="278" alt="image" src="https://github.com/user-attachments/assets/36bd1669-b31e-4506-b75d-d65106d39e38" />

### 3. Kubernetes Deployment

The Kubernetes pods running in the Minikube cluster.
<img width="722" height="105" alt="Screenshot 2026-11-03 171626" src="https://github.com/user-attachments/assets/9e308801-88d2-4030-b8bf-273733edbe3d" />


### 4. Grafana Monitoring Dashboard

The custom Grafana dashboard displaying CPU and memory utilization of the website pod.
<img width="1391" height="397" alt="Screenshot 2026-11-03 171101" src="https://github.com/user-attachments/assets/6fc77d3e-58df-4492-b002-f5452f9995f1" />

## 📁 Project File Structure

```text
devops-website/
│
├── index.html
├── style.css
├── script.js
├── Dockerfile
├── Jenkinsfile
├── .dockerignore
├── .gitignore
├── README.md
│
├── kubernetes/
   ├── deployment.yaml
   └── service.yaml

```

        
## Skills Demonstrated

- CI/CD Pipeline Automation
- Git and GitHub
- Docker Containerization
- Kubernetes Deployments and Pods
- Minikube
- Jenkins Pipeline
- Prometheus Metrics
- Grafana Dashboard Configuration
- Application Deployment Verification
- Troubleshooting and Monitoring

## Conclusion

This project provided hands-on experience in building an end-to-end DevOps deployment workflow using industry-relevant tools.

It demonstrates how application deployment can be automated through Jenkins, managed using Kubernetes, and monitored using Prometheus and Grafana.

The project helped strengthen practical understanding of CI/CD automation, containerization, Kubernetes orchestration, and application monitoring.

---

**Project Type:** DevOps | CI/CD | Kubernetes | Monitoring

**Environment:** Local Kubernetes Cluster using Minikube

**Monitoring:** Prometheus and Grafana
