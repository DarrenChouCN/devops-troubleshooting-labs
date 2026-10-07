```bash
az aks get-credentials --name MyManagedCluster --resource-group MyResourceGroup
# az aks get-credentials --name aks-cloud-k8s-lab-dev-ause-01 --resource-group rg-cloud-k8s-lab-dev-ause-01

kubectl config current-context
kubectl get nodes

cd k8s/crashloopbackoff

kubectl apply -f mock.yaml
```


```bash
kubectl get pods

kubectl describe pod <pod-name>
# kubectl describe pod troubleshooting-lab-5f4475f7b5-2g5hv

kubectl logs <pod-name>
# kubectl logs troubleshooting-lab-5f4475f7b5-2g5hv

```