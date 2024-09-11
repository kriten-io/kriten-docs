# Getting Started

This guide will get you started with Kriten. We will use kriten-example repo to demonstrate onboarding a script into kriten and launch it.
By the end of this guide, you will learn how to:

* login into Kriten
* create a Runner
* create a Task
* launch a job against configured Task

Kriten-example repo has several examples. We will be using python script hello-kriten.py. That script demonstrates Kriten capability to expose input parameters and secrets to the automation script at the time of execution - this script simply reads them and prints out into Stdout. Input parameters as supplied at the time of launching a job by a user and exposed as EXTRA_VARS json string in the running container, and secrets supplied at the time of creating a runner by the admin user and those secrets stored as kubernetes secrets and exposed to the automation script as ENV VARS & as files in /etc/secret in a running container.

## Login

Kriten requires user to authenticate. After installation the *local* admin user is created with the following default credentials *root/root*. 

To login into Kriten as following:


```console
curl -c ./token.txt $KRITEN_URL'/api/v1/login' \
--header 'Content-Type: application/json' \
--data '{
  "username": "root",
  "password": "root",
  "provider": "local"
}' 
```

On successful login, Kriten responds with Status 200 and token, which will be stored in ./token.txt file and used in subsequent steps.

Token timeout is defined as a configuration parameter at Kriten's installation, default is 3600 sec.

## Create Runner

Runner creates an environment, or one can think of it as Project, and maps following settings:

* Git repository and branch (Kriten may need a personal access token or PAT if repository is not public)
* Container image, containing all required packages to execute target code from this repo
* Secrets, required for any Tasks in this project, those will be stored as k8s secrets and will be mapped to Job at the time of execution.


```console
curl -b ./token.txt $KRITEN_URL'/api/v1/runners' \
--header 'Content-Type: application/json' \
--data '{
  "name": "kriten-examples",
  "image": "python:3.9-slim",
  "gitURL": "https://github.com/kriten-io/kriten-examples.git",
  "secret": {
      "username": "admin",
      "password": "P@55w0rd!",
      "super_secret": "1234567890!"
  }
}'
```

Body fields reference: 

|Key| Description | 
|---------|-----------|
|`name`|Runner name|
|`gitURL`|Repository with automation scripts and apps|
|`token`|(Optional) token or PAT is needed for non-public repo|
|`branch`|(Optional) Code branch, default is 'main'|
|`image`|Container image from reachable container registry|
|`secret`|Secrets shared with all tasks associated with this runner, map of key/value pairs|

## Add Task

Runner has been created, now we can create a task. Task creates execution endpoint for the target script.

To create task:

```console
curl -b ./token.txt -X POST $KRITEN_URL'/api/v1/tasks' \
--header 'Content-Type: application/json' \
--data '{
  "name": "hello-kriten",
  "runner": "kriten-examples",
  "command": "python hello-kriten/hello-kriten.py"
}'
```

As result, there will be REST API endpoint created for task and available for lunching jobs: `$KRITEN_URL/api/v1/jobs/hello-kriten`

Body fields reference: 

|Key| Description | 
|---------|-----------|
|`name`|Task name|
|`runner`|Runner name this Task is a child of|
|`command`|Command to execute automation script with any parameters|
|`schema`|*(Optional) OpenAPI schema to document and validate input parameters expected by automation script|
|`synchronous`|(Optional) If `true` Kriten will execute Job synchronously with timeout of 25 seconds, otherwise assynchronously, which is default|

*Schema validates job at the start and prevents launching job if input parameters incorrect or missing.

## Launch Job

Launching Job against that Task can be done by an athenticated user if this user got permissions to do so, defined by RBAC. In this guide we will launch the job as the admin user, which is already authenticated (assuming the token hasn't been expired).  

```console
curl -b ./token.txt -X POST $KRITEN_URL'/api/v1/jobs/hello-kriten' \
--header 'Content-Type: application/json' \
--data '{
  "agent_name": "Ethan Hunt",
  "operation":"Mission impossible"
}'
```

That will launch the job against task exposed as REST API endpoint /api/v1/jobs/hello-kriten. Kriten will launch the k8s Job and return Job ID, which then can be used to check statuc of the Job and read result.

Example of returned Job ID:

```json
{"id":"hello-kriten-ks67g", "msg":"job executed successfully"}
```

To check the status of the Job and read result:

```console
curl -b ./token.txt -X GET $KRITEN_URL'/api/v1/jobs/hello-kriten-ks67g' \
--header 'Content-Type: application/json'
```

Example result:
```json
{
  "id": "hello-kriten-ks67g",
  "owner": "root",
  "startTime": "Mon Sep 9 17:11:35 UTC 2024",
  "completionTime": "Mon Sep 9 17:11:40 UTC 2024",
  "failed": 0,
  "completed": 1,
  "stdout": "Hello, Kriten!\n\nThis script demonstrates Kriten's capabilities.\nIt reads input variables (EXTRA_VARS) and secrets, and prints them.\n\n\n^JSON\n\n{\"extra_vars\": {\"agent_name\": \"Ethan Hunt\", \"operation\": \"Mission impossible\"}, \"secrets\": {\"password\": \"P@55w0rd!\", \"username\": \"admin\", \"super_secret\": \"1234567890!\"}}\n^JSON\n\n\n\nScript completed.\n",
  "json_data": {
    "extra_vars": {
      "agent_name": "Ethan Hunt",
      "operation": "Mission impossible"
    },
    "secrets": {
      "password": "P@55w0rd!",
      "super_secret": "1234567890!",
      "username": "admin"
    }
  }
}
```

Kriten has ability to capture json data in the Stdout and return in `json_data` field, if it surrounded by opening and closing delimiter `^JSON`.

Also, Kriten can print out Stdout of executed Job by appending /log to the above request:

```console
curl -b ./token.txt -X GET $KRITEN_URL'/api/v1/jobs/hello-kriten-ks67g/log' \
--header 'Content-Type: application/json'
```

which returns:
```console
Hello, Kriten!

This script demonstrates Kriten's capabilities.
It reads input variables (EXTRA_VARS) and secrets, and prints them.


^JSON

{"extra_vars": {"agent_name": "Ethan Hunt", "operation": "Mission impossible"}, "secrets": {"password": "P@55w0rd!", "username": "admin", "super_secret": "1234567890!"}}
^JSON



Script completed.
```