## Agent Status Changed

This message is sent by the server, when it wants to notify the plugin about any change in agent state.

Agent status changed notifications only get sent when the the state of the agent has changed.

<aside class="info">
  <strong>Note</strong>: As part of notification plugin endpoint V3, all timestamp's are in `UTC` with the DateTime format <strong>"yyyy-MM-dd'T'HH:mm:ss.SSSZ"</strong>
</aside>

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

The agent status notifications is sent out when the state of an agent changes. The change of state can be either to `agent_config_state`, `build_state` or the `agent_state`. The request body will contain a JSON representing the agent.

* `agent_config_state` - can be either `Pending`, `Enabled`, `Disabled`
* `agent_state` - can be either `Idle`, `Building`, `LostContact`, `Missing`, `Cancelled`, `Unknown`
* `build_state` - can be either `Idle`, `Building`, `Cancelled`, `Unknown`
