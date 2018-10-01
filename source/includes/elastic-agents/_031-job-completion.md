## Job Completion

This message is a request to the plugin to terminate the agent of the job that has been completed.

<aside class="notice">
  <strong>Important:</strong> A plugin may, at its discretion, choose to not actually terminate an agent. This could be because the same agent can be used for another job configuration.
</aside>

<aside class="warning">
  <strong>Important:</strong> Since this call may potentially make network requests to terminate the agent, the server will, in order to improve performance, use multiple threads to deliver the this message. It is important that plugin implementors ensure that their code is thread-safe.
</aside>

<p class='request-name-heading'>Request name</p>

`cd.go.elastic-agent.job-completion`

<p class='request-body-heading'>Request body</p>

> Given the following config XML snippet —

```xml
<server agentAutoRegisterKey="1e0e05fc-eb45-11e5-bc83-93882adfccf6" />
<pipelines group="first">
  <pipeline name="up42">
        <stage name="up42_stage">
          <jobs>
            <job name="up42_job" elasticProfileId="profile1" />
          </jobs>
        </stage>
      </pipeline>
</pipelines>
<agents>
  <agent hostname="1697e6b164f7" ipaddress="172.17.0.6" uuid="a45e3ca1-4419-4bd5-b18b-882f75ffd4c2" elasticAgentId="GoCD18efbeef995e40f688cd92dc22a4d332" elasticPluginId="cd.exmaple.elastic-agent" />
</agents>

```

> The plugin will receive the following JSON body —

```json
{
  "elastic_agent_id": "GoCD18efbeef995e40f688cd92dc22a4d332",
  "job_identifier": {
    "job_id": 100,
    "job_name": "up42_job",
    "pipeline_counter": 1,
    "pipeline_label": "up42",
    "pipeline_name": "up42",
    "stage_counter": "1",
    "stage_name": "up42_stage"
  }
}
```

The request body will contain the following JSON elements:

<p class='attributes-table-follows'></p>

| Key                 | Type     | Description |
| ------------------- | -------- | ----------- |
| `elastic_agent_id`  | `String` | The Elastic agent ID of the agent on which the job has completed. |
| `job_identifier`    | `Object` | Job identifier of the job for which this call is being made. |

<p class='response-code-heading'>Response code</p>

The plugin is expected to return status `200` if it can understand the request.

<p class='response-body-heading'>Response Body</p>

Can be left blank, the server does not parse any response body returned.
