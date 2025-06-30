# Installation

## Prerequisites and Guidelines

- Installation into dedicated kubernetes cluster or namespace is recommended to limit access to Kriten resources for administrators only:
  * No other workloads beside Kriten running in cluster/namespace.
  * Kubernetes and Helm access restricted to cluster/namespace for administrators only.
- Kubernetes 1.21+
- Helm v3+

## Helm install

The Chart can be installed by adding the helm repo to your system.

Kriten can be installed along with local PostgreSQL database (recommended for Dev and UAT environments) or with external PostgreSQL database (recommended for production use).

Kriten supports local authenticator and Microsoft AD authenticator at same time. If no Microsoft AD authenticator enabled and configured, only local authentication will take place.

Helm install with values.yaml modified for target configuration:

### Add helm repo
```
helm repo add kriten https://kriten-io.github.io/kriten-charts/
helm repo update
```

### Copy values.yaml (if necessary) and edit myvalues.yaml
```helm show values kriten/kriten > myvalues.yaml```

### Install
```helm install -f myvalues.yaml kriten kriten/kriten -n kriten --create-namespace```

or

```helm install kriten kriten/kriten -n kriten --create-namespace```

## MacBook Install

Install kubectl: [Install and Set Up kubectl on macOS](https://kubernetes.io/docs/tasks/tools/install-kubectl-macos/)

Install Helm: [Installing Helm](https://helm.sh/docs/intro/install/)

Install Docker Desktop: [Install Docker Desktop on Mac](https://docs.docker.com/desktop/setup/install/mac-install/)

In Docker Desktop settings, enable Kubernetes from the settings page.

When Docker Desktop has restarted, you should have a config file in $HOME/.kube
Check that you have the docker-desktop context and switch to it, and check kubectl is working:
```
kubectl config get-contexts
kubectl config use-context docker-desktop
Switched to context "docker-desktop".

kubectl get nodes
NAME             STATUS   ROLES           AGE    VERSION
docker-desktop   Ready    control-plane   7m4s   v1.32.2
```

Add the Kriten helm repo:
```
helm repo add kriten https://kriten-io.github.io/kriten-charts/
helm repo update
```

Add nodeports:
```
kubectl apply -n kriten -f - <<EOF
apiVersion: v1
kind: Service
metadata:  
  name: kriten-nodeport
spec:
  selector:    
    app: kriten
  type: NodePort
  ports:  
  - name: http
    port: 80
    targetPort: 8080
    nodePort: 30040
---
apiVersion: v1
kind: Service
metadata:  
  name: kriten-frontend-nodeport
spec:
  selector:    
    app: kriten-frontend
  type: NodePort
  ports:  
  - name: http
    port: 80
    targetPort: 80
    nodePort: 30050
EOF
```

Set an environment variable to the IP address of your macbook:
```
export IP_ADDRESS=<your_ip_address>
```

Use helm to install Kriten and the frontend:
```
helm install kriten kriten/kriten -n kriten \
--set frontend.enabled=true \
--set frontend.backendAddress=$IP_ADDRESS':30040'  \
--set frontend.image.repository=kubecodeio/kriten-frontend \
--set frontend.image.tag="latest" \
--namespace kriten --create-namespace
```

You should now be able to connect to the Kriten API:
```
curl -c ./token.txt -X POST 'http://'$IP_ADDRESS':30040/api/v1/login' \
--header 'Content-Type: application/json' \
--data '{
  "username": "root",
  "password": "root",
  "provider": "local"
}' 
```

Which returns a token:
```
{"token":"eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6InJvb3QiLCJ1c2VyX2lkIjoiODJkOTg4NGItZmIxZC00MmQ4LTgxM2MtZTJlYjY1ZDllYmMzIiwicHJvdmlkZXIiOiJsb2NhbCIsImV4cCI6MTc0MTQ1OTkwMn0.zerwoMCIYHM4qE5k3h2rw9chwtWhrr2568zh2_1x5SY"}
```

Browse to "http://"$IP_ADDRESS":30050". 

## Helm Chart Parameters

|Parameter|Description|Default|
|---------|-----------|-------|
|`ingress.enabled`|Ingress configuration enabled|`false`
|`ingress.className`|Ingress class name|`"nginx"`
|`ingress.hosts[0].host`|Ingress host name|`"example.com"`
|`frontend.enabled`|Set to true to install GUI|`false`
|`frontend.backendAddress`| URL for the backend ingress|`"example.com"`
|`replicaCount`|Number of desired Kriten pods|`1`|
|`image.repository`|Kriten Docker image repository|`"kubecodeio/kriten"`|
|`image.tag`|Kriten Docker image tag|`"latest"`|
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
|`jwt.key`|Private key or secret to sign issued JWT|`""`
|`jwt.expiry_seconds`|JWT expiry in seconds|`3600`
|`postgresql.install`|PostgreSQL installed as part of Kriten installation if set to *true*, or use external if *false* |`true`
|`postgresql.host`|PostgreSQL Host for internal or external depending on *postgresql.install* parameter|`"kriten-community-postgresql"`
|`postgresql.port`|PostgreSQL TCP port|`5432`
|`postgresql.image.registry`|PostgreSQL Docker image registry|`docker.io`
|`postgresql.image.repository`|PostgreSQL Docker image repository|`bitnami/postgresql`
|`postgresql.image.tag`|PostgreSQL image tag|`"16"`
|`postgresql.auth.username`|PostgreSQL username|`kriten`
|`postgresql.auth.password`|PostgreSQL password|`kriten`
|`postgresql.auth.database`|PostgreSQL database name|`kriten`
|`postgresql.persistence.enabled`|PostgreSQL database persistnce storage enabled|`true`

