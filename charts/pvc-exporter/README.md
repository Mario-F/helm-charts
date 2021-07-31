# PVC Exporter Helm Chart

The helm chart to deploy pvc-exporter <https://github.com/Mario-F/pvc-exporter>

## Usage

Using the helm chart simply by using the following commands:

```shell
helm repo add mariof-charts https://mario-f.github.io/helm-charts/
helm install pvc-exporter mariof-charts/pvc-exporter
# enable prometheus monitor and rules
helm upgrade --install --set serviceMonitor.enabled=true --set prometheusRule.enabled=true pvc-exporter mariof-charts/pvc-exporter
```

## Values

| Key | Type | Default | Description |
|-----|------|---------|-------------|
| image.repository | string | `"ghcr.io/mario-f/pvc-exporter"` |  |
| image.repository | string | `".AppVersion"` |  |
| image.pullPolicy | string | `"IfNotPresent"` |  |
| image.pullSecrets | list | `[]` |  |
| serviceAccount.create | bool | `false` |  |
| scrapeInterval | int | `15` |  |
| pvcMapper.replicaCount | int | `1` |  |
| pvcMapper.metricsPort | int | `8849` |  |
| pvcMapper.extraArgs | list | `[]` |  |
| pvcMapper.resources.requests.cpu | string | `"100m"` |  |
| pvcMapper.resources.requests.memory | string | `"50Mi"` |  |
| pvcMapper.resources.limits.cpu | string | `"1000m"` |  |
| pvcMapper.resources.limits.memory | string | `"200Mi"` |  |
| pvcScanner.metricsPort | int | `8848` |  |
| pvcScanner.extraArgs | list | `[]` |  |
| pvcScanner.resources.requests.cpu | string | `"50m"` |  |
| pvcScanner.resources.requests.memory | string | `"50Mi"` |  |
| pvcScanner.resources.limits.cpu | string | `"500m"` |  |
| pvcScanner.resources.limits.memory | string | `"200Mi"` |  |
| dashboard.enabled | bool | `true` |  |
| dashboard.labels.grafana_dashboard | string | `"1"` |  |
| dashboard.uid | string | `"b064425af1e711eb"` |  |
| dashboard.title | string | `"Kubernetes / Persistent Volumes (PVC-Exporter)"` |  |
| dashboard.datasource | string | `"-- Grafana --"` |  |
| dashboard.timezone | string | `"UTC"` |  |
| serviceMonitor.enabled | bool | `false` |  |
| serviceMonitor.additionalLabels | object | `{}` |  |
| prometheusRule.enabled | bool | `false` |  |
| prometheusRule.additionalLabels | object | `{}` |  |
| prometheusRule.percent.warning | float | `0.7` |  |
| prometheusRule.percent.critical | float | `0.9` |  |
| raw.enabled | bool | `false` |  |
