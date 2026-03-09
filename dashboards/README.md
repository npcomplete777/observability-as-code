# Dashboards

Contains Perses-format dashboards synced to Dash0 by the operator.

## CRD Kind

- **API**: `perses.dev/v1alpha1`
- **Kind**: `PersesDashboard`
- **Scope**: Namespace-scoped

## Example

```yaml
apiVersion: perses.dev/v1alpha1
kind: PersesDashboard
metadata:
  name: my-service-overview
  namespace: otel-demo
spec:
  display:
    name: "My Service Overview"
  duration: 1h
  panels: {}
  layouts: []
```

## Naming Conventions

- Use kebab-case for file and resource names: `<service>-<purpose>.yaml`
- Examples: `frontend-latency.yaml`, `checkout-service-overview.yaml`

## Validation

```bash
kubectl apply --dry-run=client -f dashboards/<file>.yaml
```
