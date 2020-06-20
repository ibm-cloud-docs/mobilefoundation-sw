---

copyright:
  years: 2020
lastupdated: "2020-06-03"

keywords: mobile foundation software, deployment values, OCP registry, database configuration

subcollection:  mobilefoundation-sw

---

{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:term: .term}
{:tip: .tip}
{:note: .note}
{:external: target="_blank" .external}

# Deployment values for IBM {{site.data.keyword.mobilefoundation_short}}
{: #deployment-values}

## List of deployment values

List of deployment parameters is as follows.

| Qualifier | Parameter  | Definition | Allowed Value |
|---|---|---|---|
| image     | pullPolicy | Image Pull Policy | Always, Never, or IfNotPresent. Default: **IfNotPresent** |
| ingress | subdomain.prefix | Specifies the prefix to be added to the ingress subdomain to access the deployed service. | Defaults to **mobilefoundation**. |
|         | secret | TLS secret name| Specifies the name of the secret for the certificate that must be used in the Ingress definition. The secret must be pre-created by using the relevant certificate and key. Mandatory if SSL/TLS is enabled. Pre-create the secret with Certificate & Key before you supply the name here. Refer [here](https://mobilefirstplatform.ibmcloud.com/tutorials/en/foundation/8.0/ibmcloud/mobilefoundation-on-openshift/additional-docs/cr-configuration/#optional-creating-tls-secret-for-ingress-configuration){: external} |
|         | sslPassThrough | Enable SSL pass-through | Specifies if the SSL request should be passed through to the {{site.data.keyword.mobilefoundation_short}}  service - SSL termination occurs in {{site.data.keyword.mobilefoundation_short}}. **false** (default) or true|
|         | https | Enable backend communication over HTTPS. To enable inter-component https communication within the cluster. | **false** is default.|
|  debug | enabled | Specify whether to enable deployment trace. This prints detailed deployment progress with all the deployment values used.  | Default is **true**.|

### Database initialization configuration deployment values

List of database initialization deployment parameters is as follows.

| Qualifier | Parameter  | Definition | Allowed Value |
|---|---|---|---|
| dbinit | enabled | Specify whether to create database initialization and schema for Server, Push and Application Center deployments (Only for IBM DB2). | **true** (default) or false |
| dbinit.resources | requests.cpu | The minimum required CPU core. Specify integers, fractions (e.g. 0.5), or millicore values(e.g. 100m, where 100m is equivalent to .1 core). | Default is **900m**. |
|  | requests.memory | The minimum memory in bytes. Specify integers with one of these suffixes: E, P, T, G, M, K, or power-of-two equivalents: Ei, Pi, Ti, Gi, Mi, Ki. | Default is **1024Mi**. |
|  | limits.cpu | The upper limit of CPU core. Specify integers, fractions (e.g. 0.5), or millicores values(e.g. 100m, where 100m is equivalent to .1 core). | Default is **2000m**. |
|  | limits.memory | The memory upper limit in bytes. Specify integers with suffixes: E, P, T, G, M, K, or power-of-two equivalents: Ei, Pi, Ti, Gi, Mi, Ki. | Default is **2048Mi**. |

### Database configuration deployment values

List of database configuration deployment parameters is as follows.

| Qualifier | Parameter  | Definition | Allowed Value |
|---|---|---|---|
| db | type | The type of the database used for {{site.data.keyword.mobilefoundation_short}}  components. | **DB2** is the only supported type. |
|               | host | Hostname/IP address for {{site.data.keyword.mobilefoundation_short}} database. | |
|                       | port | 	Database port number for {{site.data.keyword.mobilefoundation_short}} to connect.  |  |
|                       | secret | A precreated secret, which has database credentials| |
|                       | name | Name of the {{site.data.keyword.mobilefoundation_short}} database |  |
|                       | userid | Provide {{site.data.keyword.mobilefoundation_short}} database username. |  |
|                       | password | Provide {{site.data.keyword.mobilefoundation_short}} database password. |  |
|                       | ssl | Database connection made over SSL. Specify whether your database connection must be http or https. Applicable only if the database type selected is DB2.| Default is **false**.  |
|                       | adminCredentialsSecret | If you have enabled DB initialization ,then provide the secret to create database tables and schemas for {{site.data.keyword.mobilefoundation_short}} components. |  |

### {{site.data.keyword.mobilefoundation_short}} server configuration deployment values

List of {{site.data.keyword.mobilefoundation_short}} server deployment parameters is as follows.

| Qualifier | Parameter  | Definition | Allowed Value |
|---|---|---|---|
| mfpserver | enabled          | Flag to enable Server | **true** (default) or false |
|           | consoleUserid | Set login userid for {{site.data.keyword.mobilefoundation_short}} server Operations console. | Default value is **admin**.|
|           | consolePassword | Set login password for {{site.data.keyword.mobilefoundation_short}} server Operations console. | Default value is **admin**.|
|  mfpserver.db | schema | {{site.data.keyword.mobilefoundation_short}} server database schema to be created when the {{site.data.keyword.mobilefoundation_short}} is deployed. If the schema already exists, it will be reused. | **MFPDATA** is the default value. |
|  mfpserver.internalClientSecretDetails | adminClientSecretId | Default {{site.data.keyword.mobilefoundation_short}} server Admin Client Secret Id. | **mfpadmin** is the default value. |
|   | adminClientSecretPassword | Default {{site.data.keyword.mobilefoundation_short}} server Admin Client Secret Password. | **nimdapfm** is the default value. |
|   | pushClientSecretId | Default Push Client secret Id. | **push** is the default value. |
|   | pushClientSecretPassword | Default Push Client secret password. | **hsup** is the default value. |
| mfpserver | adminClientSecret | Admin client secret | Specify the Client Secret name created. Refer [here](https://mobilefirstplatform.ibmcloud.com/tutorials/en/foundation/8.0/ibmcloud/mobilefoundation-on-openshift/additional-docs/cr-configuration/#optional-creating-secrets-for-confidential-clients){: external}  |
|  | pushClientSecret | Push Confidential Client secret | Specify the Client Secret name created. Refer [here](https://mobilefirstplatform.ibmcloud.com/tutorials/en/foundation/8.0/ibmcloud/mobilefoundation-on-openshift/additional-docs/cr-configuration/#optional-creating-secrets-for-confidential-clients){: external} |
|  | liveupdateClientSecret | LiveUpddate Confidential Client secret | Specify the Client Secret name created. Refer [here](https://mobilefirstplatform.ibmcloud.com/tutorials/en/foundation/8.0/ibmcloud/mobilefoundation-on-openshift/additional-docs/cr-configuration/#optional-creating-secrets-for-confidential-clients){: external} |
|  | replicas | The number of instances (pods) of {{site.data.keyword.mobilefoundation_short}} Server that need to be created | Positive integer (Default: **2**) |
| mfpserver.autoscaling     | enabled | Enables a Horizontal Pod Autoscaler. Enabling this field disables the *replicas* field. | **false** (default) or true |
|           | min  | Lower limit for the number of pods that can be set by the autoscaler. | Positive integer (default to **1**) |
|           | max | Upper limit for the number of pods that can be set by the autoscaler. Cannot be less than min. | Positive integer (default to **10**) |
|           | targetcpu | Target average CPU utilization (represented as a percentage of requested CPU) over all the pods. | Integer in the range 1 - 100(default to **50**) |
| mfpserver.pdb     | enabled | Specify whether to enable or disable Pod Disruption Budget. Enables application protection availability during a cluster node maintenance. | **true** (default) or false |
|           | min  | Minimum number of probe replicas that must be available during pod eviction. | Positive integer (defaults to 1) |
|    mfpserver | customConfiguration  |  Custom server configuration (Optional)  | Provide server-specific additional configuration reference to a pre-created config map. Refer [here](https://mobilefirstplatform.ibmcloud.com/tutorials/en/foundation/8.0/ibmcloud/mobilefoundation-on-openshift/additional-docs/cr-configuration/#optional-custom-server-configuration)|
|  | keystoreSecret | Refer the [configuration section](https://mobilefirstplatform.ibmcloud.com/tutorials/en/foundation/8.0/ibmcloud/mobilefoundation-on-openshift/additional-docs/cr-configuration/#optional-creating-custom-keystore-secret-for-the-deployments){: external} to pre-create the secret with keystores and their passwords.|
| mfpserver.resources | limits.cpu  | Describes the maximum amount of CPU allowed.  | Default is **2000m**. See Kubernetes - [meaning of CPU](https://kubernetes.io/docs/concepts/configuration/manage-compute-resources-container/#meaning-of-cpu){: external} |
|                  | limits.memory | Describes the maximum amount of memory allowed. | Default is **4096Mi**. See Kubernetes - [meaning of Memory](https://kubernetes.io/docs/concepts/configuration/manage-compute-resources-container/#meaning-of-memory){: external}|
|           | requests.cpu  | Describes the minimum amount of CPU required - if not specified defaults to limit (if specified) or otherwise implementation-defined value.  | Default is **1000m**. See Kubernetes - [meaning of CPU](https://kubernetes.io/docs/concepts/configuration/manage-compute-resources-container/#meaning-of-cpu){: external} |
|           | requests.memory | Describes the minimum amount of memory required. If not specified, the memory amount defaults to the limit (if specified) or the implementation-defined value. | Default is **1536Mi**. See Kubernetes - [meaning of Memory](https://kubernetes.io/docs/concepts/configuration/manage-compute-resources-container/#meaning-of-memory){: external} |

### {{site.data.keyword.mobilefoundation_short}} Push Notifications configuration deployment values

List of {{site.data.keyword.mobilefoundation_short}} Push Notifications deployment parameters is as follows.

| Qualifier | Parameter  | Definition | Allowed Value |
|---|---|---|---|
| mfppush | enabled          | Flag to enable {{site.data.keyword.mobilefoundation_short}} Push | **true** (default) or false |
|  | replicas| The number of instances (pods) of {{site.data.keyword.mobilefoundation_short}} server that need to be created | Positive integer (Default: **2**) |
| mfppush.autoscaling     | enabled | Enables a Horizontal Pod Autoscaler. Enabling this field disables the *replicas* field. | **false** (default) or true |
|           | min  | Lower limit for the number of pods that can be set by the autoscaler. | Positive integer (default to **1**) |
|           | max | Upper limit for the number of pods that can be set by the autoscaler. Cannot be less than minReplicas. | Positive integer (default to **10**) |
|           | targetcpu | Target average CPU usage (represented as a percentage of requested CPU) over all the pods. | Integer in the range 1 - 100(default to **50**) |
| mfppush.pdb     | enabled | Specify whether to enable or disable Pod Disruption Budget. Enables application protection availability during a cluster node maintenance. | **true** (default) or false |
|           | min  | Minimum number of probe replicas that must be available during pod eviction. | Positive integer (default to **1**) |
| mfppush | customConfiguration |  Custom configuration (Optional)  | Provide Push specific additional configuration reference to a pre-created config map. Refer [here](https://mobilefirstplatform.ibmcloud.com/tutorials/en/foundation/8.0/ibmcloud/mobilefoundation-on-openshift/additional-docs/cr-configuration/#optional-custom-server-configuration){: external} |
|  | keystoresSecretName | Refer the [configuration section](https://mobilefirstplatform.ibmcloud.com/tutorials/en/foundation/8.0/ibmcloud/mobilefoundation-on-openshift/additional-docs/cr-configuration/#optional-creating-custom-keystore-secret-for-the-deployments) to pre-create the secret with keystores and their passwords.|
| mfppush.resources | limits.cpu  | Describes the maximum amount of CPU allowed.  | Default is **1000m**. See Kubernetes - [meaning of CPU](https://kubernetes.io/docs/concepts/configuration/manage-compute-resources-container/#meaning-of-cpu){: external} |
|                  | limits.memory | Describes the maximum amount of memory allowed. | Default is **2048Mi**. See Kubernetes - [meaning of Memory](https://kubernetes.io/docs/concepts/configuration/manage-compute-resources-container/#meaning-of-memory){: external}|
|           | requests.cpu  | Describes the minimum amount of CPU required - if not specified defaults to limit (if specified) or otherwise implementation-defined value.  | Default is **750m**. See Kubernetes - [meaning of CPU](https://kubernetes.io/docs/concepts/configuration/manage-compute-resources-container/#meaning-of-cpu){: external} |
|           | requests.memory | Describes the minimum amount of memory required. If not specified, the memory amount defaults to the limit (if specified) or the implementation-defined value. | Default is **1024Mi**. See Kubernetes - [meaning of Memory](https://kubernetes.io/docs/concepts/configuration/manage-compute-resources-container/#meaning-of-memory){: external} |

### {{site.data.keyword.mobilefoundation_short}} Live Update configuration deployment values

List of {{site.data.keyword.mobilefoundation_short}} Live Update deployment parameters is as follows.

| Qualifier | Parameter  | Definition | Allowed Value |
|---|---|---|---|
| mfpliveupdate | enabled          | Flag to enable Live update | **true** (default) or false |
| mfpliveupdate | replicas  | The number of instances (pods) of {{site.data.keyword.mobilefoundation_short}} Live Update that need to be created. | Positive integer (Default: **2**. |
|  |  db.schema | {{site.data.keyword.mobilefoundation_short}} Live Update Database schema to be created when {{site.data.keyword.mobilefoundation_short}} is deployed. If the schema already exists, it will be reused. | Default value is **MFPLIVUPD**. |
| mfpliveupdate.autoscaling | enabled  | Enables a Horizontal Pod Autoscaler. Enabling this field disables the *replicas* field. | **false** (default) or true. |
|  | min  | Lower limit for the number of pods that can be set by the autoscaler. | Positive integer (defaults to **1**). |
|  | max  | Upper limit for the number of pods that can be set by the autoscaler. Cannot be less than min. | Positive integer (defaults to **10**). |
|  | targetcpu  | Target average CPU utilization (represented as a percentage of requested CPU) over all the pods. | Integer in the range 1 - 100(defaults to **50**). |
| mfpliveupdate.pdb | enabled  | Specify whether to enable or disable Pod Disruption Budget. Enables application protection availability during a cluster node maintenance. | **true** (default) or false. |
|  | min  | Minimum number of probe replicas that must be available during pod eviction. | Positive integer (defaults to **1**). |
| mfpliveupdate | customConfiguration  | Custom server configuration (Optional). | Provide server-specific additional configuration reference to a pre-created config map. Refer [here](https://mobilefirstplatform.ibmcloud.com/tutorials/en/foundation/8.0/ibmcloud/mobilefoundation-on-openshift/additional-docs/cr-configuration/#optional-custom-server-configuration){: external}. |
|  | keystoreSecret          | Refer the [configuration section](https://mobilefirstplatform.ibmcloud.com/tutorials/en/foundation/8.0/ibmcloud/mobilefoundation-on-openshift/additional-docs/cr-configuration/#optional-creating-custom-keystore-secret-for-the-deployments){: external} to pre-create the secret with keystores and their passwords. |  |
| mfpliveupdate.resources | limits.cpu  | Describes the maximum amount of CPU allowed. | Default is **1000m**. See Kubernetes - [meaning of CPU](https://kubernetes.io/docs/concepts/configuration/manage-compute-resources-container/#meaning-of-cpu){: external}. |
|  | limits.memory  | Describes the maximum amount of memory allowed. | Default is **2048Mi**. See Kubernetes - [meaning of Memory](https://kubernetes.io/docs/concepts/configuration/manage-compute-resources-container/#meaning-of-memory){: external}. |
|  | requests.cpu  | Describes the minimum amount of CPU required - if not specified defaults to limit (if specified) or otherwise implementation-defined value. | Default is **750m**. See Kubernetes - [meaning of CPU](https://kubernetes.io/docs/concepts/configuration/manage-compute-resources-container/#meaning-of-cpu){: external}. |
|  | requests.memory  | Describes the minimum amount of memory required. If not specified, the memory amount will default to the limit (if specified) or the implementation-defined value. | Default is **1024Mi**. See Kubernetes - [meaning of Memory](https://kubernetes.io/docs/concepts/configuration/manage-compute-resources-container/#meaning-of-memory){: external}. |

### {{site.data.keyword.mobilefoundation_short}} Application Center configuration deployment values

List of {{site.data.keyword.mobilefoundation_short}} Application Center deployment parameters is as follows.

| Qualifier | Parameter  | Definition | Allowed Value |
|---|---|---|---|
| mfpappcenter | enabled          | Flag to enable Application Center | **true** (default) or false |
|  | consoleUserid          | Set login userid for Application Center console. | Default is **admin**. |
|  | consoleUserid          | Set login password for Application Center console. | Default is **admin**. |
|  | customConfiguration |  Custom configuration (Optional)  | Provide Application Center specific additional configuration reference to a pre-created config map. Refer [here](https://mobilefirstplatform.ibmcloud.com/tutorials/en/foundation/8.0/ibmcloud/mobilefoundation-on-openshift/additional-docs/cr-configuration#optional-custom-server-configuration){: external} |
|  | keystoreSecret | Refer the [configuration section](https://mobilefirstplatform.ibmcloud.com/tutorials/en/foundation/8.0/ibmcloud/mobilefoundation-on-openshift/additional-docs/cr-configuration/#optional-creating-custom-keystore-secret-for-the-deployments){: external} to pre-create the secret with keystores and their passwords.|
|  mfpappcenter.db | schema | Mobile Foundation AppCenter Database schema to be created when the Mobile Foundation is deployed. If the schema already exists, it will be reused. | **APPCNTR** (default) |
| mfpappcenter.autoscaling     | enabled | Enables a Horizontal Pod Autoscaler. Enabling this field disables the *replicas* field. | **false** (default) or true |
|           | min | Lower limit for the number of pods that can be set by the autoscaler. | Positive integer (default to **1**) |
|           | max | Upper limit for the number of pods that can be set by the autoscaler. Cannot be less than minReplicas. | Positive integer (default to **10**) |
|           | targetcpu | Target average CPU usage (represented as a percentage of requested CPU) over all the pods. | Integer in the range 1 - 100(default to **50**) |
| mfpappcenter.pdb     | enabled | Specify whether to enable or disable Pod Disruption Budget. Enables application protection availability during a cluster node maintenance. | **true** (default) or false |
|           | min  | Minimum number of probe replicas that must be available during pod eviction. | Positive integer (default to **1**) |
| mfpappcenter.resources | limits.cpu  | Describes the maximum amount of CPU allowed.  | Default is **1000m**. See Kubernetes - [meaning of CPU](https://kubernetes.io/docs/concepts/configuration/manage-compute-resources-container/#meaning-of-cpu){: external} |
|                  | limits.memory | Describes the maximum amount of memory allowed. | Default is **2048Mi**. See Kubernetes - [meaning of Memory](https://kubernetes.io/docs/concepts/configuration/manage-compute-resources-container/#meaning-of-memory){: external}|
|           | requests.cpu  | Describes the minimum amount of CPU required - if not specified defaults to limit (if specified) or otherwise implementation-defined value.  | Default is **750m**. See Kubernetes - [meaning of CPU](https://kubernetes.io/docs/concepts/configuration/manage-compute-resources-container/#meaning-of-cpu){: external} |
|           | requests.memory | Describes the minimum amount of memory required. If not specified, the memory amount defaults to the limit (if specified) or the implementation-defined value. | Default is **1024Mi**. See Kubernetes - [meaning of Memory](https://kubernetes.io/docs/concepts/configuration/manage-compute-resources-container/#meaning-of-memory){: external}|

### {{site.data.keyword.mobilefoundation_short}} Analytics configuration deployment values

List of {{site.data.keyword.mobilefoundation_short}} Analytics deployment parameters is as follows.

| Qualifier | Parameter  | Definition | Allowed Value |
|---|---|---|---|
| mfpanalytics | enabled          | Flag to enable analytics | **true** (default) or false |
|  | consoleUserid          | Set login userid for Analytics console. | Default is **admin**. |
  | consolePassword          | Set login password for Analytics console. | Default is **admin**. |
|  | replicas | The number of instances (pods) of {{site.data.keyword.mobilefoundation_short}} Operational Analytics that need to be created | Positive integer (Default: **2**) |
| mfpanalytics.autoscaling     | enabled | Enables a Horizontal Pod Autoscaler. Enabling this field disables the *replicas* field. | **false** (default) or true |
|           | min  | Lower limit for the number of pods that can be set by the autoscaler. | Positive integer (default to **1**) |
|           | max | Upper limit for the number of pods that can be set by the autoscaler. Cannot be less than minReplicas. | Positive integer (default to **10**) |
|           | targetcpu | Target average CPU usage (represented as a percentage of requested CPU) over all the pods. | Integer in the range 1 - 100(default to **50**) |
| mfpanalytics.pdb     | enabled | Specify whether to enable or disable Pod Disruption Budget. Enables application protection availability during a cluster node maintenance. | **true** (default) or false |
|           | min  | Minimum number of probe replicas that must be available during pod eviction. | Positive integer (default to **1**) |
|    mfpanalytics | customConfiguration |  Custom configuration (Optional)  | Provide Analytics specific additional configuration reference to a pre-created config map. Refer [here](https://mobilefirstplatform.ibmcloud.com/tutorials/en/foundation/8.0/ibmcloud/mobilefoundation-on-openshift/additional-docs/cr-configuration/#optional-custom-server-configuration){: external} |
|  | keystoreSecret | Refer the [configuration section](https://mobilefirstplatform.ibmcloud.com/tutorials/en/foundation/8.0/ibmcloud/mobilefoundation-on-openshift/additional-docs/cr-configuration/#optional-creating-custom-keystore-secret-for-the-deployments){: external} to pre-create the secret with keystores and their passwords.|
| mfpanalytics.resources | limits.cpu  | Describes the maximum amount of CPU allowed.  | Default is **1000m**. See Kubernetes - [meaning of CPU](https://kubernetes.io/docs/concepts/configuration/manage-compute-resources-container/#meaning-of-cpu){: external}. |
|                  | limits.memory | Describes the maximum amount of memory allowed. | Default is **2048Mi**. See Kubernetes - [meaning of Memory](https://kubernetes.io/docs/concepts/configuration/manage-compute-resources-container/#meaning-of-memory){: external}.|
|           | requests.cpu  | Describes the minimum amount of CPU required - if not specified defaults to limit (if specified) or otherwise implementation-defined value.  | Default is **750m**. See Kubernetes - [meaning of CPU](https://kubernetes.io/docs/concepts/configuration/manage-compute-resources-container/#meaning-of-cpu){: external}. |
|           | requests.memory | Describes the minimum amount of memory required. If not specified, the memory amount defaults to the limit (if specified) or the implementation-defined value. | Default is **1024Mi**. See Kubernetes - [meaning of Memory](https://kubernetes.io/docs/concepts/configuration/manage-compute-resources-container/#meaning-of-memory){: external}. |

### {{site.data.keyword.mobilefoundation_short}} Analytics Receiver configuration deployment values

List of {{site.data.keyword.mobilefoundation_short}} Analytics Receiver deployment parameters is as follows.

| Qualifier | Parameter  | Definition | Allowed Value |
|---|---|---|---|
| mfpanalytics_recvr | enabled          | Flag to enable Analytics Receiver | **true** (default) or false |
|  | replicas  | The number of instances (pods) of {{site.data.keyword.mobilefoundation_short}} Analytics Receiver that needs to be created. | Positive integer (Default: **1**. |
| mfpanalytics_recvr.autoscaling | enabled  | Enables a Horizontal Pod Autoscaler. Enabling this field disables the *replicas* field. | **false** (default) or true. |
|  | min  | Lower limit for the number of pods that can be set by the autoscaler. | Positive integer (defaults to **1**). |
|  | max  | Upper limit for the number of pods that can be set by the autoscaler. Cannot be less than min. | Positive integer (defaults to **10**). |
|  | targetcpu  | Target average CPU usage (represented as a percentage of requested CPU) over all the pods. | Integer in the range 1 - 100(defaults to **50**). |
| mfpanalytics_recvr.pdb | enabled  | Specify whether to enable or disable Pod Disruption Budget. Enables application protection availability during a cluster node maintenance. | **true** (default) or false. |
|  | min  | minimum available pods | Positive integer (defaults to **1**). |
| mfpanalytics_recvr | analyticsRecvrSecret     | A pre-created secret for receiver. | Refer [here](https://mobilefirstplatform.ibmcloud.com/tutorials/en/foundation/8.0/ibmcloud/mobilefoundation-on-openshift/additional-docs/cr-configuration/#optional-creating-custom-keystore-secret-for-the-deployments){: external}. |
|  | customConfiguration | Custom configuration (Optional). | Provide Analytics specific additional configuration reference to a pre-created config map. Refer [here](https://mobilefirstplatform.ibmcloud.com/tutorials/en/foundation/8.0/ibmcloud/mobilefoundation-on-openshift/additional-docs/cr-configuration/#optional-custom-server-configuration){: external}. |
| mfpanalytics_recvr | keystoreSecret     | Refer the [configuration section](https://mobilefirstplatform.ibmcloud.com/tutorials/en/foundation/8.0/ibmcloud/mobilefoundation-on-openshift/additional-docs/cr-configuration/#optional-creating-custom-keystore-secret-for-the-deployments){: external} to pre-create the secret with keystores and their passwords. |  |
| mfpanalytics_recvr.resources | limits.cpu  | Describes the maximum amount of CPU allowed. | Default is **1000m**. See Kubernetes - [meaning of CPU](https://kubernetes.io/docs/concepts/configuration/manage-compute-resources-container/#meaning-of-cpu){: external}. |
|  | limits.memory  | Describes the maximum amount of memory allowed. | Default is **2048Mi**. See Kubernetes - [meaning of Memory](https://kubernetes.io/docs/concepts/configuration/manage-compute-resources-container/#meaning-of-memory){: external}. |
|  | requests.cpu  | Describes the minimum amount of CPU required - if not specified defaults to limit (if specified) or otherwise implementation-defined value. | Default is **750m**. See Kubernetes - [meaning of CPU](https://kubernetes.io/docs/concepts/configuration/manage-compute-resources-container/#meaning-of-cpu){: external}. |
|  | requests.memory  | Describes the minimum amount of memory required. If not specified, the memory amount defaults to the limit (if specified) or the implementation-defined value. | Default is **1024Mi**. See Kubernetes - [meaning of Memory](https://kubernetes.io/docs/concepts/configuration/manage-compute-resources-container/#meaning-of-memory){: external}. |

### Elasticsearch configuration deployment values

List of Elasticsearch deployment parameters is as follows.

| Qualifier | Parameter  | Definition | Allowed Value |
|---|---|---|---|
| elasticsearch  | namespace | Specify the namespace to be created/used to deploy Elasticsearch.  | Default is **mfes**.|
|   | master.replicas | Number of Pods requested for Elasticsearch master nodes.  | Default is **2**.|
|   | client.replicas | Number of Pods requested for Elasticsearch client nodes.  | Default is **1**.|
|   | data.replicas | Number of Pods requested for Elasticsearch data nodes.  | Default is **2**.|
|   | shards | Number of Elasticsearch shards to be set.  | Default is **3**.|
|   | replicasPerShard | Number of Elasticsearch replicas per shard.  | Default is **1**.|
|   | persistence.claimName | Specify an existing volume claim here (PVC) for Elasticsearch.  | |
|   | persistence.storageClassName | Specify a specific storage class name for Elasticsearch.  | Default is **ibmc-file-retain-gold"**.|
|   | persistence.size | Size of the volume claim.  | Defaults to **20Gi**.|
| elasticsearch.data.resources  | requests.cpu | The minimum required CPU core. Specify integers, fractions (e.g. 0.5), or millicore values(e.g. 100m, where 100m is equivalent to .1 core).  | Default is **1000m**.|
|   | requests.memory | The minimum memory in bytes. Specify integers with one of these suffixes: E, P, T, G, M, K, or power-of-two equivalents: Ei, Pi, Ti, Gi, Mi, Ki.  | Default is **2048Mi**.|
|   | limits.cpu | The upper limit of CPU core. Specify integers, fractions (e.g. 0.5), or millicore values(e.g. 100m, where 100m is equivalent to .1 core).  | Default is **2000m**.|
|   | requests.memory | The upper limit of memory in bytes. Specify integers with one of these suffixes: E, P, T, G, M, K, or power-of-two equivalents: Ei, Pi, Ti, Gi, Mi, Ki.  | Default is **10Gi**.|
| elasticsearch.master.resources  | requests.cpu | The minimum required CPU core. Specify integers, fractions (e.g. 0.5), or millicore values(e.g. 100m, where 100m is equivalent to .1 core).  | Default is **750m**.|
|   | requests.memory | The minimum memory in bytes. Specify integers with one of these suffixes: E, P, T, G, M, K, or power-of-two equivalents: Ei, Pi, Ti, Gi, Mi, Ki.  | Default is **1024Mi**.|
|   | limits.cpu | The upper limit of CPU core. Specify integers, fractions (e.g. 0.5), or millicore values(e.g. 100m, where 100m is equivalent to .1 core).  | Default is **1000m**.|
|   | requests.memory | The upper limit of memory in bytes. Specify integers with one of these suffixes: E, P, T, G, M, K, or power-of-two equivalents: Ei, Pi, Ti, Gi, Mi, Ki.  | Default is **2048Mi**.|


