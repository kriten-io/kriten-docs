# Roles Based Access Control (RBAC)

## Table of Content

- [RBAC overview](#rbac-overview)
- [RBAC Example](#rbac-example)

## RBAC overview

Access to all resource types in Kriten is controlled by flexible and granular RBAC. RBAC controlls "read" or "write" permission to all resource types in Kriten: Runners, Tasks, Jobs, Users, Groups, Roles and Role Bindings. Key components of RBAC are Users, Groups, Roles and Role Bindings, defined as following:

* Users - only local users with provider type 'local' are currently supported in Community Edition. New users are created by root user or by already existing user with RBAC "write" permission to manage Users. Any newly created user doesn't have any default permissions other than login into Kriten.

* Group - permissions are granted by binding roles to local groups, thus user needs to be a member of a group to gain permissions.

* Role - role defines resource type (supported types are 'runners', 'tasks', 'jobs', 'users', 'roles', 'role_bindings') and array of resources of that type and permission: "read" or "write", where "read" allows only to read, and "write" allows everything, including modifications and deletions.

    There are pre-defined built-in roles, which are created at the time of installation of Kriten and cannot be modified or deleted.

    | Role Name              | Resource      | Resource IDs | Permission |
    | ---------------------- | ------------- | ------------ | ---------- |
    | `Admin`                | *             | *            | write      |
    | `WriteAllRunners`      | runners       | *            | write      |
    | `WriteAllTasks`        | tasks         | *            | write      |
    | `WriteAllJobs`         | jobs          | *            | write      |
    | `WriteAllUsers`        | users         | *            | write      |
    | `WriteAllRoles`        | roles         | *            | write      |
    | `WriteAllRoleBindings` | role_bindings | *            | write      |

* Role Binding - bind role to a group.
  
    Only pre-defined built-in Role Binding installed at the time of Kriten initialization is following, which grants Admin group, containing root user, full access to all resources.
    
    | Role Binding Name | Role Name | Subject Name | Subject Kind | Subject Provider |
    | ----------------- | --------- | ------------ | ------------ | ---------------- |
    | RootAdminAccess | Admin | Admin | groups | local |

For REST API swagger documentation refer to http://github.com/kriten-io/kriten-docs.

## RBAC Example

We will demonstrate RBAC on "ansible-command" example, available in https://github.com/kriten-io/kriten-examples repo. This is a simple ansible playbook, which allows execution of show commands on a network devices or a group of devices in inventory.

We will login as root user to create the Runner and the Task as per "ansible-command" example.  Only root user will be able to run Jobs against configured Task. We would like to create a new user, i.e. "user01" and we want that user to be able to run "ansible-command" Task, but not have access to read or modify Runner or Task itself. In example, $KRITEN_URL is set to the URL of your Kriten instance, eg. `export KRITEN_URL=http://kriten-community.kriten.io`.

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

To demonstrate that newly created "user01" doesn't have permission to run "network-command" task, which confirms below by trying it as logged in user "user01":

  Login to Kriten as user "user01":
  
```console
curl -c ./token.txt $KRITEN_URL'/api/v1/login' \
--header 'Content-Type: application/json' \
--data '{
  "username": "user01",
  "password": "p@55w0rd",
  "provider": "local"
}'
```

  Run task "network-command":

```console
curl -b ./token.txt $KRITEN_URL'/api/v1/jobs/network-command' \
--header 'Content-Type: application/json' \
--data '{
  "target_hosts": "arista",
  "command":"show version"
}'
```

  Response:

```json
{
    "error": "unauthorized - user cannot access resource"
}
```
It confirms that by default any user doesn't have permission to run any task.

3. Create Group and add user "user01" to that group.

  Create group "NetworkReadOnly":
  
```console
curl -b ./token.txt $KRITEN_URL'/api/v1/groups' \
--header 'Content-Type: application/json' \
--data '{
    "name": "NetworkReadOnly",
    "provider": "local"
}'
```

  Add user "user01" into group "NetworkReadOnly":

```console
curl -b ./token.txt $KRITEN_URL'/api/v1/groups/NetworkReadOnly/users' \
--header 'Content-Type: application/json' \
--data '[
    {
        "name": "user01",
        "provider": "local"
    }
]'
```
As body contains array, one or more users can be assigned to the group at once.

4. Create a role allowing to "write" to resource type "jobs" for "network-command" task only. That role would allow executing task "network-command" (run/execute jobs).  

```console
curl -b ./token.txt $KRITEN_URL'/api/v1/roles' \
--header 'Content-Type: application/json' \
--data '{
  "name": "NetworkCommandRole",
  "resource": "jobs",
  "resources_ids": [
      "network-command"
  ],
  "access": "write"
}'
```

5. Create role binding between role "NetworkCommandRole" and user "user01".

```console
curl -b ./token.txt $KRITEN_URL'/api/v1/role_bindings' \
--header 'Content-Type: application/json' \
--data '{
  "name": "NetworkCommandRoleBinding",
  "role_name": "NetworkCommandRole",
  "subject_kind": "groups",
  "subject_provider": "local",
  "subject_name": "NetworkReadOnly"
}'
```

As result "user01" is now allowed to run "network-command" task.

```console
url -b ./token.txt $KRITEN_URL'/api/v1/jobs/network-command' \
--header 'Content-Type: application/json' \
--data '{
  "target_hosts": "arista",
  "command": "show version"
}'
```

Which returns a job identifier.
```json
{"msg":"job executed successfully","value":"network-command-ks67g"}
```

Read the job log:
```console
curl -b ./token.txt $KRITEN_URL'/api/v1/jobs/network-command-ks67g/log' \
--header 'Content-Type: application/json'
```
which returns a message.
   
```console
PLAY [Read extra_vars] *********************************************************

TASK [Reading target hosts from input vars and storing as localhost fact] ******
ok: [localhost]

PLAY [Network Configs Backup] **************************************************

TASK [Set command variable] ****************************************************
ok: [evo-eos02]

TASK [Cisco NXOS Command] ******************************************************
skipping: [evo-eos02]

TASK [Cisco IOS Command] *******************************************************
skipping: [evo-eos02]

TASK [Arista EOS Command] ******************************************************
ok: [evo-eos02]
[WARNING]: Platform linux on host evo-eos02 is using the discovered Python
interpreter at /usr/local/bin/python, but future installation of another Python
interpreter could change this. See https://docs.ansible.com/ansible/2.9/referen
ce_appendices/interpreter_discovery.html for more information.

TASK [Print command output into stdout] ****************************************
ok: [evo-eos02] => {
    "msg": [
        "Arista vEOS-lab\nHardware version: \nSerial number: C56AD1FD5F9532C2FD51A852146109EB\nHardware MAC address: 0050.56cd.2b91\nSystem MAC address: 0050.56cd.2b91\n\nSoftware image version: 4.27.0F\nArchitecture: x86_64\nInternal build version: 4.27.0F-24308433.4270F\nInternal build ID: 9088210e-613b-47db-b273-7c7b8d45a086\nImage format version: 1.0\n\nUptime: 9 weeks, 4 days, 18 hours and 16 minutes\nTotal memory: 4002360 kB\nFree memory: 2737704 kB"
    ]
}

PLAY RECAP *********************************************************************
evo-eos02                  : ok=3    changed=0    unreachable=0    failed=0    skipped=2    rescued=0    ignored=0   
localhost                  : ok=1    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0     
```



