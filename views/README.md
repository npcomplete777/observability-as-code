# Views

Contains saved views for logs, traces, and metrics in Dash0.

## CRD Kind

- **API**: `observability.dash0.com/v1alpha1`
- **Kind**: `Dash0View`
- **Scope**: Namespace-scoped

## Example

```yaml
apiVersion: observability.dash0.com/v1alpha1
kind: Dash0View
metadata:
  name: error-logs
  namespace: otel-demo
spec:
  type: resources
  filter: "severity = ERROR"
```

## Naming Conventions

- Use kebab-case: `<signal>-<purpose>.yaml`
- Examples: `error-logs.yaml`, `slow-traces.yaml`

## Validation

```bash
kubectl apply --dry-run=client -f views/<file>.yaml
```
