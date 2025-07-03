# Cronjob objects

Any task in Kriten can be executed on repatable schedule via cronjob object.

*API documentation is available via swagger $KRITEN_URL/swagger/index.html*

where $KRITEN_URL is set to the URL of your Kriten instance.


## Configure cronjob for Kriten task

Let's take simple python script "hello-kriten" from examples in https://github.com/kriten-io/kriten-community-toolkit repo. That is a simple script, which demonstrates Kriten ability to inject secrets and input parameters into python script at the time of execution. First, create a hello-kriten task following easy steps from README for hello-kriten.

Checking that "hello-kriten" task has been created.

* Login: 

```console
curl -c ./token.txt -X POST $KRITEN_URL'/api/v1/login' \
--header 'Content-Type: application/json' \
--data '{
  "username": "root",
  "password": "root",
  "provider": "local"
}' 
```

* Get task hello-kriten:

```console
curl -b ./token.txt -X GET $KRITEN_URL'/api/v1/tasks/hell-kriten' \
--header 'Content-Type: application/json'
```

Returns:
```json
{"name":"hello-kriten",
 "runner":"python",
 "command":"python examples/hello-kriten/hello-kriten.py",
 "synchronous":false}
```

* Create cronjob object for "hello-kriten" task

Let's create cronjob object to run "hello-kriten" with following extra_vars parameters every 5 minutes.

```console
curl -b ./token.txt -X POST $KRITEN_URL'/api/v1/login' \
--header 'Content-Type: application/json' \
--data '{
    "name": "hello-kriten-cronjob",
    "task": "hello-kriten",
    "schedule": "*/5 * * * *",
    "disable": false,
    "extra_vars": {
        "agent_name": "Ethan Hunt",
        "operation":"Mission impossible"
    }
}' 
```

|Key| Description | 
|---------|-----------|
|`name`| unique name of the cronjob object|
|`task`| existing task name to be executed on schedule|
|`schedule`| schedule based on Cron syntax|
|`disabled`| boolean true or false - disables cronjob, default is set to false|
|`extra_vars`| input parameters, exposed to custom code via EXTRA_VARS env var as json string|


* Cron syntax:

```console
# ┌───────────── minute (0 - 59)
# │ ┌───────────── hour (0 - 23)
# │ │ ┌───────────── day of the month (1 - 31)
# │ │ │ ┌───────────── month (1 - 12)
# │ │ │ │ ┌───────────── day of the week (0 - 6) (Sunday to Saturday)
# │ │ │ │ │                                   OR sun, mon, tue, wed, thu, fri, sat
# │ │ │ │ │
# │ │ │ │ │
# * * * * *
```

* Observing result

Cronjob object executes task as a job as per defined schedule, every 5 minutes in this example

* Get list of jobs:

```console
curl -b ./token.txt -X GET $KRITEN_URL'/api/v1/jobs' \
--header 'Content-Type: application/json'
```

Returns:

```json
[
    {
        "id": "hello-kriten-cronjob-29192975",
        "owner": "root",
        "start_time": "Thu Jul  3 21:35:00 UTC 2025",
        "completion_time": "Thu Jul  3 21:35:07 UTC 2025",
        "failed": 0,
        "completed": 1,
        "stdout": "",
        "json_data": null
    },
    {
        "id": "hello-kriten-cronjob-29192970",
        "owner": "root",
        "start_time": "Thu Jul  3 21:30:00 UTC 2025",
        "completion_time": "Thu Jul  3 21:30:07 UTC 2025",
        "failed": 0,
        "completed": 1,
        "stdout": "",
        "json_data": null
    }
]
```

Jobs are executed every 5 minutes.

* Get job result

To get result of any above job:

```console
curl -b ./token.txt -X GET $KRITEN_URL'/api/v1/jobs/hello-kriten-cronjob-29192975' \
--header 'Content-Type: application/json'
```

Returns:

```json
{
    "id": "hello-kriten-cronjob-29192975",
    "owner": "root",
    "start_time": "Thu Jul  3 21:35:00 UTC 2025",
    "completion_time": "Thu Jul  3 21:35:07 UTC 2025",
    "failed": 0,
    "completed": 1,
    "stdout": "\n\n## init container logs\nCloning into '.'...\nFrom https://github.com/kriten-io/kriten-community-toolkit.git\n6533c3d7f4a731f91e4b4db076abdb44bec322b6\tHEAD\n6533c3d7f4a731f91e4b4db076abdb44bec322b6\trefs/heads/main\n\n\n##application container logs \nHello, Kriten!\n\nThis script demonstrates Kriten's capabilities.\nIt reads input variables (EXTRA_VARS) and secrets, and prints them.\n\n\n^JSON\n\n{\"extra_vars\": {\"agent_name\": \"Ethan Hunt\", \"operation\": \"Mission impossible\"}, \"secrets\": {}}\n^JSON\n\n\n\nScript completed.\n",
    "json_data": {
        "extra_vars": {
            "agent_name": "Ethan Hunt",
            "operation": "Mission impossible"
        },
        "secrets": {}
    }
}
```




