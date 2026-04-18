# Observability Platform for Kubernetes

Full-stack monitoring for a FastAPI microservice running on Kubernetes.

## Stack
- Prometheus — metrics collection
- Grafana — dashboards and visualization  
- AlertManager — alerting
- kube-prometheus-stack — all-in-one Helm chart

## What it monitors
- Request rate (per endpoint)
- Error rate (4xx/5xx)
- p99 latency
- Pod health

## Alert rules
- HighErrorRate — fires if error rate > 0.1 req/s for 2 minutes
- PodDown — fires if any FastAPI pod is down for 1 minute

## Deploy
```bash
helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
helm install monitoring prometheus-community/kube-prometheus-stack \
  --namespace monitoring --create-namespace \
  --set grafana.adminPassword=admin123

kubectl apply -f k8s/monitoring/servicemonitor.yaml
kubectl apply -f k8s/monitoring/alert-rules.yaml
```
