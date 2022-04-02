# Cert Manager Selfservice Helm Chart

The helm chart to deploy cert-manager-selfservice <https://github.com/Mario-F/cert-manager-selfservice>

## Requirements

The chart application requires a working installation of [cert-manager](https://cert-manager.io/)

## Usage

Simple usage of the helm chart would be like:

```shell
helm repo add mariof-charts https://mario-f.github.io/helm-charts/
helm install cert-manager-selfservice \
  --set selfservice.issuer.name="my-clusterissuer" \
  mariof-charts/cert-manager-selfservice
```

## Parameters

### Common parameters

| Name               | Description                                        | Value |
| ------------------ | -------------------------------------------------- | ----- |
| `nameOverride`     | String to partially override common.names.fullname | `""`  |
| `fullnameOverride` | String to fully override common.names.fullname     | `""`  |


### Cert-Manager-Selfservice Configuration parameters

| Name                          | Description                                               | Value                 |
| ----------------------------- | --------------------------------------------------------- | --------------------- |
| `selfservice.managerId`       | Uniq owner id for certificate ressources                  | `{{ .Release.Name }}` |
| `selfservice.issuer.kind`     | The cert-manager issuer type to use                       | `ClusterIssuer`       |
| `selfservice.issuer.name`     | The name of cert-manager issuer to use                    | `default-issuer`      |
| `selfservice.debug`           | Will set debug loglevel in selfservice                    | `false`               |
| `selfservice.cleanup.enabled` | Control if cleanup should enabled                         | `true`                |
| `selfservice.cleanup.hours`   | Time in hours after which unused certificates are deleted | `72`                  |


### Cert-Manager-Selfservice Deployment parameters

| Name                 | Description                                                        | Value                                      |
| -------------------- | ------------------------------------------------------------------ | ------------------------------------------ |
| `image.repository`   | cert-manager-selfservice image repository                          | `ghcr.io/mario-f/cert-manager-selfservice` |
| `image.tag`          | cert-manager-selfservice image tag (default to AppVersion)         | `""`                                       |
| `image.pullPolicy`   | cert-manager-selfservice image pull policy                         | `IfNotPresent`                             |
| `image.pullSecrets`  | Specify docker-registry secret names as an array                   | `[]`                                       |
| `nodeSelector`       | Node labels for pod assignment.                                    | `{}`                                       |
| `tolerations`        | Tolerations for pod assignment.                                    | `[]`                                       |
| `resources.limits`   | The resources limits for the cert-manager-selfservice container    | `{}`                                       |
| `resources.requests` | The requested resources for the cert-manager-selfservice container | `{}`                                       |


### Traffic exposure parameters

| Name           | Description       | Value       |
| -------------- | ----------------- | ----------- |
| `service.type` | Service type      | `ClusterIP` |
| `service.port` | Service HTTP port | `5080`      |


### Metrics parameters

| Name                                   | Description                                                                                 | Value   |
| -------------------------------------- | ------------------------------------------------------------------------------------------- | ------- |
| `metrics.enabled`                      | Setup metrics export                                                                        | `false` |
| `metrics.port`                         | Container Metrics Port scraped by Prometheus Exporter                                       | `6081`  |
| `metrics.serviceMonitor.enabled`       | Creates a Prometheus Operator ServiceMonitor (also requires `metrics.enabled` to be `true`) | `false` |
| `metrics.serviceMonitor.namespace`     | Namespace in which Prometheus is running                                                    | `""`    |
| `metrics.serviceMonitor.interval`      | Interval at which metrics should be scraped.                                                | `""`    |
| `metrics.serviceMonitor.scrapeTimeout` | Timeout after which the scrape is ended                                                     | `""`    |


### Additional features parameters

| Name        | Description                           | Value |
| ----------- | ------------------------------------- | ----- |
| `templates` | See templates section for explanation | `[]`  |


## Templates

This chart provides a template render mechanism for rendering additional ressources bound to this release.

It works like bedag/raw helm chart but not on subchart level, see this example (values.yaml):

```yaml
templates:
  - enabled: true
    content: |
      apiVersion: v1
      kind: ConfigMap
      metadata:
        name: {{ include "parent.fullname" . }}-additional
        labels:
          {{- include "parent.labels" . | nindent 4 }}
      data:
        example.data: |
          nothing special here
          out
```
