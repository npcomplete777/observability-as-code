# observability-as-code

Declarative observability configuration managed by the [Dash0 Kubernetes Operator](https://www.dash0.com/documentation/dash0/dash0-kubernetes-operator) and synced via ArgoCD.

## Repository Structure

| Directory | CRD Kind | Description |
|-----------|----------|-------------|
| `operator/` | `Dash0OperatorConfiguration`, `Dash0Monitoring` | Operator and per-namespace monitoring config |
| `dashboards/` | `PersesDashboard` | Perses-format dashboards synced to Dash0 |
| `check-rules/` | `PrometheusRule` | Alerting and recording rules |
| `synthetic-checks/` | `Dash0SyntheticCheck` | Synthetic monitoring checks |
| `views/` | `Dash0View` | Saved views for logs, traces, and metrics |
| `prometheus-scraping/` | `ServiceMonitor`, `PodMonitor` | Prometheus scrape configurations |

## How Changes Flow

```
commit → merge to main → ArgoCD sync → Dash0 operator reconciliation → assets appear in Dash0 UI
```

1. Edit a YAML file in this repo (e.g., add a dashboard, update an alert threshold)
2. Open a PR and merge to `main`
3. ArgoCD detects the change and syncs the manifests to the cluster
4. The Dash0 operator reconciles the CRDs and pushes the configuration to the Dash0 platform
5. Changes are visible in the Dash0 UI

## Local Validation

Dry-run any manifest before committing:

```bash
kubectl apply --dry-run=client -f <file>.yaml
```

## Documentation

- [Dash0 Kubernetes Operator](https://www.dash0.com/documentation/dash0/dash0-kubernetes-operator)
