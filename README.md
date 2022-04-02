# MarioF Helm Charts

[![Conventional Commits](https://img.shields.io/badge/Conventional%20Commits-1.0.0-yellow.svg)](https://conventionalcommits.org)
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
* [Cert Manager Selfservice](charts/cert-manager-selfservice/README.md)
* [Ingress Proxy](charts/ingress-proxy/README.md)
* [KubeVis](charts/kubevis/README.md)
* [PVC Exporter](charts/pvc-exporter/README.md)
* [Whoami](charts/whoami/README.md)

## Development

### Versioning

The chart and app versions are distinct from each other, this means chart development will increase the chart version according to [semantic-versioning](https://semver.org/).

Application version update will trigger only a patch release.

### README

Some charts using bitnami [readme-generator-for-helm](https://github.com/bitnami-labs/readme-generator-for-helm), please make sure to update readme this way.

```shell
readme-generator -v values.yaml -r README.md
```
