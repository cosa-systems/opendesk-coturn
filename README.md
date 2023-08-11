<!--
SPDX-FileCopyrightText: 2023 Bundesministerium des Innern und für Heimat, PG ZenDiS "Projektgruppe für Aufbau ZenDiS"

SPDX-License-Identifier: Apache-2.0
-->
# Sovereign Workplace coturn Helm Chart

This repository contains a Helm chart for deploying coturn.
It is mainly used by Jitsi.



## Prerequisites

Before you begin, ensure you have met the following requirements:

- Kubernetes 1.21+
- Helm 3.0.0+
- PV provisioner support in the underlying infrastructure


## Documentation

The documentation is placed in the README of the coturn helm chart:

- [coturn](charts/coturn)

### Making coturn available to the Internet

Currently, there are 2 options supported: `LoadBalanacer` and `NodePort`. Depending on your cluster/network setup, there might be also other options which are not described in this readme.

#### Option 1: service of type `LoadBalancer`

This requires a cloud setup that enables a Loadbalancer attachement. This could be enabled via values:

```yaml
service:
  type: "LoadBalancer"

# all ports specified here will be available on the LoadBalancer:
coturn:
  # -- listening Port (TCP & UDP)
  listeningPort: 3478
  tls:
    # -- enable TLS
    enabled: true
    # -- TLS Port (TCP & UDP)
    listeningPort: 5349
  # -- lower bound of the UDP relay endpoints
  minPort: 49152
  # -- upper bound of the UDP relay endpoints
  maxPort: 65535
```

#### Option 2: NodePort with NAT (Network Address Translation) and PAT (Port Address Translation)

This setup requires an external firewall or loadbalancer with a public IP and port translation from the specified ports on the external IP to the corresponding NodePorts on the internal Node IPs.

```yaml
service:
  type: "NodePort"
  # -- to which NodePort is the external Listening Port fowarded?
  # only needed if type is NodePort
  listeningNodePort: 31478
  # -- to which Node Port is the external TLS Listening Port forwarded?
  # only needed if type is NodePort
  tlsListeningNodePort: 31549
  # -- starting NodePort of the UDP Relay Endpoints
  # only needed if type is NodePort
  minNodePort: 30500

# all ports specified here will be available on corresponding NodePort:
coturn:
  # -- listening Port (TCP & UDP)
  listeningPort: 3478
  tls:
    # -- enable TLS
    enabled: true
    # -- TLS Port (TCP & UDP)
    listeningPort: 5349
  # -- lower bound of the UDP relay endpoints
  minPort: 30500
  # -- upper bound of the UDP relay endpoints
  maxPort: 30550
```

## License

This project uses the following license: Apache-2.0

## Copyright

Copyright © 2023 Bundesministerium des Innern und für Heimat, PG ZenDiS "Projektgruppe für Aufbau ZenDiS"
