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

For more configuration see [values.yaml](./values.yaml)

## Parameters

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
