# Kriten RBAC (Community Edition)

## Table of Content

- [RBAC overview](#rbac-overview)
  -  [Users](#users)
  -  [Roles](#roles)
  -  [Role Bindings](#role-bindings)
- [RBAC Example](#rbac-example)

## RBAC overview

Access to all resource types in Kriten is controlled by flexible and granular RBAC. Key components of RBAC are Users, Roles and Role Bindings.

### Users

### Roles

Builtin Roles:

|Role Name|Resource|Resource IDs|Permission
|---------|-----------|-------|--------|
|`Admin`| * | * | write
|`WriteAllRunners`| runners | * | write
|`WriteAllTasks`| tasks | * | write
|`WriteAllJobs`| jobs | * | write
|`WriteAllUsers`| users | * | write
|`WriteAllRoles`| roles | * | write
|`WriteAllRoleBindings`| role_bindings | * | write

Default Role Binding:

| Role Binding Name | Role Name | Subject Name | Subject Kind | Subject Provider
|-------------------|-----------|--------------|--------------|----------------|
|`RootAdminAccess`| Admin | root | root | local


### Role Bindings

## Built-in Roles


## RBAC Example
