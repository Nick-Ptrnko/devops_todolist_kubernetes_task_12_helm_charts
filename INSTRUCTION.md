# Deployment Instructions

This project provides a Helm-based setup to deploy the `todoapp` application along with its dependent `mysql` sub-chart into a local Kubernetes environment.

## Prerequisites

Ensure you have the following CLI tools installed:
* **Kind**
* **Helm**
* **kubectl**

## Deployment Steps

To provision the environment and launch the applications completely, use the provided automated script:

```
chmod +x bootstrap.sh
./bootstrap.sh
```

The `bootstrap.sh` script executes the following automated workflow:

* **Cluster Setup**: Creates a Kind cluster using the `cluster.yml` configuration file.
* **Node Management**: Applies a `NoSchedule` taint to nodes labeled with `app=mysql` to dedicate them to database workloads.
* **Dependency Resolution**: Resolves and packages the local `mysql` sub-chart specified in `Chart.yaml`.
* **Helm Deployment**: Installs or upgrades the `todoapp` Helm chart release into the cluster.
* **Ingress Integration**: Installs the `ingress-nginx` controller, configurations its affinity to run seamlessly on the control-plane node, and applies target Ingress rules.

## Verification

Verify the resource deployment within the designated `mateapp` namespace:

```
# Check running resources in the application namespace
kubectl get all -n mateapp
```
