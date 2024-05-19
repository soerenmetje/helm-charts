# Dolibarr

[Dolibarr](https://www.dolibarr.org/) is a web application to manage your company or foundation's activity (contacts, suppliers, invoices, orders, stocks, agenda, accounting, ...).
This chart bootstraps a Dolibarr deployment on a [Kubernetes](http://kubernetes.io) cluster using the [Helm](https://helm.sh) package manager. It uses the [tuxgasy/dolibarr](https://hub.docker.com/r/tuxgasy/dolibarr) Docker image.

> **DISCLAIMER**: This is an unofficial chart not supported by Dolibarr authors.

> Forked from https://github.com/cowboysysop/charts/tree/0641bb51555291514713b2c788bfb5c48ad4f63a/charts/dolibarr
> to add PVC for Dolibarr html/custom directory

## Prerequisites

- Kubernetes >= 1.24
- Helm >= 3.9

## Installing

Install the chart:

```bash
# in case not already added
helm repo add bitnami https://charts.bitnami.com/bitnami/

helm dependency build
helm repo add soerenmetje https://soerenmetje.github.io/helm-charts/
helm repo update

helm show values soerenmetje/dolibarr > my-dolibarr-vals.yaml
# Before installing, edit my-dolibarr-vals.yaml e.g. by inserting your sub-domain
helm install my-release soerenmetje/dolibarr -f my-dolibarr-vals.yaml
```

These commands deploy Dolibarr on the Kubernetes cluster with the release name `my-release` and the configuration defined in `my-dolibarr-vals.yaml`.
## Upgrading

Upgrade the chart deployment:

```bash
helm upgrade my-release soerenmetje/dolibarr -f my-dolibarr-vals.yaml
```

The command upgrades the existing `my-release` deployment with the most latest release of the chart.

**TIP**: Use `helm repo update` to update information on available charts in the chart repositories.

## Uninstalling

Uninstall the `my-release` deployment:

```bash
helm uninstall my-release
```

The command deletes the release named `my-release` and frees all the kubernetes resources associated with the release.

**TIP**: Specify the `--purge` argument to the above command to remove the release from the store and make its name free for later use.

## Configuration

### Global parameters

| Name                      | Description                                     | Default |
|---------------------------|-------------------------------------------------|---------|
| `global.imageRegistry`    | Global Docker image registry                    | `""`    |
| `global.imagePullSecrets` | Global Docker registry secret names as an array | `[]`    |

### Common parameters

| Name                | Description                                                                                   | Default |
|---------------------|-----------------------------------------------------------------------------------------------|---------|
| `kubeVersion`       | Override Kubernetes version                                                                   | `""`    |
| `nameOverride`      | Partially override `dolibarr.fullname` template with a string (will prepend the release name) | `""`    |
| `fullnameOverride`  | Fully override `dolibarr.fullname` template with a string                                     | `""`    |
| `commonAnnotations` | Annotations to add to all deployed objects                                                    | `{}`    |
| `commonLabels`      | Labels to add to all deployed objects                                                         | `{}`    |
| `extraDeploy`       | Array of extra objects to deploy with the release                                             | `[]`    |

### Parameters

| Name                                  | Description                                                                                           | Default                      |
|---------------------------------------|-------------------------------------------------------------------------------------------------------|------------------------------|
| `replicaCount`                        | Number of replicas (do not change it)                                                                 | `1`                          |
| `updateStrategy.type`                 | Update strategy type (do not change it)                                                               | `Recreate`                   |
| `image.registry`                      | Image registry                                                                                        | `docker.io`                  |
| `image.repository`                    | Image repository                                                                                      | `tuxgasy/dolibarr`           |
| `image.tag`                           | Image tag                                                                                             | `19.0.2`                     |
| `image.digest`                        | Image digest                                                                                          | `""`                         |
| `image.pullPolicy`                    | Image pull policy                                                                                     | `IfNotPresent`               |
| `pdb.create`                          | Specifies whether a pod disruption budget should be created                                           | `false`                      |
| `pdb.minAvailable`                    | Minimum number/percentage of pods that should remain scheduled                                        | `1`                          |
| `pdb.maxUnavailable`                  | Maximum number/percentage of pods that may be made unavailable                                        | `nil`                        |
| `serviceAccount.create`               | Specifies whether a service account should be created                                                 | `true`                       |
| `serviceAccount.annotations`          | Service account annotations                                                                           | `{}`                         |
| `serviceAccount.name`                 | The name of the service account to use (Generated using the `dolibarr.fullname` template if not set)  | `nil`                        |
| `podAnnotations`                      | Additional pod annotations                                                                            | `{}`                         |
| `podLabels`                           | Additional pod labels                                                                                 | `{}`                         |
| `podSecurityContext`                  | Pod security context                                                                                  | `{}`                         |
| `priorityClassName`                   | Priority class name                                                                                   | `nil`                        |
| `securityContext`                     | Container security context                                                                            | `{}`                         |
| `containerPorts.http`                 | Container port for HTTP                                                                               | `80`                         |
| `livenessProbe.enabled`               | Enable liveness probe                                                                                 | `true`                       |
| `livenessProbe.initialDelaySeconds`   | Delay before the liveness probe is initiated                                                          | `180`                        |
| `livenessProbe.periodSeconds`         | How often to perform the liveness probe                                                               | `10`                         |
| `livenessProbe.timeoutSeconds`        | When the liveness probe times out                                                                     | `1`                          |
| `livenessProbe.failureThreshold`      | Minimum consecutive failures for the liveness probe to be considered failed after having succeeded    | `3`                          |
| `livenessProbe.successThreshold`      | Minimum consecutive successes for the liveness probe to be considered successful after having failed  | `1`                          |
| `readinessProbe.enabled`              | Enable readiness probe                                                                                | `true`                       |
| `readinessProbe.initialDelaySeconds`  | Delay before the readiness probe is initiated                                                         | `0`                          |
| `readinessProbe.periodSeconds`        | How often to perform the readiness probe                                                              | `10`                         |
| `readinessProbe.timeoutSeconds`       | When the readiness probe times out                                                                    | `1`                          |
| `readinessProbe.failureThreshold`     | Minimum consecutive failures for the readiness probe to be considered failed after having succeeded   | `3`                          |
| `readinessProbe.successThreshold`     | Minimum consecutive successes for the readiness probe to be considered successful after having failed | `1`                          |
| `startupProbe.enabled`                | Enable startup probe                                                                                  | `false`                      |
| `startupProbe.initialDelaySeconds`    | Delay before the startup probe is initiated                                                           | `0`                          |
| `startupProbe.periodSeconds`          | How often to perform the startup probe                                                                | `10`                         |
| `startupProbe.timeoutSeconds`         | When the startup probe times out                                                                      | `1`                          |
| `startupProbe.failureThreshold`       | Minimum consecutive failures for the startup probe to be considered failed after having succeeded     | `3`                          |
| `startupProbe.successThreshold`       | Minimum consecutive successes for the startup probe to be considered successful after having failed   | `1`                          |
| `service.annotations`                 | Service annotations                                                                                   | `{}`                         |
| `service.type`                        | Service type                                                                                          | `ClusterIP`                  |
| `service.clusterIP`                   | Static cluster IP address or None for headless service when service type is ClusterIP                 | `nil`                        |
| `service.loadBalancerIP`              | Static load balancer IP address when service type is LoadBalancer                                     | `nil`                        |
| `service.loadBalancerSourceRanges`    | Source IP address ranges when service type is LoadBalancer                                            | `nil`                        |
| `service.externalTrafficPolicy`       | External traffic routing policy when service type is LoadBalancer or NodePort                         | `Cluster`                    |
| `service.ports.http`                  | Service port for HTTP                                                                                 | `80`                         |
| `service.nodePorts.http`              | Service node port for HTTP when service type is LoadBalancer or NodePort                              | `nil`                        |
| `ingress.enabled`                     | Enable ingress controller resource                                                                    | `false`                      |
| `ingress.ingressClassName`            | IngressClass that will be be used to implement the Ingress                                            | `""`                         |
| `ingress.pathType`                    | Ingress path type                                                                                     | `ImplementationSpecific`     |
| `ingress.annotations`                 | Ingress annotations                                                                                   | `{}`                         |
| `ingress.hosts[0].host`               | Hostname to your Dolibarr installation                                                                | `dolibarr.local`             |
| `ingress.hosts[0].paths`              | Paths within the url structure                                                                        | `["/"]`                      |
| `ingress.tls`                         | TLS configuration                                                                                     | `[]`                         |
| `resources`                           | CPU/Memory resource requests/limits                                                                   | `{}`                         |
| `nodeSelector`                        | Node labels for pod assignment                                                                        | `{}`                         |
| `tolerations`                         | Tolerations for pod assignment                                                                        | `[]`                         |
| `affinity`                            | Map of node/pod affinities                                                                            | `{}`                         |
| `extraArgs`                           | Additional container arguments                                                                        | `{}`                         |
| `extraEnvVars`                        | Additional container environment variables                                                            | `[]`                         |
| `extraEnvVarsCM`                      | Name of existing ConfigMap containing additional container environment variables                      | `nil`                        |
| `extraEnvVarsSecret`                  | Name of existing Secret containing additional container environment variables                         | `nil`                        |
| `init.securityContext`                | Init security context                                                                                 | `{}`                         |
| `init.resources`                      | Init CPU/Memory resource requests/limits                                                              | `{}`                         |
| `persistence.enabled`                 | Enable persistence using PVC                                                                          | `false`                      |
| `persistence.existingClaim`           | Name of an existing PVC for Dolibarr documents                                                        | `nil`                        |
| `persistence.existingClaimHtmlCustom` | Name of an existing PVC for Dolibarr installed / modified modules                                     | `nil`                        |
| `persistence.accessMode`              | PVC access mode                                                                                       | `ReadWriteOnce`              |
| `persistence.annotations`             | PVC annotations                                                                                       | `{}`                         |
| `persistence.size`                    | PVC size                                                                                              | `1Gi`                        |
| `persistence.storageClass`            | PVC storage class                                                                                     | `nil`                        |
| `dolibarr.admin.username`             | Administrator username                                                                                | `admin`                      |
| `dolibarr.admin.password`             | Administrator password                                                                                | `admin`                      |
| `dolibarr.externalUrl`                | External URL                                                                                          | `http://dolibarr.local`      |
| `dolibarr.cron.enabled`               | Enable cron for scheduled jobs                                                                        | `false`                      |
| `dolibarr.cron.username`              | Cron username                                                                                         | `admin`                      |
| `dolibarr.cron.securityKey`           | Cron security key                                                                                     | `""`                         |
| `existingSecret`                      | Name of existing Secret to use                                                                        | `""`                         |
| `existingSecretKeyAdminPassword`      | Name of the key in existing Secret that contains administrator password                               | `dolibarr-admin-password`    |
| `existingSecretKeyCronSecurityKey`    | Name of the key in existing Secret that contains cron security key                                    | `dolibarr-cron-security-key` |

### MariaDB parameters

| Name                                        | Description                                                       | Default            |
|---------------------------------------------|-------------------------------------------------------------------|--------------------|
| `mariadb.enabled`                           | Whether to use the MariaDB chart                                  | `true`             |
| `mariadb.architecture`                      | MariaDB architecture                                              | `standalone`       |
| `mariadb.auth.database`                     | MariaDB database                                                  | `dolibarr`         |
| `mariadb.auth.username`                     | MariaDB user                                                      | `dolibarr`         |
| `mariadb.auth.password`                     | MariaDB password                                                  | `dolibarr`         |
| `mariadb.auth.existingSecret`               | Name of existing Secret to use                                    | `""`               |
| `mariadb.primary.service.ports.mysql`       | MariaDB port                                                      | `3306`             |
| `mariadb.primary.persistence.existingClaim` | MariaDB existing persistent volume claim                          | `nil`              |
| `externalMariadb.enabled`                   | Whether to use an external MariaDB                                | `false`            |
| `externalMariadb.host`                      | External MariaDB host                                             | `mariadb`          |
| `externalMariadb.port`                      | External MariaDB port                                             | `3306`             |
| `externalMariadb.username`                  | External MariaDB user                                             | `dolibarr`         |
| `externalMariadb.password`                  | External MariaDB password                                         | `dolibarr`         |
| `externalMariadb.existingSecret`            | Name of existing Secret to use                                    | `""`               |
| `externalMariadb.existingSecretKeyPassword` | Name of the key in existing Secret that contains MariaDB password | `mariadb-password` |
| `externalMariadb.database`                  | External MariaDB database                                         | `dolibarr`         |

### Tests parameters

| Name                     | Description       | Default              |
|--------------------------|-------------------|----------------------|
| `tests.image.registry`   | Image registry    | `ghcr.io`            |
| `tests.image.repository` | Image repository  | `cowboysysop/pytest` |
| `tests.image.tag`        | Image tag         | `1.0.35`             |
| `tests.image.digest`     | Image digest      | `""`                 |
| `tests.image.pullPolicy` | Image pull policy | `IfNotPresent`       |

