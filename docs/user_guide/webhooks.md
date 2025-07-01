# Webhooks

For seamless integrations and to facilitate event driven automation, Webhook receiver capability was added into Kriten as of version 0.5. This version supports webhook integration with Infrahub (https://opsmill.com), Netbox (https://netboxlabs.com).

Kriten defines one-to-one mapping between a webhook and a kriten task. On successful webhook event, Kriten executes associated task and passes json body as json string via EXTRA_VARS environmental variable.

Webhooks are user defined and mapped to a user, inheriting user RBAC permissions. Webhooks are secured via shared secret, defined per webhook - that secret is used to calculate signature for body of request on sending end and to validate signature on receiving end. Note: Kriten requires shared secret to be provided, it supports only signed content for authentication purpose.


Current supported webhook impementations:

|System| HTTP Headers | Signature calculation
|---------|-----------|----------------------|
|`Infrahub`| "webhook-timestamp" - message timestamp, "webhook-id" - unique message id, "webhook-signature" - calculated signature| HMAC256 base64 digest calculated on string concatenation of header fields "webhook-timestamp", "webhook-id" and json body|
|`Netbox`|"X-Hook-Signature" - calculated signature| HMAC512 hex digest calculated on json body|

Note: Any system can add support for Kriten webhook by adhering to one of those implemented options.

## Configure Kriten webhook receiver

To demonstrate capability of webhook feature, we will be leveraging "hello-kriten" example from https://github.com/kriten-io/kriten-community-toolkit repo. This simple python app prints supplied input parameters exposed to it as EXTRA_VARS environmental variable. On webhook event, that variable will be populated with json body from sender. Task "hello-kriten" has been already configured, see hello-kriten documentation in examples/hello-kriten in above repo.

Where $KRITEN_URL is set to the URL of your Kriten instance.

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

* Create webhook for "hello-kriten" task

```console
curl -b ./token.txt -X POST $KRITEN_URL'/api/v1/webhooks' \
--header 'Content-Type: application/json' \
--data '{
  "description": "Webhook for Hello Kriten task",
  "task": "hello-kriten",
  "secret": "supersecret"
}'
```

Returns:
```json
{"id":"ad7a3ce6-751e-4d8e-9921-503948f76516",
 "owner":"3b5890d3-ea33-4cfb-8752-0152916ff0b2",
 "secret":"supersecret",
 "description":"Webhook for Hello Kriten task",
 "task":"hello-kriten",
 "created_at":"2025-06-30T18:29:51.798623565Z",
 "updated_at":"2025-06-30T18:29:51.798623565Z"}
```

To execute this webhook, sender need to post to URL "$KRITEN_URL/api/v1/webhooks/run/$ID", where $ID is "id" of above created webhook, and signature calculated with "secret".

## Configure Infrahub webhook

* Create webhook in Infrahub

In Integrations -> Webhooks create Standard Webhook:

![Infrahub Webhook](../assets/infrahub_webhook.png)

Where changes to Network device in main branch would trigger webhook event. 

There is a device, fra01-pod1-leaf1:

![Infrahub Device Info](../assets/infrahub_device.png)

To create event we will modify description to "Arista switch", as result webhook event will be triggered and event data posted to Kriten webhook receiver, which will execute job against task "hello-kriten".

* Get list of jobs

```console
curl -b ./token.txt -X GET $KRITEN_URL'/api/v1/jobs' \
--header 'Content-Type: application/json'
```

From the list of jobs we identify ID and status of the latest completed job.

```json
[
    {
        "id": "hello-kriten-k62hb",
        "owner": "root",
        "start_time": "Mon Jun 30 21:11:56 UTC 2025",
        "completion_time": "Mon Jun 30 21:12:02 UTC 2025",
        "failed": 0,
        "completed": 1,
        "stdout": "",
        "json_data": null
    }
]
```

* Get job result

```console
curl -b ./token.txt -X GET $KRITEN_URL'/api/v1/jobs/hello-kriten-k62hb' \
--header 'Content-Type: application/json'
```

Returns:

```json

{
    "id": "hello-kriten-k62hb",
    "owner": "root",
    "start_time": "Mon Jun 30 21:11:56 UTC 2025",
    "completion_time": "Mon Jun 30 21:12:02 UTC 2025",
    "failed": 0,
    "completed": 1,
    "json_data": {
        "extra_vars": {
            "account_id": "183badb4-c736-e838-3b1d-c5153c211819",
            "branch": "main",
            "data": {
                "action": "updated",
                "changelog": {
                    "attributes": {
                        "description": {
                            "kind": "Text",
                            "name": "description",
                            "properties": {},
                            "value": "Arista switch",
                            "value_previous": "FRA POD1 LEAF1",
                            "value_update_status": "updated"
                        }
                    },
                    "display_label": "fra05-pod1-leaf1",
                    "node_id": "183bae51-8895-0067-3b10-c5181069938d",
                    "node_kind": "InfraDevice",
                    "relationships": {}
                },
                "fields": [
                    "description"
                ],
                "kind": "InfraDevice",
                "node_id": "183bae51-8895-0067-3b10-c5181069938d"
            },
            "event": "infrahub.node.updated",
            "id": "bad56575-c8e4-4e42-a7eb-f58ca9eda042",
            "occured_at": "2025-06-30 21:11:54.176727+00:00"
        },
        "secrets": {}
    }
}
```

Field "extra_vars" contains unchanged body passed by Infrahub on the event.


## Configure Netbox Webhook

For demonstration purpose, for Netbox we will use the same webhook we created for Infrahub, as we are not doing anything with data passed via webhook, but only priting it out from python script.

* Create webhook in Netbox

In Integrations -> Webhooks create a webhook. Define HTTP method POST, provide Kriten webhook URL and secret.

![Netbox Webhook](../assets/netbox_webhook.png)

* Create Event rule

Event Rule defines event, i.e. devide added, removed, updated, and so on and maps it to configured webhook.

In Integrations -> Event Rules, create a rule, as example, to trigger event on device update.

![Netbox Event Rules](../assets/netbox_event_rule.png)

There is device in the Netbox:

![Netbox Event Rules](../assets/netbox_device_status.png)

To trigger the event we will modify status of the device from Active to Decommissioning.

* Get list of jobs

```console
curl -b ./token.txt -X GET $KRITEN_URL'/api/v1/jobs' \
--header 'Content-Type: application/json'
```

From the list of jobs we identify ID and status of the latest completed job.

```json
[
    {
        "id": "hello-kriten-4vgn8",
        "owner": "root",
        "start_time": "Mon Jun 30 21:57:20 UTC 2025",
        "completion_time": "Mon Jun 30 21:57:27 UTC 2025",
        "failed": 0,
        "completed": 1,
        "stdout": "",
        "json_data": null
    }
]
```

* Get job result

```json
{
    "id": "hello-kriten-4vgn8",
    "owner": "root",
    "start_time": "Mon Jun 30 21:57:20 UTC 2025",
    "completion_time": "Mon Jun 30 21:57:27 UTC 2025",
    "failed": 0,
    "completed": 1,
    "json_data": {
        "extra_vars": {
            "data": {
                "airflow": null,
                "asset_tag": null,
                "cluster": null,
                "comments": "",
                "config_template": null,
                "console_port_count": 0,
                "console_server_port_count": 0,
                "created": "2025-05-09T12:50:15.843720Z",
                "custom_fields": {},
                "description": "",
                "device_bay_count": 0,
                "device_type": {
                    "description": "",
                    "display": "cEOS",
                    "id": 1,
                    "manufacturer": {
                        "description": "",
                        "display": "Arista",
                        "id": 1,
                        "name": "Arista",
                        "slug": "arista",
                        "url": "/api/dcim/manufacturers/1/"
                    },
                    "model": "cEOS",
                    "slug": "ceos",
                    "url": "/api/dcim/device-types/1/"
                },
                "display": "arista-leaf-01",
                "display_url": "/dcim/devices/1/",
                "face": null,
                "front_port_count": 0,
                "id": 1,
                "interface_count": 0,
                "inventory_item_count": 0,
                "last_updated": "2025-06-30T21:57:20.216402Z",
                "latitude": null,
                "local_context_data": null,
                "location": null,
                "longitude": null,
                "module_bay_count": 0,
                "name": "arista-leaf-01",
                "oob_ip": null,
                "parent_device": null,
                "platform": null,
                "position": null,
                "power_outlet_count": 0,
                "power_port_count": 0,
                "primary_ip": null,
                "primary_ip4": null,
                "primary_ip6": null,
                "rack": null,
                "rear_port_count": 0,
                "role": {
                    "_depth": 0,
                    "description": "",
                    "display": "leaf",
                    "id": 1,
                    "name": "leaf",
                    "slug": "leaf",
                    "url": "/api/dcim/device-roles/1/"
                },
                "serial": "",
                "site": {
                    "description": "",
                    "display": "Lab",
                    "id": 1,
                    "name": "Lab",
                    "slug": "lab",
                    "url": "/api/dcim/sites/1/"
                },
                "status": {
                    "label": "Decommissioning",
                    "value": "decommissioning"
                },
                "tags": [],
                "tenant": null,
                "url": "/api/dcim/devices/1/",
                "vc_position": null,
                "vc_priority": null,
                "virtual_chassis": null
            },
            "event": "updated",
            "model": "device",
            "request_id": "05c732a7-58f6-43ec-bbd9-26ce3e83da91",
            "snapshots": {
                "postchange": {
                    "airflow": null,
                    "asset_tag": null,
                    "cluster": null,
                    "comments": "",
                    "config_template": null,
                    "console_port_count": 0,
                    "console_server_port_count": 0,
                    "created": "2025-05-09T12:50:15.843Z",
                    "custom_fields": {},
                    "description": "",
                    "device_bay_count": 0,
                    "device_type": 1,
                    "face": null,
                    "front_port_count": 0,
                    "interface_count": 0,
                    "inventory_item_count": 0,
                    "last_updated": "2025-06-30T21:57:20.216Z",
                    "latitude": null,
                    "local_context_data": null,
                    "location": null,
                    "longitude": null,
                    "module_bay_count": 0,
                    "name": "arista-leaf-01",
                    "oob_ip": null,
                    "platform": null,
                    "position": null,
                    "power_outlet_count": 0,
                    "power_port_count": 0,
                    "primary_ip4": null,
                    "primary_ip6": null,
                    "rack": null,
                    "rear_port_count": 0,
                    "role": 1,
                    "serial": "",
                    "site": 1,
                    "status": "decommissioning",
                    "tags": [],
                    "tenant": null,
                    "vc_position": null,
                    "vc_priority": null,
                    "virtual_chassis": null
                },
                "prechange": {
                    "airflow": null,
                    "asset_tag": null,
                    "cluster": null,
                    "comments": "",
                    "config_template": null,
                    "console_port_count": 0,
                    "console_server_port_count": 0,
                    "created": "2025-05-09T12:50:15.843Z",
                    "custom_fields": {},
                    "description": "",
                    "device_bay_count": 0,
                    "device_type": 1,
                    "face": null,
                    "front_port_count": 0,
                    "interface_count": 0,
                    "inventory_item_count": 0,
                    "latitude": null,
                    "local_context_data": null,
                    "location": null,
                    "longitude": null,
                    "module_bay_count": 0,
                    "name": "arista-leaf-01",
                    "oob_ip": null,
                    "platform": null,
                    "position": null,
                    "power_outlet_count": 0,
                    "power_port_count": 0,
                    "primary_ip4": null,
                    "primary_ip6": null,
                    "rack": null,
                    "rear_port_count": 0,
                    "role": 1,
                    "serial": "",
                    "site": 1,
                    "status": "active",
                    "tags": [],
                    "tenant": null,
                    "vc_position": null,
                    "vc_priority": null,
                    "virtual_chassis": null
                }
            },
            "timestamp": "2025-06-30T21:57:20.313712+00:00",
            "username": "kubecode"
        },
        "secrets": {}
    }
}
```

Where extra_vars field contains unchanged body of event from Netbox.