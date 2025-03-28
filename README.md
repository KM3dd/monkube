# 🚀 MonKube: Multi-Cluster Monitoring Simplified
monkube is a learning-focused project that enables you to set up a multi-cluster monitoring system using Thanos. It follows a pull-based approach, where a central component collects data from agents in different clusters on demand.

## 🏗️ Architecture : 

![Thanos-prometheus architecture](Architecture_detailed(1).png)
The Prometheus instances in all the clusters are managed by Prometheus Operator for easier management and service discovery.



## 🛠️ Quick Start Guide

### Prerequisites
- KinD v

### 1. Management Cluster Setup 🖥️

Prepare your management cluster with Thanos:

```bash
# Grant execution permissions
sudo chmod +x ./create-management-cluster.sh

# Create management cluster
./create-management-cluster.sh [CLUSTER_NAME]

# Verify Thanos installation
kubectl get pods -n monitoring
```

### 2. Workload Cluster Deployment 🌟:

```bash
# Make installation script executable
sudo chmod +x ./install_new_cluster.sh

# Install and configure new workload cluster
./install_new_cluster.sh [CLUSTER_NAME] [MANAGEMENT_CLUSTER_NAME]

# Subscribe cluster to Thanos
subscribe_cluster.py [CLUSTER_NAME]
```

you can check if the cluster is added by checking logs of thanos querier in the management cluster or running :

- `kubectl port-forward svc/querier -n monitoring 9090:9090`

> **_NOTE:_**  thanos might take some around 1~2 minutes to discover the new cluster

- To remove a cluster cluster from thanos target list : `unsubscribe_cluster.py [NAME]`

This project is designed to help users understand multi-cluster monitoring with Thanos and Prometheus Operator while ensuring an efficient and scalable setup. 🚀 
