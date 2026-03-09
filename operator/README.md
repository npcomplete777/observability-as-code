# Operator Configuration

Contains the Dash0 operator configuration and per-namespace monitoring resources.

## CRD Kinds

### Dash0OperatorConfiguration

- **API**: `operator.dash0.com/v1alpha1`
- **Kind**: `Dash0OperatorConfiguration`
- **Scope**: Cluster-scoped (one per cluster)

Configures the Dash0 operator's export endpoint and authentication.

```yaml
apiVersion: operator.dash0.com/v1alpha1
kind: Dash0OperatorConfiguration
metadata:
  name: dash0-operator-configuration
spec:
  export:
    dash0:
      endpoint: ingress.<region>.aws.dash0.com:4317
      apiEndpoint: https://api.<region>.aws.dash0.com
      authorization:
        secretRef:
          name: dash0-authorization-secret
          key: token
```

### Dash0Monitoring

- **API**: `operator.dash0.com/v1beta1`
- **Kind**: `Dash0Monitoring`
- **Scope**: Namespace-scoped (one per monitored namespace)

Enables telemetry collection and asset synchronization for a namespace.

```yaml
apiVersion: operator.dash0.com/v1beta1
kind: Dash0Monitoring
metadata:
  name: dash0-monitoring
  namespace: <target-namespace>
spec:
  instrumentWorkloads:
    mode: none
  logCollection: true
  synchronizePersesDashboards: true
  synchronizePrometheusRules: true
```

## Naming Conventions

- `dash0-operator-configuration.yaml` — cluster-wide operator config
- `dash0-monitoring/<namespace>.yaml` — per-namespace monitoring config

## Validation

```bash
kubectl apply --dry-run=client -f operator/dash0-operator-configuration.yaml
kubectl apply --dry-run=client -f operator/dash0-monitoring/<file>.yaml
```
