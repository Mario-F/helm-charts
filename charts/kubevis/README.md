# KubeVis Helm Chart

The helm chart to deploy kubevis <https://github.com/Mario-F/kubevis>

## Usage

Using the helm chart simple use the following commands:

```shell
helm repo add mariof-charts https://mario-f.github.io/helm-charts/
helm install kubevis mariof-charts/kubevis
```

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
