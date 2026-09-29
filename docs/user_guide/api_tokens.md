# API Tokens

Programmatic access to Kriten is provided via API tokens (keys). API tokens are generated per user and adhere RBAC rules.

## List API tokens

Select API Tokens from the account menu top right.
For non-admin user only own API tokens will be returned, if RBAC permissions not granted to get all.
Admin user will see all tokens by following query:

![Kriten API tokens](../assets/kriten-api-tokens.png)

## Add API token

To create a token, select + New from the API Tokens menu.

![New Kriten API token](../assets/kriten-create-api-token.png)

API token object fields reference:

|Key| Description |
|---------|-----------|
|`description`|(Optional) description of the API token|
|`enabled`|(Optional) state of the API token - true or false, if not specified default will be True|
|`expires`|(Optional) If not specified, will never expire - data will be defaulted to 0000-01-01|

Copy the API key

![Kriten API key](../assets/kriten-api-token-created.png)

## Using an API token to run tasks

Put the API token in the request header:

```sh
curl -X 'POST' \
  'http://kriten-lab.192.168.10.190.nip.io/api/v1/tasks/hello-kriten/run' \
  -H 'accept: application/json' \
  -H 'Token: kri_SQnv4YCL7qsLgBY2q22FjTv4y3AtkVfDCcYQ' \
  -H 'Content-Type: application/json' \
  -d '{"greeting": "Hello"}'
```