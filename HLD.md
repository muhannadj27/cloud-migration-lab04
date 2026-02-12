# High-Level Design (HLD): Containerized Application with Managed Database

**Student:** Muhannad Jaber  
**Lab:** Containerized Application with Managed Database  
**Date:** Feb 2026  

---

## 1. Overview (Current vs Target State)

**Current Architecture:**
- WebServerVM hosts a lightweight Node.js web application  
- SQLVM hosts Microsoft SQL Server  
- VM-based deployment with limited scalability and availability  

**Target Architecture (Azure Cloud):**
- Web application containerized using Docker  
- Hosted on Azure Kubernetes Service (AKS)  
- Database migrated to Azure SQL Database (Managed SQL Service)  
- Public traffic routed via Load Balancer / Ingress  
- Maximum acceptable downtime: 6 hours  

---

## 2. Target Architecture Description

The target architecture uses container orchestration to improve scalability, availability, and reliability of the web application. The Node.js web application is packaged into a Docker container and deployed as multiple replicas (pods) within an AKS cluster. A load balancer or ingress controller distributes incoming user traffic across healthy pods.

The managed SQL database provides built-in high availability, automated backups, and patching, removing the operational overhead of managing a database virtual machine. If one pod or node fails, Kubernetes automatically reschedules workloads, ensuring continuous availability of the application.

---

## 3. Migration Steps

### Step 1: Containerization of the Web Application
- Create a Dockerfile for the Node.js application  
- Build and test the container image locally  
- Push the image to a container registry  
- Update application configuration to connect to managed SQL  

### Step 2: Migration of SQL Database
- Provision Azure SQL Database  
- Migrate schema and data from SQLVM  
- Validate data integrity and performance  
- Secure connectivity between AKS and SQL Database  

### Step 3: Configure Kubernetes for High Availability
- Deploy AKS with multiple worker nodes  
- Deploy the Node.js application as a Kubernetes Deployment  
- Configure multiple replicas (pods)  
- Enable health probes and autoscaling  

### Step 4: Cutover and Validation
- Freeze writes on the source database  
- Perform final data sync  
- Redirect traffic to the new AKS endpoint  
- Monitor application stability  

---

## 4. Architecture Diagram

![Target Architecture Diagram](diagram.png)

---

## 5. Benefits

- High availability through Kubernetes pod replication  
- Scalability through horizontal pod autoscaling  
- Reduced operational overhead with managed database  
- Improved reliability and fault tolerance  

---

## 6. Risks and Mitigation

- Risk: Data migration issues  
  Mitigation: Perform test migration and validation  

- Risk: Misconfigured networking  
  Mitigation: Validate connectivity in staging environment  

