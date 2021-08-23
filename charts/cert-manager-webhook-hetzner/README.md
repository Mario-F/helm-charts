# CertManagerWebhhokHetzner Helm Chart

The helm chart to deploy this version of cert-manager-webhook-hetzner <https://github.com/Mario-F/cert-manager-webhook-hetzner>

Mainly to utilize the following merge request: <https://github.com/vadimkim/cert-manager-webhook-hetzner/pull/9>

Also featuring config abstraction to only just provide your Hetzener API-Key and yield an default ClusterIssuer.

## Usage

Using the helm chart simple use the following commands (replace my_api_key and my@mail.acme):

```shell
helm repo add mariof-charts https://mario-f.github.io/helm-charts/
helm install cert-manager-webhook-hetzner \
  --set hetzner.token="my_api_key" \
  --set hetzener.email="my@mail.acme" \
  mariof-charts/cert-manager-webhook-hetzner
```
