# Kriten

### Kriten overview


Kriten is a code execution platform. It is written for and runs on kubernetes as a cloud native application. Kriten exposes containerized applications written in any modern languagues as no-code REST API endpoint, with local or/and AD authentication and granular RBAC it allows requester to execute that code as a kubernetes job and to get result asynchronously. 

Key features:
- No-code REST API exposure of custom application and scripts execution.
- Local or/and AD user authentication.
- Granular RBAC to permission CRUD operations against Kriten configured objects.
- Kriten scales with Kubernetes.


### Configuration flow:

Runner -> Task -> Job

Permission to perform configuration activities against those objects is granted to local or AD users and controlled via granular RBAC.


### Pre-requisites for Applications & Scripts:

* If target application needs secret(s), those are supplied at the time of Task creation and will be stored as Kubernetes Secrets. At the time of execution of the jobs against that Task, job container will get those secrets mapped as files in /etc/secret directory. Application would need to read those files to use secrets.
* If target application needs input parameters for execution, those are supplied at the time of Job submission and will be mapped as Environmental var 'EXTRA_VARS' to the job container. Application will need to read environmental var 'EXTRA_VAR' in format of json to consume those parameters.

### Main compoments:

#### Runner

Runner object defines the following:
* Git project repository and access password/token if repository is private.
* Container image with all libraries, packages and dependencies, needed to run application(s) in the repository.

#### Task

Task is a child object of Runner and defines the following:
* Command to execute application or script from associated by Runner repository in the container.
* Secrets are optionally provided, which are stored as kubernetes secrets and exposed to the job containers at the time of execution as files in /etc/secret/ directory.

Multiple tasks can be associated with the same Runner. It allows exposing same script or application with different parameters as separate tasks, i.e. one allowing only perform read kind operation and another to do write operation and to control via RBAC, which users are allowed to execute jobs against those tasks. 

#### Job

Jobs are triggered against defined Tasks. Permission is controlled via RBAC.

Executor of a Job may need to supply Input parameters as it may be required by application or script at the time of execution. Those Input parameters are provided in the body of REST API request and exposed to job containers as Environmental var 'EXTRA_VARS'. 
