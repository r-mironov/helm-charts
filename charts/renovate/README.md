# renovate

![Version: 25.67.0+1](https://img.shields.io/badge/Version-25.67.0+1-informational?style=flat-square) ![AppVersion: 25.67.0](https://img.shields.io/badge/AppVersion-25.67.0-informational?style=flat-square)

Universal dependency update tool that fits into your workflows.

**Homepage:** <https://github.com/renovatebot/renovate>

## Installation

### Add Helm repository

```shell
helm repo add renovate https://docs.renovatebot.com/helm-charts
helm repo update
```

## Install Renovate chart

Using config from a file:

```bash
helm install --generate-name --set-file renovate.config=config.json renovate/renovate
```

Using config from a string:

```bash
helm install --generate-name --set renovate.config='\{\"token\":\"...\"\}' renovate/renovate
```

**NOTE**: `renovate.config` must be a valid Renovate [self-hosted configuration](https://docs.renovatebot.com/self-hosted-configuration/)

## Configuration

The following table lists the configurable parameters of the chart and the default values.

## Values

| Key | Type | Default | Description |
|-----|------|---------|-------------|
| apiVersionOverrides.cronjob | string | `""` | String to override apiVersion of cronjob rendered by this helm chart |
| cronjob.annotations | object | `{}` |  |
| cronjob.concurrencyPolicy | string | `""` |  |
| cronjob.failedJobsHistoryLimit | string | `""` |  |
| cronjob.jobBackoffLimit | string | `""` |  |
| cronjob.jobRestartPolicy | string | `"Never"` |  |
| cronjob.labels | object | `{}` |  |
| cronjob.schedule | string | `"0 1 * * *"` |  |
| cronjob.successfulJobsHistoryLimit | string | `""` |  |
| dind.enabled | bool | `false` | Enable dind sidecar usage? |
| dind.image.pullPolicy | string | `"IfNotPresent"` |  |
| dind.image.repository | string | `"docker.io/library/docker"` |  |
| dind.image.tag | string | `"20.10.7-dind"` |  |
| dind.slim.enabled | bool | `true` | Do not add `-slim` suffix to image tag when using dind |
| env | object | `{}` |  |
| envFrom | list | `[]` |  |
| existingSecret | string | `""` |  |
| extraConfigmaps | list | `[]` | Additional configmaps. A generated configMap name is: "renovate.fullname" + "extra" + name(below) e.g. renovate-netrc-config |
| extraVolumeMounts | list | `[]` | Additional volumeMounts to the container |
| extraVolumes | list | `[]` | Additional volumes to the pod |
| image.pullPolicy | string | `"IfNotPresent"` |  |
| image.repository | string | `"renovate/renovate"` |  |
| image.tag | string | `"25.67.0"` |  |
| imagePullSecrets | object | `{}` |  |
| pod.annotations | object | `{}` |  |
| pod.labels | object | `{}` |  |
| redis.cluster.enabled | bool | `false` | Do not use clustering, not supported by renovate |
| redis.enabled | bool | `false` | Enable the Redis subchart? |
| redis.nameOverride | string | `"redis"` |  |
| redis.usePassword | bool | `false` |  |
| renovate.config | string | `""` | Inline global renovate config.json |
| renovate.existingConfigFile | string | `""` | Custom exiting global renovate config |
| resources | object | `{}` |  |
| secrets | object | `{}` |  |
| serviceAccount.annotations | object | `{}` |  |
| serviceAccount.create | bool | `false` |  |
| serviceAccount.name | string | `""` |  |
| ssh_config.config | string | `""` |  |
| ssh_config.enabled | bool | `false` |  |
| ssh_config.existingSecret | string | `""` |  |
| ssh_config.id_rsa | string | `""` |  |
| ssh_config.id_rsa_pub | string | `""` |  |

## Docker in Docker configuration

When `dind.enabled` is set to `true`, a Docker in Docker container will run as a sidecar to supply a Docker daemon to the RenovateBot container. This allows the configuration `binarySource` to be set to `docker`, which is the default configuration in the slim Docker images.

The slim suffix will be added to the tag if not present. To disable this behaviour, set `dind.slim.enabled` to `false`.
