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
| prometheusRule.thresholds.absolute | list(object) | see [below](#Absolute) | |
| prometheusRule.thresholds.predictive | list(object) | see [below](#Predictive) | |
| raw.enabled | bool | `false` |  |

### Thresholds

There are two kinds of alerting thresholds, absolute and predictive. Both types allow effectively unlimited amount of
instances to be defined, although more than two or three are rarely useful. You can define a set of labels for each
instance to indicate things like severity.

While the first will trigger an alert on crossing a fixed usage percentage, the latter will attempt to predict the time
how long (if ever) it will take to fill the volume.

*Caution*: Since duration values are parsed with golang's `time.ParseDuration`, the largest available unit is `h`. Thus,
to express ex. `1d`, you _must_ use `24h` and so on.

#### Absolute

Those alerts will trigger on usage crossing a flat percentage of the volume's total size for a given timespan.

By default, two alerts are defined:

- less than 30% left for more than one hour, labelled `severity: warning`
- less than 10% left for at least 15 minutes, labelled `severity: critical`

```yaml
      - percentage: 30
        for: 1h
        labels:
          severity: warning
      - percentage: 10
        for: 15m
        labels:
          severity: critical
```

#### Predictive

Observing values over a given timeframe, a linear prediction is made on the expected usage at a future point in time. If
the predicted value is at or below zero, indicating that the volume would be filled by then, an alert is raised.

By default the triggers are:

- based on the last six hours, the disk would fill up in less than four days, labelled `severity: warning`
- based on the last hour, the disk would fill up in less than one day, labelled `severity: critical`


```yaml
      - interval: 6h
        target: 96h
        labels:
          severity: warning
      - interval: 1h
        target: 24h
        labels:
          severity: critical
```