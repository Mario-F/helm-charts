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

## Examples (values.yaml)

Simply forward to a server on the network without tls:

```yaml
simple:
  enabled: true
  endpoint:
    ip: 10.10.10.10
    port: 8080
  ingress:
    hostnames:
      - my.example.com
```

Forward to a server using tls, custom ingress class, annotations and secure with basic-auth:

```yaml
simple:
  enabled: true
  endpoint:
    ip: 10.10.10.10
    port: 8080
  ingress:
    hostnames:
      - my.example.com
    class: "custom-nginx"
    tls:
      clusterIssuer: "letsencrypt-stage"
    annotations:
      nginx.ingress.kubernetes.io/proxy-body-size: "0"
  auth:
    username: dummyuser
    password: securepassword1234
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
