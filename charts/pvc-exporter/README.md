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

See [values.yaml](./values.yaml)
