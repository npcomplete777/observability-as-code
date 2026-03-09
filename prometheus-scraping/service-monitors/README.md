# Service Monitors

Contains `ServiceMonitor` resources for Prometheus scrape configuration targeting Kubernetes Services.

## CRD Kind

- **API**: `monitoring.coreos.com/v1`
- **Kind**: `ServiceMonitor`
- **Scope**: Namespace-scoped

## Example

```yaml
apiVersion: monitoring.coreos.com/v1
kind: ServiceMonitor
metadata:
  name: my-service-metrics
  namespace: otel-demo
spec:
  selector:
    matchLabels:
      app: my-service
  endpoints:
    - port: metrics
      interval: 30s
```

## Naming Conventions

- Use kebab-case: `<service>-metrics.yaml`

## Validation

```bash
kubectl apply --dry-run=client -f prometheus-scraping/service-monitors/<file>.yaml
```
