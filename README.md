# Cloud Linked HPC – High Performance Computing Cluster on AWS

## Project Overview

Cloud Linked HPC is a cloud-based High Performance Computing (HPC) cluster deployed on AWS using Ubuntu 22.04.5 LTS. 

The project demonstrates the design and implementation of a secure, scalable and high-availability HPC infrastructure integrating workload management, distributed storage, centralized authentication and monitoring systems.

The objective of this project is to simulate an enterprise-level HPC environment with proper network segmentation, failover mechanisms and automation.

---

## Architecture Overview

The infrastructure is deployed inside an AWS VPC and divided into two logical segments:

### Public Subnet
- Login Node
- LDAP Server (Centralized Authentication)
- ELK Stack (Log Management & Analysis)
- Zabbix (Infrastructure Monitoring)

### Private Subnet
- Controller Node 1 (SLURM + PCS)
- Controller Node 2 (SLURM + PCS)
- Compute Nodes
- BeeGFS Storage Node

Private subnet components are isolated from direct internet access to ensure security and internal communication only.

---

## Core Components Configured

### High Availability
- Pacemaker 2.1.2
- PCS 0.10.11
- Corosync 3.1.6

Controllers are configured in High Availability mode with failover capability.

---

### Workload Management
- SLURM Workload Manager

SLURM handles:
- Job scheduling
- Resource allocation
- Node management
- Partition configuration

---

### Distributed Storage
- BeeGFS 8.2.2

BeeGFS is configured as a parallel distributed file system enabling:
- Shared storage access
- High throughput
- Concurrent read/write operations across compute nodes

---

### Centralized Authentication
- LDAP Server

LDAP provides centralized user authentication for cluster access and resource management.

---

### Monitoring & Logging
- ELK Stack (Elasticsearch, Logstash, Kibana)
- Zabbix Monitoring Server

ELK is used for log collection and visualization.  
Zabbix is used for infrastructure monitoring and health checks.

A Python-based monitoring script is implemented to validate:
- SLURM service status
- BeeGFS services
- Disk utilization
- Node health

---

## Automation

Shell-based automation scripts are developed for:

- Login node setup
- Controller configuration
- SLURM installation
- Compute node setup
- BeeGFS deployment

Automation ensures reproducibility and consistent configuration.

---

## Repository Structure

- `architecture/` → Network and system architecture diagrams
- `automation/` → Shell scripts for deployment and configuration
- `configs/` → Service configuration files (SLURM, Corosync, BeeGFS, ELK, LDAP)
- `monitoring/` → Python monitoring scripts
- `screenshots/` → Dashboard and service validation screenshots
- `docs/` → Detailed setup documentation

---

## Scope of the Project

This project demonstrates:

- Deployment of HPC cluster in cloud environment
- High Availability controller configuration
- Parallel distributed storage integration
- Secure subnet segmentation
- Centralized authentication
- Monitoring and log management integration
- Infrastructure automation

The architecture is scalable and can be extended to support larger compute workloads and research applications.

---

## Conclusion

Cloud Linked HPC represents a production-oriented HPC deployment model combining high availability, distributed storage, workload management and centralized monitoring within a secure AWS-based architecture.
