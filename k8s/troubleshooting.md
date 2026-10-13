### Prepare Mock Environment
```bash
az aks get-credentials --name MyManagedCluster --resource-group MyResourceGroup
# az aks get-credentials --name aks-cloud-k8s-lab-dev-ause-01 --resource-group rg-cloud-k8s-lab-dev-ause-01

kubectl config current-context
kubectl get nodes
```

### CrashLoopBackOff

```bash
cd k8s/crashloopbackoff

kubectl apply -f mock.yaml

# use kubectl describe pod to check container states, exit reasons, and Pod events.
kubectl describe pod <pod-name>

# Use kubectl logs to inspect detailed error messages.
kubectl logs <pod-name>

kubectl delete deployment troubleshooting-lab -n default
```

### Out-Of-Memory Killed

OOMKilled means that a container process was terminated because of an out-of-memory condition.

```bash
cd k8s/oomkilled
kubectl apply -f mock.yaml

# Use kubectl logs to inspect detailed error messages.
kubectl logs <pod-name>

kubectl delete deployment oom-lab
```

### HPA Scaling Blocked

A workload is configured with memory-based HPA, but it does not scale as expected.

```bash
cd k8s/hpa-scaling-blocked
kubectl apply -f mock.yaml

# Check the configured metric and its current value.
kubectl get hpa -n hpa-lab
# Result: The memory-typo metric is unknown.

# Inspect the metric retrieval error.
kubectl describe hpa cpu-demo -n hpa-lab
# Result: HPA cannot retrieve the configured metric.

# Check memory utilization after correcting the metric name.
kubectl get hpa -n hpa-lab
# Result: Memory utilization is still unknown.

# Inspect the remaining metric errors.
kubectl describe hpa cpu-demo -n hpa-lab

# Check scaling after fixing the memory request.
kubectl get hpa -n hpa-lab
# Result: Memory utilization is 222%, above the 50% target.

# Inspect the scaling event.
kubectl describe hpa cpu-demo -n hpa-lab
# Result: HPA successfully requested 3 replicas.

# Confirm that all 3 replicas are ready after fixing the quota.
kubectl get deployments,pods -n hpa-lab
```