# API Tokens

Programmatic access to Kriten is provided via API tokens (keys). API tokens are generated per user and adhere RBAC rules.

To generate API token, a user need to have a valid login into Kriten. Following CRUD operations are available for the users:

* Add API token

```console
POST /api/v1/api_tokens
```

Body of request:

```json
{
    "description": "My persional API Token",
    "enabled": true,
    "expires": "2024-09-13T13:54:06Z"
}
```

API token object fields reference:

|Key| Description | 
|---------|-----------|
|`description`|(Optional) description of the API token|
|`enabled`|(Optional) state of the API token - true or false, if not specified default will be True|
|`expires`|(Optional) If not specified, will never expire - data will be defaulted to 0000-01-01|

Response json body:

```json
{
    "id": "c38ef92a-522e-41bb-ae5b-ab29a16727d4",
    "owner": "d9acf53d-6d9e-46ec-b352-2e99086ecb97",
    "key": "kri_rbaurEcVyGJIjRioWIaiT3WteVh8ndlVQAEl",
    "description": "My personal API Token",
    "created_at": "2024-09-13T13:58:03.430602592Z",
    "updated_at": "2024-09-13T13:58:03.430602592Z",
    "expires": "2024-09-13T13:54:06.283Z",
    "enabled": true
}
```

|Key| Description | 
|---------|-----------|
|`id`| Unique API token identifier, used for operations against token after creation|
|`key`| *API Token value|
|`owner`| User unique ID, owner of the token|
|`description`| Description of the API token|
|`enabled`| Token is enabled and can be used|
|`expires`|Expiry date and time|
|`created_at`| Date and time, when Token was created|
|`updated_at`| Date and time, when Token was last updated|

Content of field `key` is actual API Token only returned once at the time of Token creation. Token is automatically encryped at store and won't be shown again.

Example using API token with curl command:

```console
curl --header 'Token:kri_rbaurEcVyGJIjRioWIaiT3WteVh8ndlVQAEl' -X GET $KRITEN_URL'/api/v1/runners'
```

* List API tokens

```console
GET /api/v1/api_tokens
```

For non-admin user only own API tokens will be returned, if RBAC permissions not granted to get all.

Admin user will see all tokens by following query:

```console
GET /api/v1/api_tokens/all
```

* Update API token

```console
PATCH /api/v1/api_tokens/c38ef92a-522e-41bb-ae5b-ab29a16727d4
```

Update method can modify *description*, *enabled* and *expires* fields.

* Delete API token

```console
DELETE /api/v1/api_tokens/c38ef92a-522e-41bb-ae5b-ab29a16727d4
```
