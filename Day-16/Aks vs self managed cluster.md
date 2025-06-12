## K8s :

**Control plane :** Best practice is to have three nodes   

**Data plane :**  Best practice is to two nodes

## 

| Feature         | On-Premises Cluster                                                            | Self-Managed Kubernetes Cluster                                                 | Azure Kubernetes Service (AKS)                                                    |
| --------------- | ------------------------------------------------------------------------------ | ------------------------------------------------------------------------------- | --------------------------------------------------------------------------------- |
| **Maintenance** | You are responsible for all upgrades and maintenance.                          | You must manage version upgrades and patches manually.                          | Azure manages control plane upgrades and patching. Lower maintenance overhead.    |
| **Cost**        | High, due to hardware, power, and manpower costs.                              | Moderate – depends on infrastructure setup (e.g., autoscaling, VM sizing).      | Cost-effective – pay-as-you-go model with scaling flexibility.                    |
| **Scaling**     | Scaling is manual and limited by physical capacity.                            | Requires manual setup of autoscaling policies and node pools.                   | Built-in autoscaling based on node pools and demand.                              |
| **Integration** | Complex – no native load balancer; MetalLB required, not ideal for production. | Requires manual integration with CSI drivers, secrets, persistent volumes, etc. | Easy integration with Azure services (e.g., Azure Monitor, Key Vault, CSI, etc.). |
