
```
kubectl kustomize --enable-helm infrastructure/platform/argocd | kubectl apply -f -
kubectl wait --for condition=established --timeout=60s crd/applications.argoproj.io
kubectl wait --for=condition=Available deployment/argocd-server -n argocd --timeout=300s
kubectl apply -f infrastructure/applications/argocd/projects.yaml

kubectl apply -f infrastructure/infrastructure-core.yaml
kubectl apply -f infrastructure/infrastructure-platform.yaml
kubectl apply -f workloads/workloads.yaml
kubectl apply -f cumin/infrastructure/infrastructure.yaml
```
