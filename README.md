# monkube
This repo is for learning purpouses, it allows you to setup a multicluster monitoring system with thanos, it follows a pull-based approach where the central component collects data from agents in different clusters when needed. This ensures real-time access and simplifies maintenance and scalability

## Architecture : 

![Thanos-prometheus architecture](Architecture_detailed(1).png)
The Prometheus instances in all the clusters are managed by Prometheus Operator for easier management and service discovery.
## Monitoring Setup

### 1. Install management cluster with thanos :

- Run `sudo chmod +x ./create-management-cluster.sh`
- Run `./create-management-cluster.sh [NAME]`

make sure that thanos setup is running
`kubectl get pods -n monitoring`

### 2. Install a workload cluster  and qdd it to thanos target list:

- Run `sudo chmod +x ./install_new_cluster.sh`
- Run `./install_new_cluster.sh [NAME] [MANAGEMENT_CLUSTER_NAME]` : it will install a new workload cluster with kind with full monitoring setup, 
- Add your new cluster to thanos target list : `subscribe_cluster.py [NAME]`

you can check if the cluster is added by checking logs of thanos querier in the management cluster or running :

- `kubectl port-forward svc/querier -n monitoring 9090:9090`

**PS** : thanos might take some around 1~2 minutes to discover the new cluster

- Remove a cluster cluster from thanos target list : `unsubscribe_cluster.py [NAME]`