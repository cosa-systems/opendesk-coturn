# coturn Helm Chart

This Helm chart provides a coturn server within SouvAP.


## TL;DR

```bash
helm repo add coturn https://gitlab.souvap-univention.de/api/v4/projects/113/packages/helm/stable

helm upgrade -i --create-namespace --namespace="${NAMESPACE}" \
    -f values-develop.yaml \
    --set-string coturn.externalIP="1.2.3.4" \
    --set-string coturn.realm="${REALM}" \
    --set-string coturn.authentication.user="${USER}" \
    --set-string coturn.authentication.password="${PASSWORD}" \
    turn coturn/coturn/
```

## Introduction

This chart is used to deploy coturn within SouvAP.

## Prerequisites
- Kubernetes 1.16+
- Helm 3.0.0+
- PV provisioner support in the underlying infrastructure

## Installing the Chart

To install the chart with the release name coturn:

```bash
helm upgrade -i --create-namespace --namespace="${NAMESPACE}" \
    -f values-develop.yaml \
    --set-string coturn.externalIP="1.2.3.4" \
    --set-string coturn.realm="${REALM}" \
    --set-string coturn.authentication.user="${USER}" \
    --set-string coturn.authentication.password="${PASSWORD}" \
    turn coturn/coturn/
```
values.develop example:
```yaml
coturn:
  minPort: 30500
  maxPort: 30550
  verbose: true
  realm: "turn.develop.souvap-univention.de"

service:
  listeningNodePort: 31478
  tlsListeningNodePort: 31549
  minPort: 30500

```

## Uninstalling the Chart

To install the release with name coturn:

```bash
helm uninstall coturn
```
