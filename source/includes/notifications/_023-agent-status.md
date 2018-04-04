## Agent Status Changed

This message is sent by the server, when it wants to notify the plugin about a "agent status change".

Agent status changed notifications only get sent when the the state of the agent has changed.

### Request-Response basics

<p class='request-name-heading'>Request name</p>

`agent-status`

<p class='response-code-heading'>Response code</p>

The plugin is expected to return status `200` if it can understand the request.

<p class='response-body-heading'>Response Body</p>

> An example response body if the plugin could send the notification successfully

```json
{
  "status": "success"
}
```

> An example response body if the plugin could not send the notification

```json
{
  "status": "failure",
  "messages": ["Could not send email for agent agent_hostname"]
}
```

The plugin is expected to return a JSON object to indicate if the notifications could be processed.

<aside class="warning">
  <strong>Note</strong>: If plugin responds with error messages Go Server shows those in "server health messages".
</aside>

### Agent state change notifications

> A sample body when the agent state changes building.

```json
{
    "agent_config_state": "enabled",
    "agent_state": "building",
    "build_state": "building",
    "is_elastic": true,
    "free_space": "100",
    "host_name": "agent_hostname",
    "ip_address": "127.0.0.1",
    "operating_system": "rh",
    "transition_time": "2018-02-15T06:31:28.998+0000",
    "uuid": "agent_uuid"
}
```

These notifications get sent out when the state of an agent changes. The request body will contain a JSON representing the agent.

* The new state of the agent can be identified by the `.agent_state` attribute set to `building`.

<aside class="note">
In the bullets above, all JSON paths use the jq syntax documented here: https://stedolan.github.io/jq/manual/v1.5/
</aside>
