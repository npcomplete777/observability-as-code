# Synthetic Checks

Contains synthetic monitoring checks managed by the Dash0 operator.

## CRD Kind

- **API**: `observability.dash0.com/v1alpha1`
- **Kind**: `Dash0SyntheticCheck`
- **Scope**: Namespace-scoped

## Example

```yaml
apiVersion: observability.dash0.com/v1alpha1
kind: Dash0SyntheticCheck
metadata:
  name: homepage-health
  namespace: otel-demo
spec:
  type: http
  url: "https://example.com/health"
  frequency: 60
  locations:
    - us-east-1
    - eu-west-1
  assertions:
    - type: statusCode
      operator: equals
      value: "200"
```

## Naming Conventions

- Use kebab-case: `<target>-<check-type>.yaml`
- Examples: `homepage-health.yaml`, `api-availability.yaml`

## Validation

```bash
kubectl apply --dry-run=client -f synthetic-checks/<file>.yaml
```
