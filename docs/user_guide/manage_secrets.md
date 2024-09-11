# Secrets

## Table of Content

- [Secrets overview](#secrets-overview)
- [Secrets example](#secrets-example)

## Secrets overview

Automation scripts always need secrets, i.e. tokens or credentials to access infrastructure devices, services, etc. Kriten provides facility to store secrets as Kubernetes secrets and makes them available at the time of Job launching as files in /etc/secret directory and also as environmental vars. Secrets are provisioned by admin users and not visible to executors of Tasks.

Secrets are associated with Runners. Runner defines execution environment - code repository with automation code, container image with all the packages and dependencies needed to run automation code, etc.

```console
POST /api/v1/runners
```

```json
{
  "name": "kriten-examples",
  "image": "python:3.9-slim",
  "gitURL": "https://github.com/kriten-io/kriten-community-toolkit.git",
  "secret": {
      "username": "admin",
      "password": "P@55w0rd!",
      "super_secret": "1234567890!"
  }
}
```

Secrets are defined in the `secret` field of the runner and can be created at the time of Runner creation or patching (update). After secrets created - they are obfuscated and won't be visible via Kriten.

Getting Runner info:

```console
GET /api/v1/runners/kriten-example
```

Produces response, where secrets are hidden and can't be observed.

```json

{
    "secret": {
        "password": "************",
        "super_secret": "************",
        "username": "************"
    },
    "name": "kriten-examples",
    "image": "python:3.9-slim",
    "gitURL": "https://github.com/kriten-io/kriten-community-toolkit.git",
    "token": "",
    "branch": "main"
}
```

Kriten provides endpoint for CRUD operation of secrets as `/api/v1/runners/$RUNNER_NAME/secret`, i.e. for above `/api/v1/runners/kriten-examples/secret`.

* Getting secrets

```console
GET /api/v1/runners/kriten-examples/secret
```

Example response body:

```json
{
    "password": "************",
    "super_secret": "************",
    "username": "************"
}
```

* Delete all secrets associated with the runner:

```console
DELETE /api/v1/runners/kriten-examples/secret
```

* Add secrets to the runner:

```console
POST /api/v1/runners/kriten-examples/secret
```

Body of request:

```json
{
    "username": "admin",
    "password": "P@55w0rd!",
    "super_secret": "1234567890!"
}
```

That will add those secrets to the `kriten-examples` runner.

* Update secrets

```console
POST /api/v1/runners/kriten-examples/secret
```

Body of request:

```json
{
    "mysecret": "sup3r53cr3t!"
}
```

Following rules are applied at updating secrets:

|Condition| Behaviour| 
|---------|-----------|
|secret key and non-empty value already present in stored secrets | No change|
|secret key and non-empty value == "************" (obfuscated) present or not |No change|
|secret key and empty value "" for existing secret | Delete stored secret with matching key|
|secret key and non-empty value non-existing secret | Add new secret|


## Secrets Example

We will demonstrate above on example with curl commands. We will create runner with secretes as above, add a new secret to existing secrets and delete that secret after.

* Login into Kriten.

We will login into Kriten with default credentials as example.

```console
curl -c ./token.txt -X POST $KRITEN_URL'/api/v1/login' \
--header 'Content-Type: application/json' \
--data '{
  "username": "root",
  "password": "root",
  "provider": "local"
}' 
```

* Create Runner with secrets.

```console
curl -b ./token.txt -X POST $KRITEN_URL'/api/v1/runners' \
--header 'Content-Type: application/json' \
--data '{
  "name": "kriten-examples",
  "image": "python:3.9-slim",
  "gitURL": "https://github.com/kriten-io/kriten-community-toolkit.git",
  "secret": {
      "username": "admin",
      "password": "P@55w0rd!",
      "super_secret": "1234567890!"
  }
}'
```

* Get secrets.

```console
curl -b ./token.txt -X GET $KRITEN_URL'/api/v1/runners/kriten-examples/secret'
```

Body of response:

```json
{
    "password": "************",
    "super_secret": "************",
    "username": "************"
}
```

We can also observe secrets by getting runner details as following:

```console
curl -b ./token.txt -X GET $KRITEN_URL'/api/v1/runners/kriten-examples'
```

Body of response:

```json
{
    "secret": {
        "password": "************",
        "super_secret": "************",
        "username": "************"
    },
    "name": "kriten-examples",
    "image": "python:3.9-slim",
    "gitURL": "https://github.com/kriten-io/kriten-community-toolkit.git",
    "token": "",
    "branch": "main"
}
```

* Add new secret to the runner secrets.

```console
curl -b ./token.txt -X POST $KRITEN_URL'/api/v1/runners/kriten-examples/secret' \
--header 'Content-Type: application/json' \
--data '{
    "mysecret": "sup3r53cr3t!"
}' 
```

Body of response, where we can see new secret has been added:

```json
{
    "mysecret":"*************",
    "password":"*************",
    "super_secret":"*************",
    "username":"*************"
}
```

* Delete individual secret.

To delete `mysecret` we will POST again, but this time make value as empty string "".

```console
curl -b ./token.txt -X POST $KRITEN_URL'/api/v1/runners/kriten-examples/secret' \
--header 'Content-Type: application/json' \
--data '{ 
    "mysecret": ""
}' 
```

Body of response will return secrets without `mysecret`:

```json
{
    "password":"*************",
    "super_secret":"*************",
    "username":"*************"
}
```
