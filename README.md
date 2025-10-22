
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

# Poblano

Generate root credentials for s3 tenant
```
kubectl -n minio create secret generic s3-config --from-literal=config.env="export MINIO_ROOT_USER=$(openssl rand -hex 10)
export MINIO_ROOT_PASSWORD=$(openssl rand -base64 48)" --dry-run=client -o yaml | kubeseal > poblano/workloads/minio/s3-config.yaml
```

```
kubectl directpv discover
kubectl directpv init drives.yaml --dangerous
```
