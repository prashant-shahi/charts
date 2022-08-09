# signoz

![Version: 0.2.4](https://img.shields.io/badge/Version-0.2.4-informational?style=flat-square) ![Type: application](https://img.shields.io/badge/Type-application-informational?style=flat-square) ![AppVersion: 0.10.1](https://img.shields.io/badge/AppVersion-0.10.1-informational?style=flat-square)

SigNoz Observability Platform Helm Chart

**Homepage:** <https://signoz.io/>

## Maintainers

| Name | Email | Url |
| ---- | ------ | --- |
| SigNoz | <hello@signoz.io> | <https://signoz.io> |
| prashant-shahi | <prashant@signoz.io> | <https://prashantshahi.dev> |

## Source Code

* <https://github.com/signoz/charts/>
* <https://github.com/signoz/signoz>
* <https://github.com/signoz/alertmanager>
* <https://github.com/signoz/opentelemetry-collector-contrib>

## Requirements

| Repository | Name | Version |
|------------|------|---------|
| https://signoz.github.io/charts | clickhouse | 23.4.0 |

## Values

| Key | Type | Default | Description |
|-----|------|---------|-------------|
| global.image.registry | string | `nil` | Overrides the Docker registry globally for all images |
| global.storageClass | string | `nil` | Overrides the storage class for all PVC with persistence enabled. |
| fullnameOverride | string | `""` | SigNoz chart full name override |
| clickhouse.cloud | string | `"other"` | Cloud service being deployed on (example: `aws`, `azure`, `gcp`, `hcloud`, `other`). Based on the cloud, storage class for the persistent volume is selected. When set to 'aws' or 'gcp', new expandible storage class is created. When set to something else or not set, the default storage class (if any) from the k8s cluster is selected. |
| clickhouse.zookeeper.enabled | bool | `true` | Whether to install zookeeper. If false, `clickhouse.externalZookeeper` must be set. |
| clickhouse.nameOverride | string | `""` | Name override for clickhouse |
| clickhouse.fullnameOverride | string | `""` | Fullname override for clickhouse |
| clickhouse.enabled | bool | `true` | Whether to install clickhouse. If false, `clickhouse.host` must be set |
| clickhouse.namespace | string | `""` | Which namespace to install `clickhouse-operator` to (defaults to namespace chart is installed to) |
| clickhouse.cluster | string | `"cluster"` | Clickhouse cluster |
| clickhouse.database | string | `"signoz_metrics"` | Clickhouse database (SigNoz Metrics) |
| clickhouse.traceDatabase | string | `"signoz_traces"` | Clickhouse trace database (SigNoz Traces) |
| clickhouse.user | string | `"admin"` | Clickhouse user |
| clickhouse.password | string | `"27ff0399-0d3a-4bd8-919d-17c2181e6fb9"` | Clickhouse password |
| clickhouse.image | object | `{"pullPolicy":"IfNotPresent","registry":"docker.io","repository":"clickhouse/clickhouse-server","tag":"22.4.5-alpine"}` | Clickhouse image |
| clickhouse.image.registry | string | `"docker.io"` | Clickhouse image registry to use. |
| clickhouse.image.repository | string | `"clickhouse/clickhouse-server"` | Clickhouse image repository to use. |
| clickhouse.image.tag | string | `"22.4.5-alpine"` | Clickhouse image tag to use (example: `21.8`). SigNoz is not always tested with latest version of ClickHouse. Only if you know what you are doing, proceed with overriding. |
| clickhouse.image.pullPolicy | string | `"IfNotPresent"` | Clickhouse image pull policy. |
| clickhouse.service.annotations | object | `{}` | Annotations to use by service associated to Clickhouse instance |
| clickhouse.service.type | string | `"ClusterIP"` | Service Type: LoadBalancer (allows external access) or NodePort (more secure, no extra cost) |
| clickhouse.service.httpPort | int | `8123` | Clickhouse HTTP port |
| clickhouse.service.tcpPort | int | `9000` | Clickhouse TCP port |
| clickhouse.secure | bool | `false` | Whether to use TLS connection connecting to ClickHouse |
| clickhouse.verify | bool | `false` | Whether to verify TLS certificate on connection to ClickHouse |
| clickhouse.externalZookeeper | object | `{}` | URL for zookeeper. |
| clickhouse.tolerations | list | `[]` | Toleration labels for clickhouse pod assignment |
| clickhouse.affinity | object | `{}` | Affinity settings for clickhouse pod |
| clickhouse.resources | object | `{}` | Clickhouse resource requests/limits. See more at http://kubernetes.io/docs/user-guide/compute-resources/ |
| clickhouse.securityContext | object | `{"enabled":true,"fsGroup":101,"runAsGroup":101,"runAsUser":101}` | Security context for Clickhouse node |
| clickhouse.useNodeSelector | bool | `false` | If enabled, operator will prefer k8s nodes with tag `clickhouse:true` |
| clickhouse.allowedNetworkIps | list | `["10.0.0.0/8","172.16.0.0/12","192.168.0.0/16"]` | An allowlist of IP addresses or network masks the ClickHouse user is allowed to access from. By default anything within a private network will be allowed. This should suffice for most use case although to expose to other networks you will need to update this setting.  |
| clickhouse.persistence.enabled | bool | `true` | Enable data persistence using PVC for ClickHouseDB data. |
| clickhouse.persistence.existingClaim | string | `""` | Use a manually managed Persistent Volume and Claim. If defined, PVC must be created manually before volume will be bound.  |
| clickhouse.persistence.storageClass | string | `nil` | Persistent Volume Storage Class to use. If defined, `storageClassName: <storageClass>`. If set to "-", `storageClassName: ""`, which disables dynamic provisioning If undefined (the default) or set to `null`, no storageClassName spec is set, choosing the default provisioner.  |
| clickhouse.persistence.accessModes | list | `["ReadWriteOnce"]` | Access Modes for persistent volume |
| clickhouse.persistence.size | string | `"20Gi"` | Persistent Volume size |
| clickhouse.profiles | object | `{}` | Clickhouse user profile configuration. You can use this to override profile settings, for example `default/max_memory_usage: 40000000000` For the full list of settings, see: - https://clickhouse.com/docs/en/operations/settings/settings-profiles/ - https://clickhouse.com/docs/en/operations/settings/settings/  |
| clickhouse.defaultProfiles | object | `{"default/allow_experimental_window_functions":"1","default/allow_nondeterministic_mutations":"1"}` | Default user profile configuration for Clickhouse. !!! Please DO NOT override this !!! |
| clickhouse.layout | object | `{"replicasCount":1,"shardsCount":1}` | Clickhouse cluster layout. (Experimental, use at own risk) For a full list of options, see https://github.com/Altinity/clickhouse-operator/blob/master/docs/custom_resource_explained.md section on clusters and layouts.  |
| clickhouse.settings | object | `{"prometheus/endpoint":"/metrics","prometheus/port":9363}` | ClickHouse settings configuration. You can use this to override settings, for example `prometheus/port: 9363` For the full list of settings, see: - https://clickhouse.com/docs/en/operations/settings/settings/  |
| clickhouse.defaultSettings | object | `{"format_schema_path":"/etc/clickhouse-server/config.d/"}` | Default settings configuration for ClickHouse. !!! Please DO NOT override this !!! |
| clickhouse.podAnnotations | object | `{"signoz.io/path":"/metrics","signoz.io/port":"9363","signoz.io/scrape":"true"}` | ClickHouse pod(s) annotation. |
| clickhouse.coldStorage.enabled | bool | `false` | Whether to enable S3 cold storage |
| clickhouse.coldStorage.defaultKeepFreeSpaceBytes | string | `"10485760"` | Reserve free space on default disk (in bytes) |
| clickhouse.coldStorage.endpoint | string | `"https://<bucket-name>.s3.amazonaws.com/data/"` | AWS S3 endpoint |
| clickhouse.coldStorage.role.enabled | bool | `false` | Whether to enable AWS IAM ARN role. |
| clickhouse.coldStorage.role.annotations | object | `{"eks.amazonaws.com/role-arn":"arn:aws:iam::******:role/*****"}` | Annotations to use by service account associated to Clickhouse instance |
| clickhouse.coldStorage.accessKey | string | `"<access_key_id>"` | AWS Access Key |
| clickhouse.coldStorage.secretAccess | string | `"<secret_access_key>"` | AWS Secret Access Key |
| clickhouse.installCustomStorageClass | bool | `false` | When the `installCustomStorageClass` is enabled with `cloud` set as `gcp` or `aws`, it creates custom storage class with volume expansion permission. |
| clickhouse.clickhouseOperator.nodeSelector | object | `{}` | ClickhouseOperator node selector |
| externalClickhouse.host | string | `nil` | Host of the external cluster. |
| externalClickhouse.cluster | string | `"cluster"` | Name of the external cluster to run DDL queries on. |
| externalClickhouse.database | string | `"signoz_metrics"` | Database name for the external cluster |
| externalClickhouse.traceDatabase | string | `"signoz_traces"` | Clickhouse trace database (SigNoz Traces) |
| externalClickhouse.user | string | `""` | User name for the external cluster to connect to the external cluster as |
| externalClickhouse.password | string | `""` | Password for the cluster. Ignored if existingClickhouse.existingSecret is set |
| externalClickhouse.existingSecret | string | `nil` | Name of an existing Kubernetes secret object containing the password |
| externalClickhouse.existingSecretPasswordKey | string | `nil` | Name of the key pointing to the password in your Kubernetes secret |
| externalClickhouse.secure | bool | `false` | Whether to use TLS connection connecting to ClickHouse |
| externalClickhouse.verify | bool | `false` | Whether to verify TLS connection connecting to ClickHouse |
| externalClickhouse.httpPort | int | `8123` | HTTP port of Clickhouse |
| externalClickhouse.tcpPort | int | `9000` | TCP port of Clickhouse |
| queryService.name | string | `"query-service"` |  |
| queryService.replicaCount | int | `1` |  |
| queryService.image.registry | string | `"docker.io"` |  |
| queryService.image.repository | string | `"signoz/query-service"` |  |
| queryService.image.tag | string | `"0.10.1"` |  |
| queryService.image.pullPolicy | string | `"IfNotPresent"` |  |
| queryService.imagePullSecrets | list | `[]` |  |
| queryService.serviceAccount.create | bool | `true` |  |
| queryService.serviceAccount.annotations | object | `{}` |  |
| queryService.serviceAccount.name | string | `nil` |  |
| queryService.initContainers.init.enabled | bool | `true` |  |
| queryService.initContainers.init.image.registry | string | `"docker.io"` |  |
| queryService.initContainers.init.image.repository | string | `"busybox"` |  |
| queryService.initContainers.init.image.tag | float | `1.35` |  |
| queryService.initContainers.init.image.pullPolicy | string | `"IfNotPresent"` |  |
| queryService.initContainers.init.command.delay | int | `5` |  |
| queryService.initContainers.init.command.endpoint | string | `"/ping"` |  |
| queryService.initContainers.init.command.waitMessage | string | `"waiting for clickhouseDB"` |  |
| queryService.initContainers.init.command.doneMessage | string | `"clickhouse ready, starting query service now"` |  |
| queryService.configVars.storage | string | `"clickhouse"` |  |
| queryService.configVars.goDebug | string | `"netdns=go"` |  |
| queryService.configVars.telemetryEnabled | bool | `true` |  |
| queryService.configVars.deploymentType | string | `"kubernetes-helm"` |  |
| queryService.podSecurityContext | object | `{}` |  |
| queryService.securityContext | object | `{}` |  |
| queryService.service.annotations | object | `{}` | Annotations to use by service associated to Query-Service |
| queryService.service.type | string | `"ClusterIP"` | Service Type: LoadBalancer (allows external access) or NodePort (more secure, no extra cost) |
| queryService.service.port | int | `8080` | Query-Service HTTP port |
| queryService.service.internalPort | int | `8085` | Query-Service Internal port |
| queryService.ingress.enabled | bool | `false` | Enable ingress for Query-Service |
| queryService.ingress.className | string | `""` | Ingress Class Name to be used to identify ingress controllers |
| queryService.ingress.annotations | object | `{}` | Annotations to Query-Service Ingress |
| queryService.ingress.hosts | list | `[{"host":"query-service.domain.com","paths":[{"path":"/","pathType":"ImplementationSpecific","port":8080}]}]` | Query-Service Ingress Host names with their path details |
| queryService.ingress.tls | list | `[]` | Query-Service Ingress TLS |
| queryService.resources.requests.cpu | string | `"200m"` |  |
| queryService.resources.requests.memory | string | `"300Mi"` |  |
| queryService.resources.limits.cpu | string | `"750m"` |  |
| queryService.resources.limits.memory | string | `"1000Mi"` |  |
| queryService.nodeSelector | object | `{}` |  |
| queryService.tolerations | list | `[]` |  |
| queryService.affinity | object | `{}` |  |
| queryService.persistence.enabled | bool | `true` | Enable data persistence using PVC for SQLiteDB data. |
| queryService.persistence.storageClass | string | `nil` | Persistent Volume Storage Class to use. If defined, `storageClassName: <storageClass>`. If set to "-", `storageClassName: ""`, which disables dynamic provisioning If undefined (the default) or set to `null`, no storageClassName spec is set, choosing the default provisioner.  |
| queryService.persistence.accessModes | list | `["ReadWriteOnce"]` | Access Modes for persistent volume |
| queryService.persistence.size | string | `"1Gi"` | Persistent Volume size |
| frontend.name | string | `"frontend"` |  |
| frontend.replicaCount | int | `1` |  |
| frontend.image.registry | string | `"docker.io"` |  |
| frontend.image.repository | string | `"signoz/frontend"` |  |
| frontend.image.tag | string | `"0.10.1"` |  |
| frontend.image.pullPolicy | string | `"IfNotPresent"` |  |
| frontend.imagePullSecrets | list | `[]` |  |
| frontend.serviceAccount.create | bool | `true` |  |
| frontend.serviceAccount.annotations | object | `{}` |  |
| frontend.serviceAccount.name | string | `nil` |  |
| frontend.initContainers.init.enabled | bool | `true` |  |
| frontend.initContainers.init.image.registry | string | `"docker.io"` |  |
| frontend.initContainers.init.image.repository | string | `"busybox"` |  |
| frontend.initContainers.init.image.tag | float | `1.35` |  |
| frontend.initContainers.init.image.pullPolicy | string | `"IfNotPresent"` |  |
| frontend.initContainers.init.command.delay | int | `5` |  |
| frontend.initContainers.init.command.endpoint | string | `"/api/v1/version"` |  |
| frontend.initContainers.init.command.waitMessage | string | `"waiting for query-service"` |  |
| frontend.initContainers.init.command.doneMessage | string | `"clickhouse ready, starting frontend now"` |  |
| frontend.autoscaling.enabled | bool | `false` |  |
| frontend.autoscaling.minReplicas | int | `1` |  |
| frontend.autoscaling.maxReplicas | int | `11` |  |
| frontend.autoscaling.targetCPUUtilizationPercentage | int | `50` |  |
| frontend.autoscaling.targetMemoryUtilizationPercentage | int | `50` |  |
| frontend.autoscaling.behavior | object | `{}` |  |
| frontend.autoscaling.autoscalingTemplate | list | `[]` |  |
| frontend.autoscaling.keda.enabled | bool | `false` |  |
| frontend.autoscaling.keda.pollingInterval | string | `"30"` |  |
| frontend.autoscaling.keda.cooldownPeriod | string | `"300"` |  |
| frontend.autoscaling.keda.minReplicaCount | string | `"1"` |  |
| frontend.autoscaling.keda.maxReplicaCount | string | `"5"` |  |
| frontend.autoscaling.keda.triggers[0].type | string | `"memory"` |  |
| frontend.autoscaling.keda.triggers[0].metadata.type | string | `"Utilization"` |  |
| frontend.autoscaling.keda.triggers[0].metadata.value | string | `"80"` |  |
| frontend.autoscaling.keda.triggers[1].type | string | `"cpu"` |  |
| frontend.autoscaling.keda.triggers[1].metadata.type | string | `"Utilization"` |  |
| frontend.autoscaling.keda.triggers[1].metadata.value | string | `"80"` |  |
| frontend.configVars | object | `{}` |  |
| frontend.podSecurityContext | object | `{}` |  |
| frontend.securityContext | object | `{}` |  |
| frontend.service.annotations | object | `{}` | Annotations to use by service associated to Frontend |
| frontend.service.type | string | `"ClusterIP"` | Service Type: LoadBalancer (allows external access) or NodePort (more secure, no extra cost) |
| frontend.service.port | int | `3301` | Frontend HTTP port |
| frontend.ingress.enabled | bool | `false` | Enable ingress for Frontend |
| frontend.ingress.className | string | `""` | Ingress Class Name to be used to identify ingress controllers |
| frontend.ingress.annotations | object | `{}` | Annotations to Frontend Ingress |
| frontend.ingress.hosts | list | `[{"host":"frontend.domain.com","paths":[{"path":"/","pathType":"ImplementationSpecific","port":3301}]}]` | Frontend Ingress Host names with their path details |
| frontend.ingress.tls | list | `[]` | Frontend Ingress TLS |
| frontend.resources.requests.cpu | string | `"100m"` |  |
| frontend.resources.requests.memory | string | `"100Mi"` |  |
| frontend.resources.limits.cpu | string | `"200m"` |  |
| frontend.resources.limits.memory | string | `"200Mi"` |  |
| frontend.nodeSelector | object | `{}` |  |
| frontend.tolerations | list | `[]` |  |
| frontend.affinity | object | `{}` |  |
| alertmanager.name | string | `"alertmanager"` |  |
| alertmanager.replicaCount | int | `1` |  |
| alertmanager.image.registry | string | `"docker.io"` |  |
| alertmanager.image.repository | string | `"signoz/alertmanager"` |  |
| alertmanager.image.pullPolicy | string | `"IfNotPresent"` |  |
| alertmanager.image.tag | string | `"0.23.0-0.2"` |  |
| alertmanager.command | list | `[]` |  |
| alertmanager.extraArgs | object | `{}` |  |
| alertmanager.imagePullSecrets | list | `[]` |  |
| alertmanager.service.annotations | object | `{}` | Annotations to use by service associated to Alertmanager |
| alertmanager.service.type | string | `"ClusterIP"` | Service Type: LoadBalancer (allows external access) or NodePort (more secure, no extra cost) |
| alertmanager.service.port | int | `9093` | Alertmanager HTTP port |
| alertmanager.service.nodePort | string | `nil` | Set this to you want to force a specific nodePort. Must be use with service.type=NodePort |
| alertmanager.serviceAccount.create | bool | `true` |  |
| alertmanager.serviceAccount.annotations | object | `{}` |  |
| alertmanager.serviceAccount.name | string | `nil` |  |
| alertmanager.initContainers.init.enabled | bool | `true` |  |
| alertmanager.initContainers.init.image.registry | string | `"docker.io"` |  |
| alertmanager.initContainers.init.image.repository | string | `"busybox"` |  |
| alertmanager.initContainers.init.image.tag | float | `1.35` |  |
| alertmanager.initContainers.init.image.pullPolicy | string | `"IfNotPresent"` |  |
| alertmanager.initContainers.init.command.delay | int | `5` |  |
| alertmanager.initContainers.init.command.endpoint | string | `"/api/v1/version"` |  |
| alertmanager.initContainers.init.command.waitMessage | string | `"waiting for query-service"` |  |
| alertmanager.initContainers.init.command.doneMessage | string | `"clickhouse ready, starting alertmanager now"` |  |
| alertmanager.podSecurityContext.fsGroup | int | `65534` |  |
| alertmanager.dnsConfig | object | `{}` |  |
| alertmanager.securityContext.runAsUser | int | `65534` |  |
| alertmanager.securityContext.runAsNonRoot | bool | `true` |  |
| alertmanager.securityContext.runAsGroup | int | `65534` |  |
| alertmanager.additionalPeers | list | `[]` |  |
| alertmanager.livenessProbe.httpGet.path | string | `"/"` |  |
| alertmanager.livenessProbe.httpGet.port | string | `"http"` |  |
| alertmanager.readinessProbe.httpGet.path | string | `"/"` |  |
| alertmanager.readinessProbe.httpGet.port | string | `"http"` |  |
| alertmanager.ingress.enabled | bool | `false` | Enable ingress for Alertmanager |
| alertmanager.ingress.className | string | `""` | Ingress Class Name to be used to identify ingress controllers |
| alertmanager.ingress.annotations | object | `{}` | Annotations to Alertmanager Ingress |
| alertmanager.ingress.hosts | list | `[{"host":"alertmanager.domain.com","paths":[{"path":"/","pathType":"ImplementationSpecific","port":9093}]}]` | Alertmanager Ingress Host names with their path details |
| alertmanager.ingress.tls | list | `[]` | Alertmanager Ingress TLS |
| alertmanager.resources.requests.cpu | string | `"100m"` |  |
| alertmanager.resources.requests.memory | string | `"100Mi"` |  |
| alertmanager.resources.limits.cpu | string | `"200m"` |  |
| alertmanager.resources.limits.memory | string | `"200Mi"` |  |
| alertmanager.nodeSelector | object | `{}` |  |
| alertmanager.tolerations | list | `[]` |  |
| alertmanager.affinity | object | `{}` |  |
| alertmanager.statefulSet.annotations | object | `{}` |  |
| alertmanager.podAnnotations | object | `{}` |  |
| alertmanager.podLabels | object | `{}` |  |
| alertmanager.podDisruptionBudget | object | `{}` |  |
| alertmanager.persistence.enabled | bool | `true` | Enable data persistence using PVC for Alertmanager data. |
| alertmanager.persistence.storageClass | string | `nil` | Persistent Volume Storage Class to use. If defined, `storageClassName: <storageClass>`. If set to "-", `storageClassName: ""`, which disables dynamic provisioning If undefined (the default) or set to `null`, no storageClassName spec is set, choosing the default provisioner.  |
| alertmanager.persistence.accessModes | list | `["ReadWriteOnce"]` | Access Modes for persistent volume |
| alertmanager.persistence.size | string | `"100Mi"` | Persistent Volume size |
| alertmanager.configmapReload.enabled | bool | `false` |  |
| alertmanager.configmapReload.name | string | `"configmap-reload"` |  |
| alertmanager.configmapReload.image.repository | string | `"jimmidyson/configmap-reload"` |  |
| alertmanager.configmapReload.image.tag | string | `"v0.5.0"` |  |
| alertmanager.configmapReload.image.pullPolicy | string | `"IfNotPresent"` |  |
| alertmanager.configmapReload.resources | object | `{}` |  |
| otelCollector.name | string | `"otel-collector"` |  |
| otelCollector.image.registry | string | `"docker.io"` |  |
| otelCollector.image.repository | string | `"signoz/otelcontribcol"` |  |
| otelCollector.image.tag | string | `"0.45.1-1.3"` |  |
| otelCollector.image.pullPolicy | string | `"Always"` |  |
| otelCollector.imagePullSecrets | list | `[]` |  |
| otelCollector.service.annotations | object | `{}` | Annotations to use by service associated to OtelCollector |
| otelCollector.service.type | string | `"ClusterIP"` | Service Type: LoadBalancer (allows external access) or NodePort (more secure, no extra cost) |
| otelCollector.serviceAccount.create | bool | `true` |  |
| otelCollector.serviceAccount.annotations | object | `{}` |  |
| otelCollector.serviceAccount.name | string | `nil` |  |
| otelCollector.annotations | object | `{}` | OtelColector Deployment annotation. |
| otelCollector.podAnnotations | object | `{"internal.signoz.io/path":"/metrics","internal.signoz.io/port":"8889","internal.signoz.io/scrape":"true","signoz.io/path":"/metrics","signoz.io/port":"8888","signoz.io/scrape":"true"}` | OtelColector pod(s) annotation. |
| otelCollector.minReadySeconds | int | `5` |  |
| otelCollector.progressDeadlineSeconds | int | `120` |  |
| otelCollector.replicaCount | int | `1` |  |
| otelCollector.ballastSizeMib | int | `683` |  |
| otelCollector.initContainers.init.enabled | bool | `true` |  |
| otelCollector.initContainers.init.image.registry | string | `"docker.io"` |  |
| otelCollector.initContainers.init.image.repository | string | `"busybox"` |  |
| otelCollector.initContainers.init.image.tag | float | `1.35` |  |
| otelCollector.initContainers.init.image.pullPolicy | string | `"IfNotPresent"` |  |
| otelCollector.initContainers.init.command.delay | int | `5` |  |
| otelCollector.initContainers.init.command.endpoint | string | `"/ping"` |  |
| otelCollector.initContainers.init.command.waitMessage | string | `"waiting for clickhouseDB"` |  |
| otelCollector.initContainers.init.command.doneMessage | string | `"clickhouse ready, starting otel collector now"` |  |
| otelCollector.ports.otlp.enabled | bool | `true` | Whether to enable service port for OTLP gRPC |
| otelCollector.ports.otlp.containerPort | int | `4317` | Container port for OTLP gRPC |
| otelCollector.ports.otlp.servicePort | int | `4317` | Service port for OTLP gRPC |
| otelCollector.ports.otlp.protocol | string | `"TCP"` | Protocol to use for OTLP gRPC |
| otelCollector.ports.otlp-http.enabled | bool | `true` | Whether to enable service port for OTLP HTTP |
| otelCollector.ports.otlp-http.containerPort | int | `4318` | Container port for OTLP HTTP |
| otelCollector.ports.otlp-http.servicePort | int | `4318` | Service port for OTLP HTTP |
| otelCollector.ports.otlp-http.protocol | string | `"TCP"` | Protocol to use for OTLP HTTP |
| otelCollector.ports.jaeger-compact.enabled | bool | `false` | Whether to enable service port for Jaeger Compact |
| otelCollector.ports.jaeger-compact.containerPort | int | `6831` | Container port for Jaeger Compact |
| otelCollector.ports.jaeger-compact.servicePort | int | `6831` | Service port for Jaeger Compact |
| otelCollector.ports.jaeger-compact.protocol | string | `"UDP"` | Protocol to use for Jaeger Compact |
| otelCollector.ports.jaeger-thrift.enabled | bool | `true` | Whether to enable service port for Jaeger Thrift HTTP |
| otelCollector.ports.jaeger-thrift.containerPort | int | `14268` | Container port for Jaeger Thrift |
| otelCollector.ports.jaeger-thrift.servicePort | int | `14268` | Service port for Jaeger Thrift |
| otelCollector.ports.jaeger-thrift.protocol | string | `"TCP"` | Protocol to use for Jaeger Thrift |
| otelCollector.ports.jaeger-grpc.enabled | bool | `true` | Whether to enable service port for Jaeger gRPC |
| otelCollector.ports.jaeger-grpc.containerPort | int | `14250` | Container port for Jaeger gRPC |
| otelCollector.ports.jaeger-grpc.servicePort | int | `14250` | Service port for Jaeger gRPC |
| otelCollector.ports.jaeger-grpc.protocol | string | `"TCP"` | Protocol to use for Jaeger gRPC |
| otelCollector.ports.zipkin.enabled | bool | `false` | Whether to enable service port for Zipkin |
| otelCollector.ports.zipkin.containerPort | int | `9411` | Container port for Zipkin |
| otelCollector.ports.zipkin.servicePort | int | `9411` | Service port for Zipkin |
| otelCollector.ports.zipkin.protocol | string | `"TCP"` | Protocol to use for Zipkin |
| otelCollector.ports.prometheus-metrics.enabled | bool | `false` | Whether to enable service port for SigNoz exported prometheus metrics |
| otelCollector.ports.prometheus-metrics.containerPort | int | `8889` | Container port for SigNoz exported prometheus metrics |
| otelCollector.ports.prometheus-metrics.servicePort | int | `8889` | Service port for SigNoz exported prometheus metrics |
| otelCollector.ports.prometheus-metrics.protocol | string | `"TCP"` | Protocol to use for SigNoz exported prometheus metrics |
| otelCollector.ports.metrics.enabled | bool | `false` | Whether to enable service port for internal metrics |
| otelCollector.ports.metrics.containerPort | int | `8888` | Container port for internal metrics |
| otelCollector.ports.metrics.servicePort | int | `8888` | Service port for internal metrics |
| otelCollector.ports.metrics.protocol | string | `"TCP"` | Protocol to use for internal metrics |
| otelCollector.ports.zpages.enabled | bool | `false` | Whether to enable service port for ZPages |
| otelCollector.ports.zpages.containerPort | int | `55679` | Container port for Zpages |
| otelCollector.ports.zpages.servicePort | int | `55679` | Service port for Zpages |
| otelCollector.ports.zpages.protocol | string | `"TCP"` | Protocol to use for Zpages |
| otelCollector.livenessProbe.enabled | bool | `false` |  |
| otelCollector.livenessProbe.port | int | `13133` |  |
| otelCollector.livenessProbe.path | string | `"/"` |  |
| otelCollector.livenessProbe.initialDelaySeconds | int | `5` |  |
| otelCollector.livenessProbe.periodSeconds | int | `10` |  |
| otelCollector.livenessProbe.timeoutSeconds | int | `5` |  |
| otelCollector.livenessProbe.failureThreshold | int | `6` |  |
| otelCollector.livenessProbe.successThreshold | int | `1` |  |
| otelCollector.readinessProbe.enabled | bool | `false` |  |
| otelCollector.readinessProbe.port | int | `13133` |  |
| otelCollector.readinessProbe.path | string | `"/"` |  |
| otelCollector.readinessProbe.initialDelaySeconds | int | `5` |  |
| otelCollector.readinessProbe.periodSeconds | int | `10` |  |
| otelCollector.readinessProbe.timeoutSeconds | int | `5` |  |
| otelCollector.readinessProbe.failureThreshold | int | `6` |  |
| otelCollector.readinessProbe.successThreshold | int | `1` |  |
| otelCollector.customLivenessProbe | object | `{}` |  |
| otelCollector.customReadinessProbe | object | `{}` |  |
| otelCollector.ingress.enabled | bool | `false` | Enable ingress for OtelCollector |
| otelCollector.ingress.className | string | `""` | Ingress Class Name to be used to identify ingress controllers |
| otelCollector.ingress.annotations | object | `{}` | Annotations to OtelCollector Ingress |
| otelCollector.ingress.hosts | list | `[{"host":"otelcollector.domain.com","paths":[{"path":"/","pathType":"ImplementationSpecific","port":4318}]}]` | OtelCollector Ingress Host names with their path details |
| otelCollector.ingress.tls | list | `[]` | OtelCollector Ingress TLS |
| otelCollector.resources.requests.cpu | string | `"200m"` |  |
| otelCollector.resources.requests.memory | string | `"400Mi"` |  |
| otelCollector.resources.limits.cpu | string | `"1000m"` |  |
| otelCollector.resources.limits.memory | string | `"2Gi"` |  |
| otelCollector.nodeSelector | object | `{}` |  |
| otelCollector.tolerations | list | `[]` |  |
| otelCollector.affinity | object | `{}` |  |
| otelCollector.autoscaling.enabled | bool | `false` |  |
| otelCollector.autoscaling.minReplicas | int | `1` |  |
| otelCollector.autoscaling.maxReplicas | int | `11` |  |
| otelCollector.autoscaling.targetCPUUtilizationPercentage | int | `50` |  |
| otelCollector.autoscaling.targetMemoryUtilizationPercentage | int | `50` |  |
| otelCollector.autoscaling.behavior | object | `{}` |  |
| otelCollector.autoscaling.autoscalingTemplate | list | `[]` |  |
| otelCollector.autoscaling.keda.enabled | bool | `false` |  |
| otelCollector.autoscaling.keda.pollingInterval | string | `"30"` |  |
| otelCollector.autoscaling.keda.cooldownPeriod | string | `"300"` |  |
| otelCollector.autoscaling.keda.minReplicaCount | string | `"1"` |  |
| otelCollector.autoscaling.keda.maxReplicaCount | string | `"5"` |  |
| otelCollector.autoscaling.keda.triggers[0].type | string | `"memory"` |  |
| otelCollector.autoscaling.keda.triggers[0].metadata.type | string | `"Utilization"` |  |
| otelCollector.autoscaling.keda.triggers[0].metadata.value | string | `"80"` |  |
| otelCollector.autoscaling.keda.triggers[1].type | string | `"cpu"` |  |
| otelCollector.autoscaling.keda.triggers[1].metadata.type | string | `"Utilization"` |  |
| otelCollector.autoscaling.keda.triggers[1].metadata.value | string | `"80"` |  |
| otelCollector.config | object | See `values.yaml` for defaults | Configurations for OtelCollector |
| otelCollectorMetrics.name | string | `"otel-collector-metrics"` |  |
| otelCollectorMetrics.image.registry | string | `"docker.io"` |  |
| otelCollectorMetrics.image.repository | string | `"signoz/otelcontribcol"` |  |
| otelCollectorMetrics.image.tag | string | `"0.45.1-1.3"` |  |
| otelCollectorMetrics.image.pullPolicy | string | `"Always"` |  |
| otelCollectorMetrics.imagePullSecrets | list | `[]` |  |
| otelCollectorMetrics.service.annotations | object | `{}` | Annotations to use by service associated to OtelCollectorMetrics |
| otelCollectorMetrics.service.type | string | `"ClusterIP"` | Service Type: LoadBalancer (allows external access) or NodePort (more secure, no extra cost) |
| otelCollectorMetrics.serviceAccount.create | bool | `true` |  |
| otelCollectorMetrics.serviceAccount.annotations | object | `{}` |  |
| otelCollectorMetrics.serviceAccount.name | string | `nil` |  |
| otelCollectorMetrics.annotations | object | `{}` | OtelColectorMetrics Deployment annotation. |
| otelCollectorMetrics.podAnnotations | object | `{"signoz.io/path":"/metrics","signoz.io/port":"8888","signoz.io/scrape":"true"}` | OtelColectorMetrics pod(s) annotation. |
| otelCollectorMetrics.minReadySeconds | int | `5` |  |
| otelCollectorMetrics.progressDeadlineSeconds | int | `120` |  |
| otelCollectorMetrics.replicaCount | int | `1` |  |
| otelCollectorMetrics.ballastSizeMib | int | `683` |  |
| otelCollectorMetrics.initContainers.init.enabled | bool | `true` |  |
| otelCollectorMetrics.initContainers.init.image.registry | string | `"docker.io"` |  |
| otelCollectorMetrics.initContainers.init.image.repository | string | `"busybox"` |  |
| otelCollectorMetrics.initContainers.init.image.tag | float | `1.35` |  |
| otelCollectorMetrics.initContainers.init.image.pullPolicy | string | `"IfNotPresent"` |  |
| otelCollectorMetrics.initContainers.init.command.delay | int | `5` |  |
| otelCollectorMetrics.initContainers.init.command.endpoint | string | `"/ping"` |  |
| otelCollectorMetrics.initContainers.init.command.waitMessage | string | `"waiting for clickhouseDB"` |  |
| otelCollectorMetrics.initContainers.init.command.doneMessage | string | `"clickhouse ready, starting otel collector metrics now"` |  |
| otelCollectorMetrics.ports.metrics.enabled | bool | `false` | Whether to enable service port for internal metrics |
| otelCollectorMetrics.ports.metrics.containerPort | int | `8888` | Container port for internal metrics |
| otelCollectorMetrics.ports.metrics.servicePort | int | `8888` | Service port for internal metrics |
| otelCollectorMetrics.ports.metrics.protocol | string | `"TCP"` | Protocol to use for internal metrics |
| otelCollectorMetrics.ports.zpages.enabled | bool | `false` | Whether to enable service port for ZPages |
| otelCollectorMetrics.ports.zpages.containerPort | int | `55679` | Container port for Zpages |
| otelCollectorMetrics.ports.zpages.servicePort | int | `55679` | Service port for Zpages |
| otelCollectorMetrics.ports.zpages.protocol | string | `"TCP"` | Protocol to use for Zpages |
| otelCollectorMetrics.ports.health-check.enabled | bool | `true` | Whether to enable service port for health check |
| otelCollectorMetrics.ports.health-check.containerPort | int | `13133` | Container port for health check |
| otelCollectorMetrics.ports.health-check.servicePort | int | `13133` | Service port for health check |
| otelCollectorMetrics.ports.health-check.protocol | string | `"TCP"` | Protocol to use for health check |
| otelCollectorMetrics.ports.pprof.enabled | bool | `false` | Whether to enable service port for pprof |
| otelCollectorMetrics.ports.pprof.containerPort | int | `1777` | Container port for pprof |
| otelCollectorMetrics.ports.pprof.servicePort | int | `1777` | Service port for pprof |
| otelCollectorMetrics.ports.pprof.protocol | string | `"TCP"` | Protocol to use for pprof |
| otelCollectorMetrics.livenessProbe.enabled | bool | `false` |  |
| otelCollectorMetrics.livenessProbe.port | int | `13133` |  |
| otelCollectorMetrics.livenessProbe.path | string | `"/"` |  |
| otelCollectorMetrics.livenessProbe.initialDelaySeconds | int | `5` |  |
| otelCollectorMetrics.livenessProbe.periodSeconds | int | `10` |  |
| otelCollectorMetrics.livenessProbe.timeoutSeconds | int | `5` |  |
| otelCollectorMetrics.livenessProbe.failureThreshold | int | `6` |  |
| otelCollectorMetrics.livenessProbe.successThreshold | int | `1` |  |
| otelCollectorMetrics.readinessProbe.enabled | bool | `false` |  |
| otelCollectorMetrics.readinessProbe.port | int | `13133` |  |
| otelCollectorMetrics.readinessProbe.path | string | `"/"` |  |
| otelCollectorMetrics.readinessProbe.initialDelaySeconds | int | `5` |  |
| otelCollectorMetrics.readinessProbe.periodSeconds | int | `10` |  |
| otelCollectorMetrics.readinessProbe.timeoutSeconds | int | `5` |  |
| otelCollectorMetrics.readinessProbe.failureThreshold | int | `6` |  |
| otelCollectorMetrics.readinessProbe.successThreshold | int | `1` |  |
| otelCollectorMetrics.customLivenessProbe | object | `{}` |  |
| otelCollectorMetrics.customReadinessProbe | object | `{}` |  |
| otelCollectorMetrics.ingress.enabled | bool | `false` | Enable ingress for OtelCollectorMetrics |
| otelCollectorMetrics.ingress.className | string | `""` | Ingress Class Name to be used to identify ingress controllers |
| otelCollectorMetrics.ingress.annotations | object | `{}` | Annotations to OtelCollectorMetrics Ingress |
| otelCollectorMetrics.ingress.hosts | list | `[{"host":"otelcollector-metrics.domain.com","paths":[{"path":"/","pathType":"ImplementationSpecific","port":13133}]}]` | OtelCollectorMetrics Ingress Host names with their path details |
| otelCollectorMetrics.ingress.tls | list | `[]` | OtelCollectorMetrics Ingress TLS |
| otelCollectorMetrics.resources.requests.cpu | string | `"200m"` |  |
| otelCollectorMetrics.resources.requests.memory | string | `"400Mi"` |  |
| otelCollectorMetrics.resources.limits.cpu | string | `"1000m"` |  |
| otelCollectorMetrics.resources.limits.memory | string | `"2Gi"` |  |
| otelCollectorMetrics.nodeSelector | object | `{}` |  |
| otelCollectorMetrics.tolerations | list | `[]` |  |
| otelCollectorMetrics.affinity | object | `{}` |  |
| otelCollectorMetrics.config | object | See `values.yaml` for defaults | Configurations for OtelCollectorMetrics |
| otelCollectorMetrics.config.processors.memory_limiter | string | `nil` | Memory Limiter processor If set to null, will be overridden with values based on k8s resource limits. |

