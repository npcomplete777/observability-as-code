# Check Rules

Contains Prometheus alerting and recording rules synced to Dash0 by the operator.

## CRD Kind

- **API**: `monitoring.coreos.com/v1`
- **Kind**: `PrometheusRule`
- **Scope**: Namespace-scoped

## Example

```yaml
apiVersion: monitoring.coreos.com/v1
kind: PrometheusRule
metadata:
  name: high-error-rate
  namespace: otel-demo
spec:
  groups:
    - name: service-alerts
      rules:
        - alert: HighErrorRate
          expr: rate(http_server_request_duration_seconds_count{http_response_status_code=~"5.."}[5m]) > 0.1
          for: 5m
          labels:
            severity: warning
          annotations:
            summary: "High error rate detected"
            description: "Error rate exceeds 10% for 5 minutes"
```

## Naming Conventions

- Use kebab-case: `<scope>-<purpose>.yaml`
- Examples: `frontend-alerts.yaml`, `slo-recording-rules.yaml`

## Validation

```bash
kubectl apply --dry-run=client -f check-rules/<file>.yaml
```
