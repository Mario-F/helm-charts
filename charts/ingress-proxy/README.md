# Ingress Proxy

This helm charts aims to make cluster external http(s) endpoints accessible through the clusters ingress.

Reasons to do this could be any of:

* Use the clusters Hostname/DNS service
* Use the clusters certificate managment
* Use clusters ingress IP (maybe a single ipv4 WAN endpoint)
* ... sure there will be more

## Usage

Using the helm chart simply by executing the following commands:

```shell
helm repo add mariof-charts https://mario-f.github.io/helm-charts/
helm install ingress-proxy mariof-charts/ingress-proxy
```
