# Kriten

### Kriten overview


Kriten is a code execution platform. It is written for and runs on kubernetes as a cloud native application. Kriten exposes containerized applications written in any modern languagues as no-code REST API endpoint, with local or/and AD authentication and granular RBAC it allows requester to execute that code as a kubernetes job and to get result asynchronously or synchronously. 

Key features:
- No-code REST API exposure of custom application and scripts execution.
- Local or/and AD user authentication (Community edition provides only Local authentication).
- Granular RBAC to permission CRUD operations against Kriten configured objects.
- Kriten scales with Kubernetes.


### Configuration flow:

Runner -> Task -> Job

Permission to perform configuration activities against those objects is granted to local or AD users via local Group membership and controlled via granular RBAC.


### Pre-requisites for Applications & Scripts:

* If target application needs secret(s), those are supplied at the time of Task creation as Key/Value pairs and will be stored as Kubernetes Secrets. At the time of execution of a Job against that Task, a K8s Job container will get those secrets mapped as files in /etc/secret directory and as Environmental Vars. Application would need to read those files or Environmental vars to use secrets.
* If target application needs input parameters for execution, those are supplied at the time of Job submission and mapped as Environmental var 'EXTRA_VARS' inside K8s Job container. Application will need to read environmental var 'EXTRA_VAR' in format of json to consume those parameters.

