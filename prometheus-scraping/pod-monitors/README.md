# Pod Monitors

Contains `PodMonitor` resources for Prometheus scrape configuration targeting Pods directly.

## CRD Kind

- **API**: `monitoring.coreos.com/v1`
- **Kind**: `PodMonitor`
- **Scope**: Namespace-scoped

## Example

```yaml
apiVersion: monitoring.coreos.com/v1
kind: PodMonitor
metadata:
  name: my-app-pods
  namespace: otel-demo
spec:
  selector:
    matchLabels:
      app: my-app
  podMetricsEndpoints:
    - port: metrics
      interval: 30s
```

## Naming Conventions

- Use kebab-case: `<workload>-pods.yaml`

## Validation

```bash
kubectl apply --dry-run=client -f prometheus-scraping/pod-monitors/<file>.yaml
```
