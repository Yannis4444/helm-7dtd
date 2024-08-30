# Helm Chart for a 7 days to die server

![version](https://img.shields.io/github/tag/alexnuttinck/helm-7dtd.svg?label=release) ![test](https://github.com/alexnuttinck/helm-7dtd/actions/workflows/test.yaml/badge.svg) ![release](https://github.com/alexnuttinck/helm-7dtd/actions/workflows/release.yaml/badge.svg)

Helm Chart to deploy a `7 days to die` server in a Kubernetes cluster.

## Introduction

This [Helm](https://github.com/kubernetes/helm) chart installs [7dtd](https://7daystodie.com/) in a Kubernetes cluster.

## Prerequisites

- Kubernetes cluster 1.10+
- Helm 3.0.0+

## Installation

### Add Helm repository

```
helm repo add 7dtd https://alexnuttinck.dev/helm-7dtd/
helm repo update
```

### Configure the chart

The following items can be set via `--set` flag during installation or configured by editing the `values.yaml` directly (need to download the chart first).

Feel free to modify values.yaml before installation

values.yaml options:

https://github.com/vinanrra/Docker-7DaysToDie/blob/master/docs/parameters.md#7-days-to-die

### Install the chart

Install the 7dtd helm chart with a release name `my-release`:

```bash
helm install my-release 7dtd/7dtd
```

or by cloning this repository:

```
helm install 7daystodie . -f values.yaml --namespace 7days --create-namespace
```

## Uninstallation

To uninstall/delete the `my-release` statefulset:

```bash
helm delete my-release
```

## Configuration

The following table lists the configurable parameters of the swagger-ui chart and the default values.

| Parameter                          | Description                                                                                                                                                                                 | Default                                              |
|------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------|
| **Image**                          |
| `image.repository`                 | 7dtd Image name                                                                                                                                                                             | `vinanrra/7dtd-server`                               |
| `image.tag`                        | 7dtd Image tag                                                                                                                                                                              | Optional to overwrite the image version              |
| `image.pullPolicy`                 | 7dtd Image pull policy                                                                                                                                                                      | `IfNotPresent`                                       |
| **Environment**                    |
| `env`                              | Environment variables as described in the [underlying Docker](https://github.com/vinanrra/Docker-7DaysToDie/blob/69e5b0ae5e8a3ccff74eed23ee8b54bd6d286e5c/docs/parameters.md#7-days-to-die) | Check the `values.yaml` file for the default values. |
| **Service**                        |
| `service.type`                     | Type of service for 7dtd frontend                                                                                                                                                           | `NodePort`                                           |
| `service.clusterIP`                | internal cluster service IP (set to "-" to pass an empty value)                                                                                                                             | `nil`                                                |
| `service.loadBalancerIP`           | LoadBalancerIP if service type is `LoadBalancer`                                                                                                                                            | `nil`                                                |
| `service.loadBalancerSourceRanges` | Address that are allowed when svc is `LoadBalancer`                                                                                                                                         | `[]`                                                 |
| `service.annotations`              | Service annotations                                                                                                                                                                         | `{}`                                                 |
| **Ingress**                        |
| `ingress.enabled`                  | Enables Ingress                                                                                                                                                                             | `false`                                              |
| `ingress.annotations`              | Ingress annotations                                                                                                                                                                         | `{}`                                                 |
| `ingress.path`                     | Path to access frontend                                                                                                                                                                     | `/`                                                  |
| `ingress.hosts`                    | Ingress hosts                                                                                                                                                                               | `[]`                                                 |
| `ingress.tls`                      | Ingress TLS configuration                                                                                                                                                                   | `[]`                                                 |
| **ReadinessProbe**                 |
| `readinessProbe`                   | Rediness Probe settings                                                                                                                                                                     | Check the `values.yaml` file for the default values. |
| **LivenessProbe**                  |
| `livenessProbe`                    | Liveness Probe settings                                                                                                                                                                     | Check the `values.yaml` file for the default values. |
| **Resources**                      |
| `resources`                        | CPU/Memory resource requests/limits                                                                                                                                                         | `{}`                                                 |

## Credits

Docker versions of 7dtd are pulled from:

* https://github.com/vinanrra/Docker-7DaysToDie
* https://hub.docker.com/r/vinanrra/7dtd-server

## Contributing

Feel free to contribute by making a [pull request](https://github.com/alexnuttinck/helm-7dtd/pull/new/master).

Please read the official [Contribution Guide](https://github.com/helm/charts/blob/master/CONTRIBUTING.md) from Helm for more information on how you can contribute to this Chart.

## License

[MIT License](/LICENSE.md)
