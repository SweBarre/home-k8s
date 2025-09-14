
```
helm repo add argocd https://argoproj.github.io/argo-helm
helm repo update
helm install --create-namespace --namespace argocd argocd argocd/argo-cd -f infrastructure/argocd/values.yaml

kubectl wait --for condition=established --timeout=60s crd/applications.argoproj.io
kubectl wait --for=condition=Available deployment/argocd-server -n argocd --timeout=300s
```
