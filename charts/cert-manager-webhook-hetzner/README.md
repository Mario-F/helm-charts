# Cert Manager Webhook Hetzner Helm Chart

The helm chart to deploy this version of cert-manager-webhook-hetzner <https://github.com/Mario-F/cert-manager-webhook-hetzner>

Also featuring config abstraction to only just provide your Hetzener API-Key and yield an default ClusterIssuer.

## Requirements

This chart requires a working installation of [cert-manager](https://cert-manager.io/)

## Usage

Using the helm chart simple use the following commands (replace my_api_key and my@mail.acme):

```shell
helm repo add mariof-charts https://mario-f.github.io/helm-charts/
helm install cert-manager-webhook-hetzner \
  --set hetzner.token="my_api_key" \
  --set hetzener.email="my@mail.acme" \
  mariof-charts/cert-manager-webhook-hetzner
```

## Parameters

### Common parameters

| Name               | Description                                        | Value |
| ------------------ | -------------------------------------------------- | ----- |
| `nameOverride`     | String to partially override common.names.fullname | `""`  |
| `fullnameOverride` | String to fully override common.names.fullname     | `""`  |


### Cert-Manager-Webhook-Hetzner Configuration parameters

| Name                             | Description                                                            | Value                                            |
| -------------------------------- | ---------------------------------------------------------------------- | ------------------------------------------------ |
| `groupName`                      | Cert-Manager groupName                                                 | `acme.default.hetzner.webhook`                   |
| `hetzner.token`                  | Hetzner DNS api token                                                  | `""`                                             |
| `hetzner.email`                  | E-Mail presented to lets-encrypt                                       | `""`                                             |
| `hetzner.acmeServer`             | lets-encrypt api to use                                                | `https://acme-v02.api.letsencrypt.org/directory` |
| `certManager.namespace`          | Namespace cert-manager is deployed                                     | `cert-manager`                                   |
| `certManager.serviceAccountName` | ServiceAccountname of cert-manager access this webhook                 | `cert-manager`                                   |
| `image.repository`               | cert-manager-webhook-hetzner image repository                          | `mariof2002/cert-manager-webhook-hetzner`        |
| `image.tag`                      | cert-manager-webhook-hetzner image tag (default to AppVersion)         | `""`                                             |
| `image.pullPolicy`               | cert-manager-webhook-hetzner image pull policy                         | `IfNotPresent`                                   |
| `service.type`                   | Service type                                                           | `ClusterIP`                                      |
| `service.port`                   | Service HTTP port                                                      | `443`                                            |
| `resources.limits`               | The resources limits for the cert-manager-webhook-hetzner container    | `{}`                                             |
| `resources.requests`             | The requested resources for the cert-manager-webhook-hetzner container | `{}`                                             |
| `nodeSelector`                   | Node labels for pod assignment.                                        | `{}`                                             |
| `tolerations`                    | Tolerations for pod assignment.                                        | `[]`                                             |
| `affinity`                       | Affinity for pod assignment                                            | `{}`                                             |


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