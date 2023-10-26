


# Swagger Kriten
API Gateway for your kubernetes services.
  

## Informations

### Version

v0.3

### License

[Apache 2.0](http://www.apache.org/licenses/LICENSE-2.0.html)

### Contact

Evolvere Support info@evolvere-tech.co.uk https://www.evolvere-tech.co.uk/contact

### Terms Of Service

http://swagger.io/terms/

## Content negotiation

### URI Schemes
  * http

### Consumes
  * application/json

### Produces
  * application/json

## Access control

### Security Schemes

#### Bearer (header: Authorization)

Type "Bearer" followed by a space and JWT token.

> **Type**: apikey

## All endpoints

###  authenticate

| Method  | URI     | Name   | Summary |
|---------|---------|--------|---------|
| GET | /api/v1/refresh | [get refresh](#get-refresh) | Auth admin |
| POST | /api/v1/login | [post login](#post-login) | Authenticate users |
  


###  jobs

| Method  | URI     | Name   | Summary |
|---------|---------|--------|---------|
| GET | /api/v1/jobs | [get jobs](#get-jobs) | List all jobs |
| GET | /api/v1/jobs/{id} | [get jobs ID](#get-jobs-id) | Get a job |
| POST | /api/v1/jobs | [post jobs](#post-jobs) | Create a new job |
  


###  rolebindings

| Method  | URI     | Name   | Summary |
|---------|---------|--------|---------|
| DELETE | /api/v1/role_bindings/{id} | [delete role bindings ID](#delete-role-bindings-id) | Delete a role binding |
| GET | /api/v1/role_bindings | [get role bindings](#get-role-bindings) | List all role bindings |
| GET | /api/v1/role_bindings/{id} | [get role bindings ID](#get-role-bindings-id) | Get a role binding |
| PATCH | /api/v1/role_bindings/{id} | [patch role bindings ID](#patch-role-bindings-id) | Update a role binding |
| POST | /api/v1/role_bindings | [post role bindings](#post-role-bindings) | Create a new role binding |
  


###  roles

| Method  | URI     | Name   | Summary |
|---------|---------|--------|---------|
| DELETE | /api/v1/roles/{id} | [delete roles ID](#delete-roles-id) | Delete a role |
| GET | /api/v1/roles | [get roles](#get-roles) | List all roles |
| GET | /api/v1/roles/{id} | [get roles ID](#get-roles-id) | Get a role |
| PATCH | /api/v1/roles/{id} | [patch roles ID](#patch-roles-id) | Update a role |
| POST | /api/v1/roles | [post roles](#post-roles) | Create a new role |
  


###  runners

| Method  | URI     | Name   | Summary |
|---------|---------|--------|---------|
| DELETE | /api/v1/runners/{rname} | [delete runners rname](#delete-runners-rname) | Delete a runner |
| GET | /api/v1/runners | [get runners](#get-runners) | List all runners |
| GET | /api/v1/runners/{rname} | [get runners rname](#get-runners-rname) | Get a runner |
| PATCH | /api/v1/runners/{rname} | [patch runners rname](#patch-runners-rname) | Update a runner |
| POST | /api/v1/runners | [post runners](#post-runners) | Create a new runner |
  


###  tasks

| Method  | URI     | Name   | Summary |
|---------|---------|--------|---------|
| DELETE | /api/v1/tasks/{id} | [delete tasks ID](#delete-tasks-id) | Delete a task |
| GET | /api/v1/tasks | [get tasks](#get-tasks) | List all tasks |
| GET | /api/v1/tasks/{id} | [get tasks ID](#get-tasks-id) | Get a task |
| PATCH | /api/v1/tasks/{id} | [patch tasks ID](#patch-tasks-id) | Update a task |
| POST | /api/v1/tasks | [post tasks](#post-tasks) | Create a new task |
  


###  users

| Method  | URI     | Name   | Summary |
|---------|---------|--------|---------|
| DELETE | /api/v1/users/{id} | [delete users ID](#delete-users-id) | Delete a user |
| GET | /api/v1/users | [get users](#get-users) | List all users |
| GET | /api/v1/users/{id} | [get users ID](#get-users-id) | Get a user |
| PATCH | /api/v1/users/{id} | [patch users ID](#patch-users-id) | Update a user |
| POST | /api/v1/users | [post users](#post-users) | Create a new user |
  


## Paths

### <span id="delete-role-bindings-id"></span> Delete a role binding (*DeleteRoleBindingsID*)

```
DELETE /api/v1/role_bindings/{id}
```

Delete by role binding ID

#### Consumes
  * application/json

#### Produces
  * application/json

#### Security Requirements
  * Bearer

#### Parameters

| Name | Source | Type | Go type | Separator | Required | Default | Description |
|------|--------|------|---------|-----------| :------: |---------|-------------|
| id | `path` | string | `string` |  | ✓ |  | RoleBinding ID |

#### All responses
| Code | Status | Description | Has headers | Schema |
|------|--------|-------------|:-----------:|--------|
| [204](#delete-role-bindings-id-204) | No Content | No Content |  | [schema](#delete-role-bindings-id-204-schema) |
| [400](#delete-role-bindings-id-400) | Bad Request | Bad Request |  | [schema](#delete-role-bindings-id-400-schema) |
| [404](#delete-role-bindings-id-404) | Not Found | Not Found |  | [schema](#delete-role-bindings-id-404-schema) |
| [500](#delete-role-bindings-id-500) | Internal Server Error | Internal Server Error |  | [schema](#delete-role-bindings-id-500-schema) |

#### Responses


##### <span id="delete-role-bindings-id-204"></span> 204 - No Content
Status: No Content

###### <span id="delete-role-bindings-id-204-schema"></span> Schema
   
  

[ModelsRoleBinding](#models-role-binding)

##### <span id="delete-role-bindings-id-400"></span> 400 - Bad Request
Status: Bad Request

###### <span id="delete-role-bindings-id-400-schema"></span> Schema
   
  

[HelpersHTTPError](#helpers-http-error)

##### <span id="delete-role-bindings-id-404"></span> 404 - Not Found
Status: Not Found

###### <span id="delete-role-bindings-id-404-schema"></span> Schema
   
  

[HelpersHTTPError](#helpers-http-error)

##### <span id="delete-role-bindings-id-500"></span> 500 - Internal Server Error
Status: Internal Server Error

###### <span id="delete-role-bindings-id-500-schema"></span> Schema
   
  

[HelpersHTTPError](#helpers-http-error)

### <span id="delete-roles-id"></span> Delete a role (*DeleteRolesID*)

```
DELETE /api/v1/roles/{id}
```

Delete by role ID

#### Consumes
  * application/json

#### Produces
  * application/json

#### Security Requirements
  * Bearer

#### Parameters

| Name | Source | Type | Go type | Separator | Required | Default | Description |
|------|--------|------|---------|-----------| :------: |---------|-------------|
| id | `path` | string | `string` |  | ✓ |  | Role ID |

#### All responses
| Code | Status | Description | Has headers | Schema |
|------|--------|-------------|:-----------:|--------|
| [204](#delete-roles-id-204) | No Content | No Content |  | [schema](#delete-roles-id-204-schema) |
| [400](#delete-roles-id-400) | Bad Request | Bad Request |  | [schema](#delete-roles-id-400-schema) |
| [404](#delete-roles-id-404) | Not Found | Not Found |  | [schema](#delete-roles-id-404-schema) |
| [500](#delete-roles-id-500) | Internal Server Error | Internal Server Error |  | [schema](#delete-roles-id-500-schema) |

#### Responses


##### <span id="delete-roles-id-204"></span> 204 - No Content
Status: No Content

###### <span id="delete-roles-id-204-schema"></span> Schema
   
  

[ModelsRole](#models-role)

##### <span id="delete-roles-id-400"></span> 400 - Bad Request
Status: Bad Request

###### <span id="delete-roles-id-400-schema"></span> Schema
   
  

[HelpersHTTPError](#helpers-http-error)

##### <span id="delete-roles-id-404"></span> 404 - Not Found
Status: Not Found

###### <span id="delete-roles-id-404-schema"></span> Schema
   
  

[HelpersHTTPError](#helpers-http-error)

##### <span id="delete-roles-id-500"></span> 500 - Internal Server Error
Status: Internal Server Error

###### <span id="delete-roles-id-500-schema"></span> Schema
   
  

[HelpersHTTPError](#helpers-http-error)

### <span id="delete-runners-rname"></span> Delete a runner (*DeleteRunnersRname*)

```
DELETE /api/v1/runners/{rname}
```

Delete by runner name

#### Consumes
  * application/json

#### Produces
  * application/json

#### Security Requirements
  * Bearer

#### Parameters

| Name | Source | Type | Go type | Separator | Required | Default | Description |
|------|--------|------|---------|-----------| :------: |---------|-------------|
| rname | `path` | string | `string` |  | ✓ |  | Runner name |

#### All responses
| Code | Status | Description | Has headers | Schema |
|------|--------|-------------|:-----------:|--------|
| [204](#delete-runners-rname-204) | No Content | No Content |  | [schema](#delete-runners-rname-204-schema) |
| [400](#delete-runners-rname-400) | Bad Request | Bad Request |  | [schema](#delete-runners-rname-400-schema) |
| [404](#delete-runners-rname-404) | Not Found | Not Found |  | [schema](#delete-runners-rname-404-schema) |
| [500](#delete-runners-rname-500) | Internal Server Error | Internal Server Error |  | [schema](#delete-runners-rname-500-schema) |

#### Responses


##### <span id="delete-runners-rname-204"></span> 204 - No Content
Status: No Content

###### <span id="delete-runners-rname-204-schema"></span> Schema
   
  

[ModelsRunner](#models-runner)

##### <span id="delete-runners-rname-400"></span> 400 - Bad Request
Status: Bad Request

###### <span id="delete-runners-rname-400-schema"></span> Schema
   
  

[HelpersHTTPError](#helpers-http-error)

##### <span id="delete-runners-rname-404"></span> 404 - Not Found
Status: Not Found

###### <span id="delete-runners-rname-404-schema"></span> Schema
   
  

[HelpersHTTPError](#helpers-http-error)

##### <span id="delete-runners-rname-500"></span> 500 - Internal Server Error
Status: Internal Server Error

###### <span id="delete-runners-rname-500-schema"></span> Schema
   
  

[HelpersHTTPError](#helpers-http-error)

### <span id="delete-tasks-id"></span> Delete a task (*DeleteTasksID*)

```
DELETE /api/v1/tasks/{id}
```

Delete by task name

#### Consumes
  * application/json

#### Produces
  * application/json

#### Security Requirements
  * Bearer

#### Parameters

| Name | Source | Type | Go type | Separator | Required | Default | Description |
|------|--------|------|---------|-----------| :------: |---------|-------------|
| id | `path` | string | `string` |  | ✓ |  | Task name |

#### All responses
| Code | Status | Description | Has headers | Schema |
|------|--------|-------------|:-----------:|--------|
| [204](#delete-tasks-id-204) | No Content | No Content |  | [schema](#delete-tasks-id-204-schema) |
| [400](#delete-tasks-id-400) | Bad Request | Bad Request |  | [schema](#delete-tasks-id-400-schema) |
| [404](#delete-tasks-id-404) | Not Found | Not Found |  | [schema](#delete-tasks-id-404-schema) |
| [500](#delete-tasks-id-500) | Internal Server Error | Internal Server Error |  | [schema](#delete-tasks-id-500-schema) |

#### Responses


##### <span id="delete-tasks-id-204"></span> 204 - No Content
Status: No Content

###### <span id="delete-tasks-id-204-schema"></span> Schema
   
  

[ModelsTask](#models-task)

##### <span id="delete-tasks-id-400"></span> 400 - Bad Request
Status: Bad Request

###### <span id="delete-tasks-id-400-schema"></span> Schema
   
  

[HelpersHTTPError](#helpers-http-error)

##### <span id="delete-tasks-id-404"></span> 404 - Not Found
Status: Not Found

###### <span id="delete-tasks-id-404-schema"></span> Schema
   
  

[HelpersHTTPError](#helpers-http-error)

##### <span id="delete-tasks-id-500"></span> 500 - Internal Server Error
Status: Internal Server Error

###### <span id="delete-tasks-id-500-schema"></span> Schema
   
  

[HelpersHTTPError](#helpers-http-error)

### <span id="delete-users-id"></span> Delete a user (*DeleteUsersID*)

```
DELETE /api/v1/users/{id}
```

Delete by user ID

#### Consumes
  * application/json

#### Produces
  * application/json

#### Security Requirements
  * Bearer

#### Parameters

| Name | Source | Type | Go type | Separator | Required | Default | Description |
|------|--------|------|---------|-----------| :------: |---------|-------------|
| id | `path` | string | `string` |  | ✓ |  | User ID |

#### All responses
| Code | Status | Description | Has headers | Schema |
|------|--------|-------------|:-----------:|--------|
| [204](#delete-users-id-204) | No Content | No Content |  | [schema](#delete-users-id-204-schema) |
| [400](#delete-users-id-400) | Bad Request | Bad Request |  | [schema](#delete-users-id-400-schema) |
| [404](#delete-users-id-404) | Not Found | Not Found |  | [schema](#delete-users-id-404-schema) |
| [500](#delete-users-id-500) | Internal Server Error | Internal Server Error |  | [schema](#delete-users-id-500-schema) |

#### Responses


##### <span id="delete-users-id-204"></span> 204 - No Content
Status: No Content

###### <span id="delete-users-id-204-schema"></span> Schema
   
  

[ModelsUser](#models-user)

##### <span id="delete-users-id-400"></span> 400 - Bad Request
Status: Bad Request

###### <span id="delete-users-id-400-schema"></span> Schema
   
  

[HelpersHTTPError](#helpers-http-error)

##### <span id="delete-users-id-404"></span> 404 - Not Found
Status: Not Found

###### <span id="delete-users-id-404-schema"></span> Schema
   
  

[HelpersHTTPError](#helpers-http-error)

##### <span id="delete-users-id-500"></span> 500 - Internal Server Error
Status: Internal Server Error

###### <span id="delete-users-id-500-schema"></span> Schema
   
  

[HelpersHTTPError](#helpers-http-error)

### <span id="get-jobs"></span> List all jobs (*GetJobs*)

```
GET /api/v1/jobs
```

List all jobs

#### Consumes
  * application/json

#### Produces
  * application/json

#### Security Requirements
  * Bearer

#### All responses
| Code | Status | Description | Has headers | Schema |
|------|--------|-------------|:-----------:|--------|
| [200](#get-jobs-200) | OK | OK |  | [schema](#get-jobs-200-schema) |
| [400](#get-jobs-400) | Bad Request | Bad Request |  | [schema](#get-jobs-400-schema) |
| [404](#get-jobs-404) | Not Found | Not Found |  | [schema](#get-jobs-404-schema) |
| [500](#get-jobs-500) | Internal Server Error | Internal Server Error |  | [schema](#get-jobs-500-schema) |

#### Responses


##### <span id="get-jobs-200"></span> 200 - OK
Status: OK

###### <span id="get-jobs-200-schema"></span> Schema
   
  

[]string

##### <span id="get-jobs-400"></span> 400 - Bad Request
Status: Bad Request

###### <span id="get-jobs-400-schema"></span> Schema
   
  

[HelpersHTTPError](#helpers-http-error)

##### <span id="get-jobs-404"></span> 404 - Not Found
Status: Not Found

###### <span id="get-jobs-404-schema"></span> Schema
   
  

[HelpersHTTPError](#helpers-http-error)

##### <span id="get-jobs-500"></span> 500 - Internal Server Error
Status: Internal Server Error

###### <span id="get-jobs-500-schema"></span> Schema
   
  

[HelpersHTTPError](#helpers-http-error)

### <span id="get-jobs-id"></span> Get a job (*GetJobsID*)

```
GET /api/v1/jobs/{id}
```

Get information about a specific job

#### Consumes
  * application/json

#### Produces
  * application/json

#### Security Requirements
  * Bearer

#### Parameters

| Name | Source | Type | Go type | Separator | Required | Default | Description |
|------|--------|------|---------|-----------| :------: |---------|-------------|
| id | `path` | string | `string` |  | ✓ |  | Job  id |

#### All responses
| Code | Status | Description | Has headers | Schema |
|------|--------|-------------|:-----------:|--------|
| [200](#get-jobs-id-200) | OK | OK |  | [schema](#get-jobs-id-200-schema) |
| [400](#get-jobs-id-400) | Bad Request | Bad Request |  | [schema](#get-jobs-id-400-schema) |
| [404](#get-jobs-id-404) | Not Found | Not Found |  | [schema](#get-jobs-id-404-schema) |
| [500](#get-jobs-id-500) | Internal Server Error | Internal Server Error |  | [schema](#get-jobs-id-500-schema) |

#### Responses


##### <span id="get-jobs-id-200"></span> 200 - OK
Status: OK

###### <span id="get-jobs-id-200-schema"></span> Schema
   
  

[ModelsTask](#models-task)

##### <span id="get-jobs-id-400"></span> 400 - Bad Request
Status: Bad Request

###### <span id="get-jobs-id-400-schema"></span> Schema
   
  

[HelpersHTTPError](#helpers-http-error)

##### <span id="get-jobs-id-404"></span> 404 - Not Found
Status: Not Found

###### <span id="get-jobs-id-404-schema"></span> Schema
   
  

[HelpersHTTPError](#helpers-http-error)

##### <span id="get-jobs-id-500"></span> 500 - Internal Server Error
Status: Internal Server Error

###### <span id="get-jobs-id-500-schema"></span> Schema
   
  

[HelpersHTTPError](#helpers-http-error)

### <span id="get-refresh"></span> Auth admin (*GetRefresh*)

```
GET /api/v1/refresh
```

Refresh time limit of a JWT token

#### Consumes
  * application/json

#### Produces
  * application/json

#### Security Requirements
  * Bearer

#### Parameters

| Name | Source | Type | Go type | Separator | Required | Default | Description |
|------|--------|------|---------|-----------| :------: |---------|-------------|
| token | `header` | string | `string` |  |  |  | JWT Token can be provided as Cookie |

#### All responses
| Code | Status | Description | Has headers | Schema |
|------|--------|-------------|:-----------:|--------|
| [200](#get-refresh-200) | OK | OK |  | [schema](#get-refresh-200-schema) |
| [400](#get-refresh-400) | Bad Request | Bad Request |  | [schema](#get-refresh-400-schema) |
| [401](#get-refresh-401) | Unauthorized | Unauthorized |  | [schema](#get-refresh-401-schema) |
| [404](#get-refresh-404) | Not Found | Not Found |  | [schema](#get-refresh-404-schema) |
| [500](#get-refresh-500) | Internal Server Error | Internal Server Error |  | [schema](#get-refresh-500-schema) |

#### Responses


##### <span id="get-refresh-200"></span> 200 - OK
Status: OK

###### <span id="get-refresh-200-schema"></span> Schema
   
  



##### <span id="get-refresh-400"></span> 400 - Bad Request
Status: Bad Request

###### <span id="get-refresh-400-schema"></span> Schema
   
  

[HelpersHTTPError](#helpers-http-error)

##### <span id="get-refresh-401"></span> 401 - Unauthorized
Status: Unauthorized

###### <span id="get-refresh-401-schema"></span> Schema
   
  

[HelpersHTTPError](#helpers-http-error)

##### <span id="get-refresh-404"></span> 404 - Not Found
Status: Not Found

###### <span id="get-refresh-404-schema"></span> Schema
   
  

[HelpersHTTPError](#helpers-http-error)

##### <span id="get-refresh-500"></span> 500 - Internal Server Error
Status: Internal Server Error

###### <span id="get-refresh-500-schema"></span> Schema
   
  

[HelpersHTTPError](#helpers-http-error)

### <span id="get-role-bindings"></span> List all role bindings (*GetRoleBindings*)

```
GET /api/v1/role_bindings
```

List all roles bindings available on the cluster

#### Consumes
  * application/json

#### Produces
  * application/json

#### Security Requirements
  * Bearer

#### All responses
| Code | Status | Description | Has headers | Schema |
|------|--------|-------------|:-----------:|--------|
| [200](#get-role-bindings-200) | OK | OK |  | [schema](#get-role-bindings-200-schema) |
| [400](#get-role-bindings-400) | Bad Request | Bad Request |  | [schema](#get-role-bindings-400-schema) |
| [404](#get-role-bindings-404) | Not Found | Not Found |  | [schema](#get-role-bindings-404-schema) |
| [500](#get-role-bindings-500) | Internal Server Error | Internal Server Error |  | [schema](#get-role-bindings-500-schema) |

#### Responses


##### <span id="get-role-bindings-200"></span> 200 - OK
Status: OK

###### <span id="get-role-bindings-200-schema"></span> Schema
   
  

[][ModelsRoleBinding](#models-role-binding)

##### <span id="get-role-bindings-400"></span> 400 - Bad Request
Status: Bad Request

###### <span id="get-role-bindings-400-schema"></span> Schema
   
  

[HelpersHTTPError](#helpers-http-error)

##### <span id="get-role-bindings-404"></span> 404 - Not Found
Status: Not Found

###### <span id="get-role-bindings-404-schema"></span> Schema
   
  

[HelpersHTTPError](#helpers-http-error)

##### <span id="get-role-bindings-500"></span> 500 - Internal Server Error
Status: Internal Server Error

###### <span id="get-role-bindings-500-schema"></span> Schema
   
  

[HelpersHTTPError](#helpers-http-error)

### <span id="get-role-bindings-id"></span> Get a role binding (*GetRoleBindingsID*)

```
GET /api/v1/role_bindings/{id}
```

Get information about a specific role binding

#### Consumes
  * application/json

#### Produces
  * application/json

#### Security Requirements
  * Bearer

#### Parameters

| Name | Source | Type | Go type | Separator | Required | Default | Description |
|------|--------|------|---------|-----------| :------: |---------|-------------|
| id | `path` | string | `string` |  | ✓ |  | RoleBinding ID |

#### All responses
| Code | Status | Description | Has headers | Schema |
|------|--------|-------------|:-----------:|--------|
| [200](#get-role-bindings-id-200) | OK | OK |  | [schema](#get-role-bindings-id-200-schema) |
| [400](#get-role-bindings-id-400) | Bad Request | Bad Request |  | [schema](#get-role-bindings-id-400-schema) |
| [404](#get-role-bindings-id-404) | Not Found | Not Found |  | [schema](#get-role-bindings-id-404-schema) |
| [500](#get-role-bindings-id-500) | Internal Server Error | Internal Server Error |  | [schema](#get-role-bindings-id-500-schema) |

#### Responses


##### <span id="get-role-bindings-id-200"></span> 200 - OK
Status: OK

###### <span id="get-role-bindings-id-200-schema"></span> Schema
   
  

[ModelsRoleBinding](#models-role-binding)

##### <span id="get-role-bindings-id-400"></span> 400 - Bad Request
Status: Bad Request

###### <span id="get-role-bindings-id-400-schema"></span> Schema
   
  

[HelpersHTTPError](#helpers-http-error)

##### <span id="get-role-bindings-id-404"></span> 404 - Not Found
Status: Not Found

###### <span id="get-role-bindings-id-404-schema"></span> Schema
   
  

[HelpersHTTPError](#helpers-http-error)

##### <span id="get-role-bindings-id-500"></span> 500 - Internal Server Error
Status: Internal Server Error

###### <span id="get-role-bindings-id-500-schema"></span> Schema
   
  

[HelpersHTTPError](#helpers-http-error)

### <span id="get-roles"></span> List all roles (*GetRoles*)

```
GET /api/v1/roles
```

List all roles available on the cluster

#### Consumes
  * application/json

#### Produces
  * application/json

#### Security Requirements
  * Bearer

#### All responses
| Code | Status | Description | Has headers | Schema |
|------|--------|-------------|:-----------:|--------|
| [200](#get-roles-200) | OK | OK |  | [schema](#get-roles-200-schema) |
| [400](#get-roles-400) | Bad Request | Bad Request |  | [schema](#get-roles-400-schema) |
| [404](#get-roles-404) | Not Found | Not Found |  | [schema](#get-roles-404-schema) |
| [500](#get-roles-500) | Internal Server Error | Internal Server Error |  | [schema](#get-roles-500-schema) |

#### Responses


##### <span id="get-roles-200"></span> 200 - OK
Status: OK

###### <span id="get-roles-200-schema"></span> Schema
   
  

[][ModelsRole](#models-role)

##### <span id="get-roles-400"></span> 400 - Bad Request
Status: Bad Request

###### <span id="get-roles-400-schema"></span> Schema
   
  

[HelpersHTTPError](#helpers-http-error)

##### <span id="get-roles-404"></span> 404 - Not Found
Status: Not Found

###### <span id="get-roles-404-schema"></span> Schema
   
  

[HelpersHTTPError](#helpers-http-error)

##### <span id="get-roles-500"></span> 500 - Internal Server Error
Status: Internal Server Error

###### <span id="get-roles-500-schema"></span> Schema
   
  

[HelpersHTTPError](#helpers-http-error)

### <span id="get-roles-id"></span> Get a role (*GetRolesID*)

```
GET /api/v1/roles/{id}
```

Get information about a specific role

#### Consumes
  * application/json

#### Produces
  * application/json

#### Security Requirements
  * Bearer

#### Parameters

| Name | Source | Type | Go type | Separator | Required | Default | Description |
|------|--------|------|---------|-----------| :------: |---------|-------------|
| id | `path` | string | `string` |  | ✓ |  | Role ID |

#### All responses
| Code | Status | Description | Has headers | Schema |
|------|--------|-------------|:-----------:|--------|
| [200](#get-roles-id-200) | OK | OK |  | [schema](#get-roles-id-200-schema) |
| [400](#get-roles-id-400) | Bad Request | Bad Request |  | [schema](#get-roles-id-400-schema) |
| [404](#get-roles-id-404) | Not Found | Not Found |  | [schema](#get-roles-id-404-schema) |
| [500](#get-roles-id-500) | Internal Server Error | Internal Server Error |  | [schema](#get-roles-id-500-schema) |

#### Responses


##### <span id="get-roles-id-200"></span> 200 - OK
Status: OK

###### <span id="get-roles-id-200-schema"></span> Schema
   
  

[ModelsRole](#models-role)

##### <span id="get-roles-id-400"></span> 400 - Bad Request
Status: Bad Request

###### <span id="get-roles-id-400-schema"></span> Schema
   
  

[HelpersHTTPError](#helpers-http-error)

##### <span id="get-roles-id-404"></span> 404 - Not Found
Status: Not Found

###### <span id="get-roles-id-404-schema"></span> Schema
   
  

[HelpersHTTPError](#helpers-http-error)

##### <span id="get-roles-id-500"></span> 500 - Internal Server Error
Status: Internal Server Error

###### <span id="get-roles-id-500-schema"></span> Schema
   
  

[HelpersHTTPError](#helpers-http-error)

### <span id="get-runners"></span> List all runners (*GetRunners*)

```
GET /api/v1/runners
```

List all runners available on the cluster

#### Consumes
  * application/json

#### Produces
  * application/json

#### Security Requirements
  * Bearer

#### All responses
| Code | Status | Description | Has headers | Schema |
|------|--------|-------------|:-----------:|--------|
| [200](#get-runners-200) | OK | OK |  | [schema](#get-runners-200-schema) |
| [400](#get-runners-400) | Bad Request | Bad Request |  | [schema](#get-runners-400-schema) |
| [404](#get-runners-404) | Not Found | Not Found |  | [schema](#get-runners-404-schema) |
| [500](#get-runners-500) | Internal Server Error | Internal Server Error |  | [schema](#get-runners-500-schema) |

#### Responses


##### <span id="get-runners-200"></span> 200 - OK
Status: OK

###### <span id="get-runners-200-schema"></span> Schema
   
  

[][ModelsRunner](#models-runner)

##### <span id="get-runners-400"></span> 400 - Bad Request
Status: Bad Request

###### <span id="get-runners-400-schema"></span> Schema
   
  

[HelpersHTTPError](#helpers-http-error)

##### <span id="get-runners-404"></span> 404 - Not Found
Status: Not Found

###### <span id="get-runners-404-schema"></span> Schema
   
  

[HelpersHTTPError](#helpers-http-error)

##### <span id="get-runners-500"></span> 500 - Internal Server Error
Status: Internal Server Error

###### <span id="get-runners-500-schema"></span> Schema
   
  

[HelpersHTTPError](#helpers-http-error)

### <span id="get-runners-rname"></span> Get a runner (*GetRunnersRname*)

```
GET /api/v1/runners/{rname}
```

Get information about a specific runner

#### Consumes
  * application/json

#### Produces
  * application/json

#### Security Requirements
  * Bearer

#### Parameters

| Name | Source | Type | Go type | Separator | Required | Default | Description |
|------|--------|------|---------|-----------| :------: |---------|-------------|
| rname | `path` | string | `string` |  | ✓ |  | Runner name |

#### All responses
| Code | Status | Description | Has headers | Schema |
|------|--------|-------------|:-----------:|--------|
| [200](#get-runners-rname-200) | OK | OK |  | [schema](#get-runners-rname-200-schema) |
| [400](#get-runners-rname-400) | Bad Request | Bad Request |  | [schema](#get-runners-rname-400-schema) |
| [404](#get-runners-rname-404) | Not Found | Not Found |  | [schema](#get-runners-rname-404-schema) |
| [500](#get-runners-rname-500) | Internal Server Error | Internal Server Error |  | [schema](#get-runners-rname-500-schema) |

#### Responses


##### <span id="get-runners-rname-200"></span> 200 - OK
Status: OK

###### <span id="get-runners-rname-200-schema"></span> Schema
   
  

[ModelsRunner](#models-runner)

##### <span id="get-runners-rname-400"></span> 400 - Bad Request
Status: Bad Request

###### <span id="get-runners-rname-400-schema"></span> Schema
   
  

[HelpersHTTPError](#helpers-http-error)

##### <span id="get-runners-rname-404"></span> 404 - Not Found
Status: Not Found

###### <span id="get-runners-rname-404-schema"></span> Schema
   
  

[HelpersHTTPError](#helpers-http-error)

##### <span id="get-runners-rname-500"></span> 500 - Internal Server Error
Status: Internal Server Error

###### <span id="get-runners-rname-500-schema"></span> Schema
   
  

[HelpersHTTPError](#helpers-http-error)

### <span id="get-tasks"></span> List all tasks (*GetTasks*)

```
GET /api/v1/tasks
```

List all tasks available on the cluster

#### Consumes
  * application/json

#### Produces
  * application/json

#### Security Requirements
  * Bearer

#### All responses
| Code | Status | Description | Has headers | Schema |
|------|--------|-------------|:-----------:|--------|
| [200](#get-tasks-200) | OK | OK |  | [schema](#get-tasks-200-schema) |
| [400](#get-tasks-400) | Bad Request | Bad Request |  | [schema](#get-tasks-400-schema) |
| [404](#get-tasks-404) | Not Found | Not Found |  | [schema](#get-tasks-404-schema) |
| [500](#get-tasks-500) | Internal Server Error | Internal Server Error |  | [schema](#get-tasks-500-schema) |

#### Responses


##### <span id="get-tasks-200"></span> 200 - OK
Status: OK

###### <span id="get-tasks-200-schema"></span> Schema
   
  

[][ModelsTask](#models-task)

##### <span id="get-tasks-400"></span> 400 - Bad Request
Status: Bad Request

###### <span id="get-tasks-400-schema"></span> Schema
   
  

[HelpersHTTPError](#helpers-http-error)

##### <span id="get-tasks-404"></span> 404 - Not Found
Status: Not Found

###### <span id="get-tasks-404-schema"></span> Schema
   
  

[HelpersHTTPError](#helpers-http-error)

##### <span id="get-tasks-500"></span> 500 - Internal Server Error
Status: Internal Server Error

###### <span id="get-tasks-500-schema"></span> Schema
   
  

[HelpersHTTPError](#helpers-http-error)

### <span id="get-tasks-id"></span> Get a task (*GetTasksID*)

```
GET /api/v1/tasks/{id}
```

Get information about a specific task

#### Consumes
  * application/json

#### Produces
  * application/json

#### Security Requirements
  * Bearer

#### Parameters

| Name | Source | Type | Go type | Separator | Required | Default | Description |
|------|--------|------|---------|-----------| :------: |---------|-------------|
| id | `path` | string | `string` |  | ✓ |  | Task name |

#### All responses
| Code | Status | Description | Has headers | Schema |
|------|--------|-------------|:-----------:|--------|
| [200](#get-tasks-id-200) | OK | OK |  | [schema](#get-tasks-id-200-schema) |
| [400](#get-tasks-id-400) | Bad Request | Bad Request |  | [schema](#get-tasks-id-400-schema) |
| [404](#get-tasks-id-404) | Not Found | Not Found |  | [schema](#get-tasks-id-404-schema) |
| [500](#get-tasks-id-500) | Internal Server Error | Internal Server Error |  | [schema](#get-tasks-id-500-schema) |

#### Responses


##### <span id="get-tasks-id-200"></span> 200 - OK
Status: OK

###### <span id="get-tasks-id-200-schema"></span> Schema
   
  

[ModelsTask](#models-task)

##### <span id="get-tasks-id-400"></span> 400 - Bad Request
Status: Bad Request

###### <span id="get-tasks-id-400-schema"></span> Schema
   
  

[HelpersHTTPError](#helpers-http-error)

##### <span id="get-tasks-id-404"></span> 404 - Not Found
Status: Not Found

###### <span id="get-tasks-id-404-schema"></span> Schema
   
  

[HelpersHTTPError](#helpers-http-error)

##### <span id="get-tasks-id-500"></span> 500 - Internal Server Error
Status: Internal Server Error

###### <span id="get-tasks-id-500-schema"></span> Schema
   
  

[HelpersHTTPError](#helpers-http-error)

### <span id="get-users"></span> List all users (*GetUsers*)

```
GET /api/v1/users
```

List all users available on the cluster

#### Consumes
  * application/json

#### Produces
  * application/json

#### Security Requirements
  * Bearer

#### All responses
| Code | Status | Description | Has headers | Schema |
|------|--------|-------------|:-----------:|--------|
| [200](#get-users-200) | OK | OK |  | [schema](#get-users-200-schema) |
| [400](#get-users-400) | Bad Request | Bad Request |  | [schema](#get-users-400-schema) |
| [404](#get-users-404) | Not Found | Not Found |  | [schema](#get-users-404-schema) |
| [500](#get-users-500) | Internal Server Error | Internal Server Error |  | [schema](#get-users-500-schema) |

#### Responses


##### <span id="get-users-200"></span> 200 - OK
Status: OK

###### <span id="get-users-200-schema"></span> Schema
   
  

[][ModelsUser](#models-user)

##### <span id="get-users-400"></span> 400 - Bad Request
Status: Bad Request

###### <span id="get-users-400-schema"></span> Schema
   
  

[HelpersHTTPError](#helpers-http-error)

##### <span id="get-users-404"></span> 404 - Not Found
Status: Not Found

###### <span id="get-users-404-schema"></span> Schema
   
  

[HelpersHTTPError](#helpers-http-error)

##### <span id="get-users-500"></span> 500 - Internal Server Error
Status: Internal Server Error

###### <span id="get-users-500-schema"></span> Schema
   
  

[HelpersHTTPError](#helpers-http-error)

### <span id="get-users-id"></span> Get a user (*GetUsersID*)

```
GET /api/v1/users/{id}
```

Get information about a specific user

#### Consumes
  * application/json

#### Produces
  * application/json

#### Security Requirements
  * Bearer

#### Parameters

| Name | Source | Type | Go type | Separator | Required | Default | Description |
|------|--------|------|---------|-----------| :------: |---------|-------------|
| id | `path` | string | `string` |  | ✓ |  | User ID |

#### All responses
| Code | Status | Description | Has headers | Schema |
|------|--------|-------------|:-----------:|--------|
| [200](#get-users-id-200) | OK | OK |  | [schema](#get-users-id-200-schema) |
| [400](#get-users-id-400) | Bad Request | Bad Request |  | [schema](#get-users-id-400-schema) |
| [404](#get-users-id-404) | Not Found | Not Found |  | [schema](#get-users-id-404-schema) |
| [500](#get-users-id-500) | Internal Server Error | Internal Server Error |  | [schema](#get-users-id-500-schema) |

#### Responses


##### <span id="get-users-id-200"></span> 200 - OK
Status: OK

###### <span id="get-users-id-200-schema"></span> Schema
   
  

[ModelsUser](#models-user)

##### <span id="get-users-id-400"></span> 400 - Bad Request
Status: Bad Request

###### <span id="get-users-id-400-schema"></span> Schema
   
  

[HelpersHTTPError](#helpers-http-error)

##### <span id="get-users-id-404"></span> 404 - Not Found
Status: Not Found

###### <span id="get-users-id-404-schema"></span> Schema
   
  

[HelpersHTTPError](#helpers-http-error)

##### <span id="get-users-id-500"></span> 500 - Internal Server Error
Status: Internal Server Error

###### <span id="get-users-id-500-schema"></span> Schema
   
  

[HelpersHTTPError](#helpers-http-error)

### <span id="patch-role-bindings-id"></span> Update a role binding (*PatchRoleBindingsID*)

```
PATCH /api/v1/role_bindings/{id}
```

Update a role binding in the cluster

#### Consumes
  * application/json

#### Produces
  * application/json

#### Security Requirements
  * Bearer

#### Parameters

| Name | Source | Type | Go type | Separator | Required | Default | Description |
|------|--------|------|---------|-----------| :------: |---------|-------------|
| id | `path` | string | `string` |  | ✓ |  | RoleBinding ID |
| role | `body` | [ModelsRoleBinding](#models-role-binding) | `models.ModelsRoleBinding` | | ✓ | | Update role |

#### All responses
| Code | Status | Description | Has headers | Schema |
|------|--------|-------------|:-----------:|--------|
| [200](#patch-role-bindings-id-200) | OK | OK |  | [schema](#patch-role-bindings-id-200-schema) |
| [400](#patch-role-bindings-id-400) | Bad Request | Bad Request |  | [schema](#patch-role-bindings-id-400-schema) |
| [404](#patch-role-bindings-id-404) | Not Found | Not Found |  | [schema](#patch-role-bindings-id-404-schema) |
| [500](#patch-role-bindings-id-500) | Internal Server Error | Internal Server Error |  | [schema](#patch-role-bindings-id-500-schema) |

#### Responses


##### <span id="patch-role-bindings-id-200"></span> 200 - OK
Status: OK

###### <span id="patch-role-bindings-id-200-schema"></span> Schema
   
  

[ModelsRoleBinding](#models-role-binding)

##### <span id="patch-role-bindings-id-400"></span> 400 - Bad Request
Status: Bad Request

###### <span id="patch-role-bindings-id-400-schema"></span> Schema
   
  

[HelpersHTTPError](#helpers-http-error)

##### <span id="patch-role-bindings-id-404"></span> 404 - Not Found
Status: Not Found

###### <span id="patch-role-bindings-id-404-schema"></span> Schema
   
  

[HelpersHTTPError](#helpers-http-error)

##### <span id="patch-role-bindings-id-500"></span> 500 - Internal Server Error
Status: Internal Server Error

###### <span id="patch-role-bindings-id-500-schema"></span> Schema
   
  

[HelpersHTTPError](#helpers-http-error)

### <span id="patch-roles-id"></span> Update a role (*PatchRolesID*)

```
PATCH /api/v1/roles/{id}
```

Update a role in the cluster

#### Consumes
  * application/json

#### Produces
  * application/json

#### Security Requirements
  * Bearer

#### Parameters

| Name | Source | Type | Go type | Separator | Required | Default | Description |
|------|--------|------|---------|-----------| :------: |---------|-------------|
| id | `path` | string | `string` |  | ✓ |  | Role ID |
| role | `body` | [ModelsRole](#models-role) | `models.ModelsRole` | | ✓ | | Update role |

#### All responses
| Code | Status | Description | Has headers | Schema |
|------|--------|-------------|:-----------:|--------|
| [200](#patch-roles-id-200) | OK | OK |  | [schema](#patch-roles-id-200-schema) |
| [400](#patch-roles-id-400) | Bad Request | Bad Request |  | [schema](#patch-roles-id-400-schema) |
| [404](#patch-roles-id-404) | Not Found | Not Found |  | [schema](#patch-roles-id-404-schema) |
| [500](#patch-roles-id-500) | Internal Server Error | Internal Server Error |  | [schema](#patch-roles-id-500-schema) |

#### Responses


##### <span id="patch-roles-id-200"></span> 200 - OK
Status: OK

###### <span id="patch-roles-id-200-schema"></span> Schema
   
  

[ModelsRole](#models-role)

##### <span id="patch-roles-id-400"></span> 400 - Bad Request
Status: Bad Request

###### <span id="patch-roles-id-400-schema"></span> Schema
   
  

[HelpersHTTPError](#helpers-http-error)

##### <span id="patch-roles-id-404"></span> 404 - Not Found
Status: Not Found

###### <span id="patch-roles-id-404-schema"></span> Schema
   
  

[HelpersHTTPError](#helpers-http-error)

##### <span id="patch-roles-id-500"></span> 500 - Internal Server Error
Status: Internal Server Error

###### <span id="patch-roles-id-500-schema"></span> Schema
   
  

[HelpersHTTPError](#helpers-http-error)

### <span id="patch-runners-rname"></span> Update a runner (*PatchRunnersRname*)

```
PATCH /api/v1/runners/{rname}
```

Update a runner in the cluster

#### Consumes
  * application/json

#### Produces
  * application/json

#### Security Requirements
  * Bearer

#### Parameters

| Name | Source | Type | Go type | Separator | Required | Default | Description |
|------|--------|------|---------|-----------| :------: |---------|-------------|
| rname | `path` | string | `string` |  | ✓ |  | Runner name |
| runner | `body` | [ModelsRunner](#models-runner) | `models.ModelsRunner` | | ✓ | | Update runner |

#### All responses
| Code | Status | Description | Has headers | Schema |
|------|--------|-------------|:-----------:|--------|
| [200](#patch-runners-rname-200) | OK | OK |  | [schema](#patch-runners-rname-200-schema) |
| [400](#patch-runners-rname-400) | Bad Request | Bad Request |  | [schema](#patch-runners-rname-400-schema) |
| [404](#patch-runners-rname-404) | Not Found | Not Found |  | [schema](#patch-runners-rname-404-schema) |
| [500](#patch-runners-rname-500) | Internal Server Error | Internal Server Error |  | [schema](#patch-runners-rname-500-schema) |

#### Responses


##### <span id="patch-runners-rname-200"></span> 200 - OK
Status: OK

###### <span id="patch-runners-rname-200-schema"></span> Schema
   
  

[ModelsRunner](#models-runner)

##### <span id="patch-runners-rname-400"></span> 400 - Bad Request
Status: Bad Request

###### <span id="patch-runners-rname-400-schema"></span> Schema
   
  

[HelpersHTTPError](#helpers-http-error)

##### <span id="patch-runners-rname-404"></span> 404 - Not Found
Status: Not Found

###### <span id="patch-runners-rname-404-schema"></span> Schema
   
  

[HelpersHTTPError](#helpers-http-error)

##### <span id="patch-runners-rname-500"></span> 500 - Internal Server Error
Status: Internal Server Error

###### <span id="patch-runners-rname-500-schema"></span> Schema
   
  

[HelpersHTTPError](#helpers-http-error)

### <span id="patch-tasks-id"></span> Update a task (*PatchTasksID*)

```
PATCH /api/v1/tasks/{id}
```

Update a task in the cluster

#### Consumes
  * application/json

#### Produces
  * application/json

#### Security Requirements
  * Bearer

#### Parameters

| Name | Source | Type | Go type | Separator | Required | Default | Description |
|------|--------|------|---------|-----------| :------: |---------|-------------|
| id | `path` | string | `string` |  | ✓ |  | Task name |
| task | `body` | [ModelsTask](#models-task) | `models.ModelsTask` | | ✓ | | Update task |

#### All responses
| Code | Status | Description | Has headers | Schema |
|------|--------|-------------|:-----------:|--------|
| [200](#patch-tasks-id-200) | OK | OK |  | [schema](#patch-tasks-id-200-schema) |
| [400](#patch-tasks-id-400) | Bad Request | Bad Request |  | [schema](#patch-tasks-id-400-schema) |
| [404](#patch-tasks-id-404) | Not Found | Not Found |  | [schema](#patch-tasks-id-404-schema) |
| [500](#patch-tasks-id-500) | Internal Server Error | Internal Server Error |  | [schema](#patch-tasks-id-500-schema) |

#### Responses


##### <span id="patch-tasks-id-200"></span> 200 - OK
Status: OK

###### <span id="patch-tasks-id-200-schema"></span> Schema
   
  

[ModelsTask](#models-task)

##### <span id="patch-tasks-id-400"></span> 400 - Bad Request
Status: Bad Request

###### <span id="patch-tasks-id-400-schema"></span> Schema
   
  

[HelpersHTTPError](#helpers-http-error)

##### <span id="patch-tasks-id-404"></span> 404 - Not Found
Status: Not Found

###### <span id="patch-tasks-id-404-schema"></span> Schema
   
  

[HelpersHTTPError](#helpers-http-error)

##### <span id="patch-tasks-id-500"></span> 500 - Internal Server Error
Status: Internal Server Error

###### <span id="patch-tasks-id-500-schema"></span> Schema
   
  

[HelpersHTTPError](#helpers-http-error)

### <span id="patch-users-id"></span> Update a user (*PatchUsersID*)

```
PATCH /api/v1/users/{id}
```

Update a user in the cluster

#### Consumes
  * application/json

#### Produces
  * application/json

#### Security Requirements
  * Bearer

#### Parameters

| Name | Source | Type | Go type | Separator | Required | Default | Description |
|------|--------|------|---------|-----------| :------: |---------|-------------|
| id | `path` | string | `string` |  | ✓ |  | User ID |
| user | `body` | [ModelsUser](#models-user) | `models.ModelsUser` | | ✓ | | Update user |

#### All responses
| Code | Status | Description | Has headers | Schema |
|------|--------|-------------|:-----------:|--------|
| [200](#patch-users-id-200) | OK | OK |  | [schema](#patch-users-id-200-schema) |
| [400](#patch-users-id-400) | Bad Request | Bad Request |  | [schema](#patch-users-id-400-schema) |
| [404](#patch-users-id-404) | Not Found | Not Found |  | [schema](#patch-users-id-404-schema) |
| [500](#patch-users-id-500) | Internal Server Error | Internal Server Error |  | [schema](#patch-users-id-500-schema) |

#### Responses


##### <span id="patch-users-id-200"></span> 200 - OK
Status: OK

###### <span id="patch-users-id-200-schema"></span> Schema
   
  

[ModelsUser](#models-user)

##### <span id="patch-users-id-400"></span> 400 - Bad Request
Status: Bad Request

###### <span id="patch-users-id-400-schema"></span> Schema
   
  

[HelpersHTTPError](#helpers-http-error)

##### <span id="patch-users-id-404"></span> 404 - Not Found
Status: Not Found

###### <span id="patch-users-id-404-schema"></span> Schema
   
  

[HelpersHTTPError](#helpers-http-error)

##### <span id="patch-users-id-500"></span> 500 - Internal Server Error
Status: Internal Server Error

###### <span id="patch-users-id-500-schema"></span> Schema
   
  

[HelpersHTTPError](#helpers-http-error)

### <span id="post-jobs"></span> Create a new job (*PostJobs*)

```
POST /api/v1/jobs
```

Add a job to the cluster

#### Consumes
  * application/json

#### Produces
  * application/json

#### Security Requirements
  * Bearer

#### Parameters

| Name | Source | Type | Go type | Separator | Required | Default | Description |
|------|--------|------|---------|-----------| :------: |---------|-------------|
| evars | `body` | [interface{}](#interface) | `interface{}` | |  | | Extra vars |

#### All responses
| Code | Status | Description | Has headers | Schema |
|------|--------|-------------|:-----------:|--------|
| [200](#post-jobs-200) | OK | OK |  | [schema](#post-jobs-200-schema) |
| [400](#post-jobs-400) | Bad Request | Bad Request |  | [schema](#post-jobs-400-schema) |
| [404](#post-jobs-404) | Not Found | Not Found |  | [schema](#post-jobs-404-schema) |
| [500](#post-jobs-500) | Internal Server Error | Internal Server Error |  | [schema](#post-jobs-500-schema) |

#### Responses


##### <span id="post-jobs-200"></span> 200 - OK
Status: OK

###### <span id="post-jobs-200-schema"></span> Schema
   
  

[ModelsTask](#models-task)

##### <span id="post-jobs-400"></span> 400 - Bad Request
Status: Bad Request

###### <span id="post-jobs-400-schema"></span> Schema
   
  

[HelpersHTTPError](#helpers-http-error)

##### <span id="post-jobs-404"></span> 404 - Not Found
Status: Not Found

###### <span id="post-jobs-404-schema"></span> Schema
   
  

[HelpersHTTPError](#helpers-http-error)

##### <span id="post-jobs-500"></span> 500 - Internal Server Error
Status: Internal Server Error

###### <span id="post-jobs-500-schema"></span> Schema
   
  

[HelpersHTTPError](#helpers-http-error)

### <span id="post-login"></span> Authenticate users (*PostLogin*)

```
POST /api/v1/login
```

authenticate and generates a JWT token

#### Consumes
  * application/json

#### Produces
  * application/json

#### Parameters

| Name | Source | Type | Go type | Separator | Required | Default | Description |
|------|--------|------|---------|-----------| :------: |---------|-------------|
| credentials | `body` | [ModelsCredentials](#models-credentials) | `models.ModelsCredentials` | | ✓ | | Your Active Directory credentials |

#### All responses
| Code | Status | Description | Has headers | Schema |
|------|--------|-------------|:-----------:|--------|
| [200](#post-login-200) | OK | OK |  | [schema](#post-login-200-schema) |
| [400](#post-login-400) | Bad Request | Bad Request |  | [schema](#post-login-400-schema) |
| [401](#post-login-401) | Unauthorized | Unauthorized |  | [schema](#post-login-401-schema) |
| [404](#post-login-404) | Not Found | Not Found |  | [schema](#post-login-404-schema) |
| [500](#post-login-500) | Internal Server Error | Internal Server Error |  | [schema](#post-login-500-schema) |

#### Responses


##### <span id="post-login-200"></span> 200 - OK
Status: OK

###### <span id="post-login-200-schema"></span> Schema
   
  



##### <span id="post-login-400"></span> 400 - Bad Request
Status: Bad Request

###### <span id="post-login-400-schema"></span> Schema
   
  

[HelpersHTTPError](#helpers-http-error)

##### <span id="post-login-401"></span> 401 - Unauthorized
Status: Unauthorized

###### <span id="post-login-401-schema"></span> Schema
   
  

[HelpersHTTPError](#helpers-http-error)

##### <span id="post-login-404"></span> 404 - Not Found
Status: Not Found

###### <span id="post-login-404-schema"></span> Schema
   
  

[HelpersHTTPError](#helpers-http-error)

##### <span id="post-login-500"></span> 500 - Internal Server Error
Status: Internal Server Error

###### <span id="post-login-500-schema"></span> Schema
   
  

[HelpersHTTPError](#helpers-http-error)

### <span id="post-role-bindings"></span> Create a new role binding (*PostRoleBindings*)

```
POST /api/v1/role_bindings
```

Add a role binding to the cluster

#### Consumes
  * application/json

#### Produces
  * application/json

#### Security Requirements
  * Bearer

#### Parameters

| Name | Source | Type | Go type | Separator | Required | Default | Description |
|------|--------|------|---------|-----------| :------: |---------|-------------|
| roleBinding | `body` | [ModelsRoleBinding](#models-role-binding) | `models.ModelsRoleBinding` | | ✓ | | New role binding |

#### All responses
| Code | Status | Description | Has headers | Schema |
|------|--------|-------------|:-----------:|--------|
| [200](#post-role-bindings-200) | OK | OK |  | [schema](#post-role-bindings-200-schema) |
| [400](#post-role-bindings-400) | Bad Request | Bad Request |  | [schema](#post-role-bindings-400-schema) |
| [404](#post-role-bindings-404) | Not Found | Not Found |  | [schema](#post-role-bindings-404-schema) |
| [500](#post-role-bindings-500) | Internal Server Error | Internal Server Error |  | [schema](#post-role-bindings-500-schema) |

#### Responses


##### <span id="post-role-bindings-200"></span> 200 - OK
Status: OK

###### <span id="post-role-bindings-200-schema"></span> Schema
   
  

[ModelsRoleBinding](#models-role-binding)

##### <span id="post-role-bindings-400"></span> 400 - Bad Request
Status: Bad Request

###### <span id="post-role-bindings-400-schema"></span> Schema
   
  

[HelpersHTTPError](#helpers-http-error)

##### <span id="post-role-bindings-404"></span> 404 - Not Found
Status: Not Found

###### <span id="post-role-bindings-404-schema"></span> Schema
   
  

[HelpersHTTPError](#helpers-http-error)

##### <span id="post-role-bindings-500"></span> 500 - Internal Server Error
Status: Internal Server Error

###### <span id="post-role-bindings-500-schema"></span> Schema
   
  

[HelpersHTTPError](#helpers-http-error)

### <span id="post-roles"></span> Create a new role (*PostRoles*)

```
POST /api/v1/roles
```

Add a role to the cluster

#### Consumes
  * application/json

#### Produces
  * application/json

#### Security Requirements
  * Bearer

#### Parameters

| Name | Source | Type | Go type | Separator | Required | Default | Description |
|------|--------|------|---------|-----------| :------: |---------|-------------|
| role | `body` | [ModelsRole](#models-role) | `models.ModelsRole` | | ✓ | | New role |

#### All responses
| Code | Status | Description | Has headers | Schema |
|------|--------|-------------|:-----------:|--------|
| [200](#post-roles-200) | OK | OK |  | [schema](#post-roles-200-schema) |
| [400](#post-roles-400) | Bad Request | Bad Request |  | [schema](#post-roles-400-schema) |
| [404](#post-roles-404) | Not Found | Not Found |  | [schema](#post-roles-404-schema) |
| [500](#post-roles-500) | Internal Server Error | Internal Server Error |  | [schema](#post-roles-500-schema) |

#### Responses


##### <span id="post-roles-200"></span> 200 - OK
Status: OK

###### <span id="post-roles-200-schema"></span> Schema
   
  

[ModelsRole](#models-role)

##### <span id="post-roles-400"></span> 400 - Bad Request
Status: Bad Request

###### <span id="post-roles-400-schema"></span> Schema
   
  

[HelpersHTTPError](#helpers-http-error)

##### <span id="post-roles-404"></span> 404 - Not Found
Status: Not Found

###### <span id="post-roles-404-schema"></span> Schema
   
  

[HelpersHTTPError](#helpers-http-error)

##### <span id="post-roles-500"></span> 500 - Internal Server Error
Status: Internal Server Error

###### <span id="post-roles-500-schema"></span> Schema
   
  

[HelpersHTTPError](#helpers-http-error)

### <span id="post-runners"></span> Create a new runner (*PostRunners*)

```
POST /api/v1/runners
```

Add a runner to the cluster

#### Consumes
  * application/json

#### Produces
  * application/json

#### Security Requirements
  * Bearer

#### Parameters

| Name | Source | Type | Go type | Separator | Required | Default | Description |
|------|--------|------|---------|-----------| :------: |---------|-------------|
| runner | `body` | [ModelsRunner](#models-runner) | `models.ModelsRunner` | | ✓ | | New runner |

#### All responses
| Code | Status | Description | Has headers | Schema |
|------|--------|-------------|:-----------:|--------|
| [200](#post-runners-200) | OK | OK |  | [schema](#post-runners-200-schema) |
| [400](#post-runners-400) | Bad Request | Bad Request |  | [schema](#post-runners-400-schema) |
| [404](#post-runners-404) | Not Found | Not Found |  | [schema](#post-runners-404-schema) |
| [500](#post-runners-500) | Internal Server Error | Internal Server Error |  | [schema](#post-runners-500-schema) |

#### Responses


##### <span id="post-runners-200"></span> 200 - OK
Status: OK

###### <span id="post-runners-200-schema"></span> Schema
   
  

[ModelsRunner](#models-runner)

##### <span id="post-runners-400"></span> 400 - Bad Request
Status: Bad Request

###### <span id="post-runners-400-schema"></span> Schema
   
  

[HelpersHTTPError](#helpers-http-error)

##### <span id="post-runners-404"></span> 404 - Not Found
Status: Not Found

###### <span id="post-runners-404-schema"></span> Schema
   
  

[HelpersHTTPError](#helpers-http-error)

##### <span id="post-runners-500"></span> 500 - Internal Server Error
Status: Internal Server Error

###### <span id="post-runners-500-schema"></span> Schema
   
  

[HelpersHTTPError](#helpers-http-error)

### <span id="post-tasks"></span> Create a new task (*PostTasks*)

```
POST /api/v1/tasks
```

Add a task to the cluster

#### Consumes
  * application/json

#### Produces
  * application/json

#### Security Requirements
  * Bearer

#### Parameters

| Name | Source | Type | Go type | Separator | Required | Default | Description |
|------|--------|------|---------|-----------| :------: |---------|-------------|
| task | `body` | [ModelsTask](#models-task) | `models.ModelsTask` | | ✓ | | New task |

#### All responses
| Code | Status | Description | Has headers | Schema |
|------|--------|-------------|:-----------:|--------|
| [200](#post-tasks-200) | OK | OK |  | [schema](#post-tasks-200-schema) |
| [400](#post-tasks-400) | Bad Request | Bad Request |  | [schema](#post-tasks-400-schema) |
| [404](#post-tasks-404) | Not Found | Not Found |  | [schema](#post-tasks-404-schema) |
| [500](#post-tasks-500) | Internal Server Error | Internal Server Error |  | [schema](#post-tasks-500-schema) |

#### Responses


##### <span id="post-tasks-200"></span> 200 - OK
Status: OK

###### <span id="post-tasks-200-schema"></span> Schema
   
  

[ModelsTask](#models-task)

##### <span id="post-tasks-400"></span> 400 - Bad Request
Status: Bad Request

###### <span id="post-tasks-400-schema"></span> Schema
   
  

[HelpersHTTPError](#helpers-http-error)

##### <span id="post-tasks-404"></span> 404 - Not Found
Status: Not Found

###### <span id="post-tasks-404-schema"></span> Schema
   
  

[HelpersHTTPError](#helpers-http-error)

##### <span id="post-tasks-500"></span> 500 - Internal Server Error
Status: Internal Server Error

###### <span id="post-tasks-500-schema"></span> Schema
   
  

[HelpersHTTPError](#helpers-http-error)

### <span id="post-users"></span> Create a new user (*PostUsers*)

```
POST /api/v1/users
```

Add a user to the cluster

#### Consumes
  * application/json

#### Produces
  * application/json

#### Security Requirements
  * Bearer

#### Parameters

| Name | Source | Type | Go type | Separator | Required | Default | Description |
|------|--------|------|---------|-----------| :------: |---------|-------------|
| user | `body` | [ModelsUser](#models-user) | `models.ModelsUser` | | ✓ | | New user |

#### All responses
| Code | Status | Description | Has headers | Schema |
|------|--------|-------------|:-----------:|--------|
| [200](#post-users-200) | OK | OK |  | [schema](#post-users-200-schema) |
| [400](#post-users-400) | Bad Request | Bad Request |  | [schema](#post-users-400-schema) |
| [404](#post-users-404) | Not Found | Not Found |  | [schema](#post-users-404-schema) |
| [500](#post-users-500) | Internal Server Error | Internal Server Error |  | [schema](#post-users-500-schema) |

#### Responses


##### <span id="post-users-200"></span> 200 - OK
Status: OK

###### <span id="post-users-200-schema"></span> Schema
   
  

[ModelsUser](#models-user)

##### <span id="post-users-400"></span> 400 - Bad Request
Status: Bad Request

###### <span id="post-users-400-schema"></span> Schema
   
  

[HelpersHTTPError](#helpers-http-error)

##### <span id="post-users-404"></span> 404 - Not Found
Status: Not Found

###### <span id="post-users-404-schema"></span> Schema
   
  

[HelpersHTTPError](#helpers-http-error)

##### <span id="post-users-500"></span> 500 - Internal Server Error
Status: Internal Server Error

###### <span id="post-users-500-schema"></span> Schema
   
  

[HelpersHTTPError](#helpers-http-error)

## Models

### <span id="helpers-http-error"></span> helpers.HTTPError


  



**Properties**

| Name | Type | Go type | Required | Default | Description | Example |
|------|------|---------|:--------:| ------- |-------------|---------|
| code | integer| `int64` |  | |  | `400` |
| message | string| `string` |  | |  | `status bad request` |



### <span id="models-credentials"></span> models.Credentials


  



**Properties**

| Name | Type | Go type | Required | Default | Description | Example |
|------|------|---------|:--------:| ------- |-------------|---------|
| password | string| `string` |  | |  |  |
| provider | string| `string` |  | |  |  |
| username | string| `string` |  | |  |  |



### <span id="models-role"></span> models.Role


  



**Properties**

| Name | Type | Go type | Required | Default | Description | Example |
|------|------|---------|:--------:| ------- |-------------|---------|
| access | string| `string` |  | |  |  |
| created_at | string| `string` |  | |  |  |
| name | string| `string` |  | |  |  |
| resource | string| `string` |  | |  |  |
| resources_ids | []string| `[]string` |  | |  |  |
| role_id | string| `string` |  | |  |  |
| updated_at | string| `string` |  | |  |  |



### <span id="models-role-binding"></span> models.RoleBinding


  



**Properties**

| Name | Type | Go type | Required | Default | Description | Example |
|------|------|---------|:--------:| ------- |-------------|---------|
| created_at | string| `string` |  | |  |  |
| name | string| `string` |  | |  |  |
| role_binding_id | string| `string` |  | |  |  |
| role_id | string| `string` |  | |  |  |
| subject_id | string| `string` |  | |  |  |
| subject_kind | string| `string` |  | |  |  |
| subject_provider | string| `string` |  | |  |  |
| updated_at | string| `string` |  | |  |  |



### <span id="models-runner"></span> models.Runner


  



**Properties**

| Name | Type | Go type | Required | Default | Description | Example |
|------|------|---------|:--------:| ------- |-------------|---------|
| accessGroups | string| `string` |  | |  |  |
| gitURL | string| `string` |  | |  |  |
| id | string| `string` |  | |  |  |
| image | string| `string` |  | |  |  |
| token | string| `string` |  | |  |  |



### <span id="models-task"></span> models.Task


  



**Properties**

| Name | Type | Go type | Required | Default | Description | Example |
|------|------|---------|:--------:| ------- |-------------|---------|
| accessGroups | string| `string` |  | |  |  |
| command | string| `string` |  | |  |  |
| id | string| `string` |  | |  |  |
| runner | string| `string` |  | |  |  |
| secret | map of string| `map[string]string` |  | |  |  |
| synchronous | boolean| `bool` |  | |  |  |



### <span id="models-user"></span> models.User


  



**Properties**

| Name | Type | Go type | Required | Default | Description | Example |
|------|------|---------|:--------:| ------- |-------------|---------|
| created_at | string| `string` |  | |  |  |
| password | string| `string` |  | |  |  |
| provider | string| `string` |  | |  |  |
| updated_at | string| `string` |  | |  |  |
| user_id | string| `string` |  | |  |  |
| username | string| `string` |  | |  |  |


