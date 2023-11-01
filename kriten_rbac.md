# Kriten RBAC (Community Edition)

## Table of Content

- [RBAC overview](#rbac-overview)
- [RBAC Example](#rbac-example)

## RBAC overview

Access to all resource types in Kriten is controlled by flexible and granular RBAC. RBAC controlls "read" or "write" permission to all resource types in Kriten: Runners, Tasks, Jobs, Users, Roles and Role Binding. Key components of RBAC are Users, Roles and Role Bindings, defined as following:

* Users - only local users with provider type 'local' are currently supported in Community Edition. New users are created by root user or by already existing user with RBAC "write" permission to manage Users. Any newly created user doesn't have any default permissions other than login into Kriten.
  
    Example of creating User (body of request):

    ```json
    {
      "username": "user01",
      "password": "p@55w0rd",
      "provider": "local"
    }
    ```
    Where "provider"="local" is only support option in current release of Community Edition of Kriten and means only locally stored users are supported.

* Roles - Role defines resource type (supported types are 'runners', 'tasks', 'jobs', 'users', 'roles', 'role_bindings') and array of resources of that type and permission: "read" or "write", where "read" allows only to read, and "write" allows everything, including modifications and deletions.

    Example of creating Role (body of request):

    ```json
    {
      "name": "RunHelloKritenRole",
      "resource": "jobs",
      "resources_ids": [
          "hello-kriten"
      ],
      "access": "write"
    }
    ```
    In above example, there Role "RunHelloKritenRole" is being created, which allows execution of Jobs ("write" permission) against Task name "hello-kriten" only. Permission could be granted to multiple Tasks, as resource_ids field is an array.

    There are pre-defined built-in Roles, which are created at the time of installation of Kriten and cannot be modified or deleted:

    |Role Name|Resource|Resource IDs|Permission
    |---------|-----------|-------|--------|
    |`Admin`| * | * | write
    |`WriteAllRunners`| runners | * | write
    |`WriteAllTasks`| tasks | * | write
    |`WriteAllJobs`| jobs | * | write
    |`WriteAllUsers`| users | * | write
    |`WriteAllRoles`| roles | * | write
    |`WriteAllRoleBindings`| role_bindings | * | write

* Role Bindings - Bind Users and Roles.
  
    Example of creating Role Binding (body of request), which binds Role "RuneHelloKritenRole" created above to the user "user01".

    ```json
    {
      "name": "RunHelloKritenRoleBinding",
      "role_name": "RunHelloKritenRole",
      "subject_kind": "users",
      "subject_provider": "local",
      "subject_name": "user01"
    }
    ```
    Where "subject_kind"="users" and "subject_provider"="local" are only supported options in current release of Community Edition of Kriten, "subject_name" specifies user "user01" this binding for.
    
    Only pre-defined built-in Role Binding installed at the time of Kriten initialization is following, which grants root full access to all resources.
    
    | Role Binding Name | Role Name | Subject Name | Subject Kind | Subject Provider
    |-------------------|-----------|--------------|--------------|----------------|
    |`RootAdminAccess`| Admin | root | root | local

For REST API swagger documentation refer to http://github.com/kriten-io/kriten-docs.

## RBAC Example

We will demonstrate RBAC on "hello-kriten" example, available in https://github.com/kriten-io/kriten-examples repo. This is a simple python script, which demonstrates capabilities of Kriten.

We will user root user to create the Runner and the Task as per "hello-kriten" example.  Only root user will be able to run Jobs against configured Task. We would like to create a new user, i.e. "user01" and we want that user to be able to run "hello-kriten" Task. In example, $KRITEN_URL is set to the URL of your Kriten instance, eg. `export KRITEN_URL=http://kriten-community.kriten.io`.

1. Login as root:

```console
curl -c ./token.txt $KRITEN_URL'/api/v1/login' \
--header 'Content-Type: application/json' \
--data '{
  "username": "root",
  "password": "root",
  "provider": "local"
}'
```
Note: cURL stores token in file ./token.txt, which we will use in all following cURL examples.

2. Create user "user01":

```console
curl -b ./token.txt $KRITEN_URL'/api/v1/users' \
--header 'Content-Type: application/json' \
--data '{
  "username": "user01",
  "password": "p@55w0rd",
  "provider": "local"
}'
```

To demonstrate that newly created "user01" doesn't have permission to launch Jobs againt "hello-kriten" Task, which confirm below by trying to launch the Job as logged in user "user01":

```console
curl -b ./token.txt $KRITEN_URL'/api/v1/jobs/hello-kriten' \
--header 'Content-Type: application/json' \
--data '{
  "agent_name": "Ethan Hunt",
  "operation":"Mission impossible"
}'
```

Response:

```json
{
    "error": "unauthorized - user cannot access resource"
}
```

3. Create Role allowing to "write" to resource type "jobs" for "hello-kriten" only.

```console
curl -b ./token.txt $KRITEN_URL'/api/v1/roles' \
--header 'Content-Type: application/json' \
--data '{
  "name": "RunHelloKritenRole",
  "resource": "jobs",
  "resources_ids": [
      "hello-kriten"
  ],
  "access": "write"
}'
```

4. Create Role Binding between Role "RunHelloKritenRole" and user "user01".

We will need unique uuid of the user "user01", provide by Kriten as response to the user creation or can be obtained via GET Users method.

```console
curl -b ./token.txt $KRITEN_URL'/api/v1/roles' \
--header 'Content-Type: application/json' \
--data '{
  "name": "RunHelloKritenRoleBinding",
  "role_name": "RunHelloKritenRole",
  "subject_kind": "users",
  "subject_provider": "local",
  "subject_name": "user01"
}'
```

As result "user01" is now allowed to launch Jobs against "hello-kriten" Task.

```console
curl -b ./token.txt $KRITEN_URL'/api/v1/jobs/hello-kriten' \
--header 'Content-Type: application/json' \
--data '{
  "agent_name": "Ethan Hunt",
  "operation":"Mission impossible"
}'
```

Which returns a job identifier.
```json
{"msg":"job executed successfully","value":"hello-kriten-ks67g"}
```

Read the job output.
```console
curl -b ./token.txt $KRITEN_URL'/api/v1/jobs/hello-kriten-ks67g' \
--header 'Content-Type: application/json'
```
   which returns a message.
   
```console
Hello, Kriten!

This script demonstrates Kriten's capabilities.
It reads input variables (EXTRA_VARS) and secrets, and prints them.


{'extra_vars': {'agent_name': 'Ethan Hunt', 'operation': 'Mission impossible'},
 'secrets': {'password': 'P@55w0rd!',
             'super_secret': '1234567890!',
             'username': 'admin'}}


Script completed.
```


