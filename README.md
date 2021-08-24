# MarioF Helm Charts

![Release Charts](https://github.com/mario-f/helm-charts/workflows/Release%20Charts/badge.svg?branch=main)
[![Average time to resolve an issue](http://isitmaintained.com/badge/resolution/mario-f/helm-charts.svg)](http://isitmaintained.com/project/mario-f/helm-charts "Average time to resolve an issue")
[![Percentage of issues still open](http://isitmaintained.com/badge/open/mario-f/helm-charts.svg)](http://isitmaintained.com/project/mario-f/helm-charts "Percentage of issues still open")

## Usage

[Helm](https://helm.sh) must be installed to use the charts.
Please refer to Helm's [documentation](https://helm.sh/docs/) to get started.

Once Helm is set up properly, add the repo as follows:

```shell
helm repo add mariof-charts https://mario-f.github.io/helm-charts/
```

You can then run `helm search repo mariof-charts` to see the charts.

## Charts

* [Cert Manager Webhook Hetzner](charts/cert-manager-webhook-hetzner/README.md)
* [Ingress Proxy](charts/ingress-proxy/README.md)
* [KubeVis](charts/kubevis/README.md)
* [PVC Exporter](charts/pvc-exporter/README.md)
