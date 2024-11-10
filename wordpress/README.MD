# WordPress Helm Chart

This Helm Chart deploys WordPress and MySQL in a separate namespace `wordpress` using NodePort for external access to WordPress. The chart automatically creates necessary Deployment, Service, and PersistentVolumeClaim resources for both applications.

## Chart Structure

- Chart.yaml — Helm chart metadata
- values.yaml — main configuration settings for WordPress and MySQL, including images, services, storage, and resource limits
- templates/namespace.yaml — creates the `wordpress` namespace
- templates/deployment.yaml — creates the Deployment for MySQL and WordPress
- templates/pv.yaml — creates the PersistentVolume for MySQL and WordPress
- templates/pvc.yaml — creates the PersistentVolumeClaim for MySQL and WordPress
- templates/service.yaml — creates the Service for MySQL and WordPress

## Deploy the Chart

1. Install the Helm chart in the `wordpress` namespace
```bash
helm install wordpress ./wordpress --namespace wordpress --create-namespace
```

2. Verify that all resources have been successfully deployed
```bash
kubectl get all -n wordpress
```
## View the List of Pods

To view all pods in the `wordpress` namespace, run
```bash
kubectl get pods -n wordpress
```
## Connecting to Each Pod

To connect to a pod, use the `exec` command. For example, to connect to a WordPress pod
```bash
kubectl exec -it <wordpress-pod-name> -n wordpress -- /bin/bash
```
To connect to a MySQL pod
```bash
kubectl exec -it <mysql-pod-name> -n wordpress -- /bin/bash
```
## View Logs

To view the logs for each pod, use the `logs` command. For example, to view WordPress logs
```bash
kubectl logs -f $(kubectl get pod -A app=wordpress -o name) -n wordpress
```
For MySQL logs
```bash
kubectl logs -f $(kubectl get pod -A app=mysql -o name) -n wordpress
```

# Check services
```bash
kubectl get svc -n wordpress
```
