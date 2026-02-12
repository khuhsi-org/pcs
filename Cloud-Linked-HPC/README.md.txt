#  Cloud Linked High Performance Computing (HPC) Cluster on AWS

## Project Overview

This project demonstrates the deployment of a scalable, secure, and high-availability High Performance Computing (HPC) cluster on AWS using Ubuntu 22.04.5 LTS.

The infrastructure integrates:

- SLURM Workload Manager
- BeeGFS 8.2.2 Parallel File System
- Pacemaker 2.1.2 & PCS 0.10.11 for High Availability
- Corosync 3.1.6 for cluster communication
- LDAP for centralized authentication
- ELK Stack (Elasticsearch, Logstash, Kibana) for log analysis
- Zabbix for infrastructure monitoring
- Python-based automation and monitoring scripts

The system is designed with subnet segmentation, controller failover, distributed storage, and centralized monitoring to simulate a real enterprise HPC environment.

---

## Architecture Design

###  AWS VPC Segmentation

The infrastructure is divided into two subnets:

### Public Subnet
- Login Node
- LDAP Server
- ELK Stack (Elasticsearch, Logstash, Kibana)
- Zabbix Monitoring Server

### Private Subnet
- Controller Node 1 (SLURM + PCS)
- Controller Node 2 (SLURM + PCS)
- Compute Nodes
- BeeGFS Storage Node

Private subnet nodes do not have direct internet access. Communication is restricted through Security Groups and internal VPC routing.

---

## High Availability Configuration

Controllers are configured in Active/Passive mode using:

- Pacemaker 2.1.2
- PCS 0.10.11
- Corosync 3.1.6

Features implemented:

- Cluster authentication
- Virtual IP failover
- Quorum policy configuration
- Resource restart and failover management

If one controller fails, SLURM services automatically shift to the secondary controller.

---

## Workload Management – SLURM

SLURM is configured for:

- Job scheduling
- Resource allocation
- Node management
- Partition configuration

Example commands used:
sinfo
squeue
sbatch job.sh
scontrol show nodes



Cluster nodes are defined in `slurm.conf`.

---

##  Distributed Storage – BeeGFS 8.2.2

BeeGFS provides:

- Parallel distributed file system
- Centralized shared storage
- Metadata and storage separation
- High throughput for compute workloads

Compute nodes mount shared storage for parallel processing.

---

##  Monitoring & Logging

###  ELK Stack
- Log ingestion via Logstash
- Indexing via Elasticsearch
- Visualization through Kibana dashboards

### Zabbix
- CPU, Memory, Disk monitoring
- Infrastructure alerts
- Node health status

###  Python Monitoring Script

A custom Python script checks:

- SLURM controller status
- BeeGFS services
- Disk utilization
- Node availability

---

##  Security Implementation

- VPC subnet segmentation
- Restricted SSH access
- Internal communication only for controllers
- LDAP-based centralized authentication
- Security group based port control

Configured ports include:

- 22 (SSH)
- 6817 (SLURM)
- 5405 (Corosync)
- 5044 (Logstash)
- 9200 (Elasticsearch)
- 5601 (Kibana)

---

##  Automation

Shell scripts are developed for:

- Login node setup
- Controller setup
- SLURM installation
- Compute node configuration
- BeeGFS deployment

Automation ensures reproducibility and reduces manual configuration effort.

---

##  Repository Structure
Cloud-Linked-HPC/
│
├── architecture/
├── automation/
├── configs/
├── screenshots/
└── docs/



---

##  Testing & Validation

- SLURM job execution tested using sample batch jobs
- Failover validation performed by stopping primary controller
- Storage validation via parallel read/write tests
- Log verification through Kibana dashboards

---

##  Documentation

Detailed setup guide available in:docs/Cloud_Linked_HPC_Setup_Guide.pdf


---

##  Author

Khushi Kumari  
PG-HPCSA  
GitHub: https://github.com/khuhsi-org

---

##  Conclusion

This project demonstrates the deployment of a production-like HPC cluster on AWS with high availability, distributed storage, workload management, centralized authentication, and real-time monitoring.

The architecture is designed to be scalable, fault-tolerant, and enterprise-ready.

