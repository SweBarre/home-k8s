
```
kubectl kustomize --enable-helm infrastructure/applications/argocd | kubectl apply -f -
kubectl wait --for condition=established --timeout=60s crd/applications.argoproj.io
kubectl wait --for=condition=Available deployment/argocd-server -n argocd --timeout=300s
kubectl apply -f infrastructure/applications/argocd/projects.yaml
```
