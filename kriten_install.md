# Kriten Installation

## Table of Content

- [Kriten Installation](#kriten-installation)
  - [Table of Content](#table-of-content)
  - [Installation](#installation)
    - [Prerequisites and Guidelines](#prerequisites-and-guidelines)
    - [Helm install](#helm-install)
    - [Helm Chart Parameters](#helm-chart-parameters)


## Installation

### Prerequisites and Guidelines

- Installation into dedicated kubernetes cluster or namespace is recommended to limit access to Kriten resources for administrators only:
  * No other workloads beside Kriten running in cluster/namespace.
  * Kubernetes and Helm access restricted to cluster/namespace for administrators only.
- Kubernetes 1.21+
- Helm v3+

### Helm install

The Chart can be installed by cloning the Helm Chart from GitHub: https://github.com/evolvere-tech/kriten-charts

Kriten can be installed with integrated PostgreSQL database (recommended for Dev and UAT environments) or with external PostgreSQL database (recommended for production use).

Kriten supports local authenticator and Microsoft AD authenticator at same time. If no Microsoft AD authenticator enabled and configured, only local authentication will take place.

Helm install with values.yaml modified for target configuration:

`helm install kriten ./kriten-charts -n kriten`


### Helm Chart Parameters

|Parameter|Description|Default|
|---------|-----------|-------|
|`replicaCount`|Number of desired Kriten Core pods|`1`|
|`image.repository`|Kriten Docker image repository|`"evolvere/kriten-core"`|
|`image.tag`|Kriten Docker image tag|`"v0.3-beta4"`|
|`image.pullPolicy`|Pull policy for Kriten Docker image|`"IfNotPresent"`|
|`imagePullSecrets`|Kubernetes secrets to pull container images from private repository|`["name": "dockerhub]`|
|`name`|Kriten deployment name|`"kriten"`
|`namespace`|Namespace for Kriten|`"kriten"`
|`serviceAccount.create`| Specifies whether a service account should be created for Kriten|`true`
|`serviceAccount.annotations`| Annotations to add to the service account|`{}`
|`serviceAccount.name`|The name of the service account to use, if not set and create true, a name is generated using the fullname template|`""`
|`service.type`|Kriten k8s service type|`ClusterIP`
|`service.port`|Kriten k8s service port|`80`
|`ldap.enabled`|LDAP/AD authenticator enabled|`false`
|`ldap.binUser`|LDAP/AD bind account name|`""`
|`ldap.bindPass`|LDAP/AD bind account password|`""`
|`ldap.fqdn`|LDAP/AD service IP or FQDN|`""`
|`ldap.port`|LDAP/AD access TCP port (389 or 639 for TLS)|`389`
|`ldap.baseDN`|LDAP/AD base DN|`""`
|`jwt.key`|Private key or secret to sign issued JWT|`"vcwYCYkum_2Fsukk_i"`
|`jwt.expiry_seconds`|JWT expiry in seconds|`3600`
|`postgresql.install`|PostgreSQL installed as part of Kriten installation in same k8s cluster|`true`
|`postgresql.image.registry`|PostgreSQL Docker image registry|`docker.io`
|`postgresql.image.repository`|PostgreSQL Docker image repository|`bitnami/postgresql`
|`postgresql.image.tag`|PostgreSQL image tag|`"16"`
|`postgresql.auth.username`|PostgreSQL username|`kriten`
|`postgresql.auth.password`|PostgreSQL password|`kriten`
|`postgresql.auth.database`|PostgreSQL database name|`kriten`
|`postgresql.persistence.enabled`|PostgreSQL database persistnce storage enabled|`true`
|`ingress.enabled`|Ingress configuration enabled|`true`
|`ingress.className`|Ingress class name|`"nginx"`
|`ingress.hosts`|Ingress hosts and paths definitions|`[]`
