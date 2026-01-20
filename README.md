# PCS-Based High Availability Gateway

## Overview
This repository contains the core configuration and design of a high-availability
gateway implemented using Pacemaker, Corosync, and PCS.

## Architecture
- Two-node Linux cluster
- PCS-managed Virtual IP
- HA Gateway role (login/API + storage mount)
- Automatic failover on node failure

## Components
- Corosync: Cluster communication
- Pacemaker: Resource management
- PCS: Cluster configuration interface

## Failover Behavior
When the active node fails, PCS automatically migrates the gateway role to the
standby node, ensuring uninterrupted user access.

## Scope
This repository focuses on infrastructure-level high availability.

