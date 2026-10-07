### Prepare Mock Environment
```bash
az aks get-credentials --name MyManagedCluster --resource-group MyResourceGroup
# az aks get-credentials --name aks-cloud-k8s-lab-dev-ause-01 --resource-group rg-cloud-k8s-lab-dev-ause-01

kubectl config current-context
kubectl get nodes
```

### Troubleshooting CrashLoopBackOff
```bash
cd k8s/crashloopbackoff

kubectl apply -f mock.yaml

# use kubectl describe pod to check container states, exit reasons, and Pod events.
kubectl describe pod <pod-name>

# Use kubectl logs to inspect detailed error messages.
kubectl logs <pod-name>

kubectl delete deployment troubleshooting-lab -n default
```

### Troubleshooting Out-Of-Memory Killed
```bash
cd k8s/oomkilled

kubectl apply -f mock.yaml

# Use kubectl logs to inspect detailed error messages.
kubectl logs <pod-name>

kubectl delete deployment oom-lab
```