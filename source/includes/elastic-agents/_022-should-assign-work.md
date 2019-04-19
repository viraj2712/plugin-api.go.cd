## Should Assign Work

When there are multiple agents available to run a job, the server will ask the plugin if jobs should be assigned to a particular agent. The request will contain information about the agent, the job configuration and the environment that the agent belongs to.
This allows plugin to decide if proposed agent is suitable to schedule a job on it. For example, plugin can check if flavor or region of VM is suitable.

<p class='request-name-heading'>Request name</p>

`cd.go.elastic-agent.should-assign-work`

<p class='request-body-heading'>Request body</p>

> Given the following config XML snippet —

```xml
<cruise>
  <server agentAutoRegisterKey="1e0e05fc-eb45-11e5-bc83-93882adfccf6"/>
  <elastic>
    <clusterProfiles>
      <clusterProfile id="docker-local" pluginId="cd.go.contrib.elastic-agent.docker">
        <property>
          <key>DockerURI</key>
          <value>https://docker-uri/</value>
        </property>
      </clusterProfile>
    </clusterProfiles>
    <agentProfiles>
      <agentProfile id="ec2.small-us-east" clusterProfileId="docker-local">
        <property>
          <key>ami-id</key>
          <value>ami-6ac7408f</value>
        </property>
        <property>
          <key>region</key>
          <value>us-east-1</value>
        </property>
      </agentProfile>
    </agentProfiles>
  </elastic>
  <pipelines>
    <pipeline name='build'>
      <job name="run-upgrade" runOnAllAgents="true" timeout='30' elasticProfileId="ec2.small-us-east">
        <tasks>
          <ant target="upgrade"/>
        </tasks>
      </job>
    </pipeline>
  </pipelines>
  <environments>
    <environment name="staging">
      <pipelines>
        <pipeline name="build"/>
      </pipelines>
    </environment>
  </environments>
  <agents>
    <agent elasticAgentId='i-283432d4' elasticPluginId='com.example.go.testplugin'/>
  </agents>
</cruise>
```

> The plugin will receive the following JSON body —

```json
{
  "agent": {
    "agent_id": "i-283432d4",
    "agent_state": "Idle",
    "build_state": "Idle",
    "config_state": "Enabled"
  },
  "environment": "staging",
  "job_identifier": {
    "job_id": 100,
    "job_name": "run-upgrade",
    "pipeline_counter": 1,
    "pipeline_label": "build",
    "pipeline_name": "build",
    "stage_counter": "1",
    "stage_name": "test-stage"
  },
  "elastic_agent_profile_properties": {
      "Image": "gocd/gocd-agent-alpine-3.5:v18.1.0",
      "MaxMemory": "https://docker-uri/"
  },
  "cluster_profile_properties": {
    "Image": "DockerURI",
    "MaxMemory": "500Mb"
  }
}
```

The request body will contain the following JSON elements:

<p class='attributes-table-follows'></p>

| Key                                | Type     | Description                                                                                                                                                                                                                                                                                          |
| -------------------                | -------- | -----------                                                                                                                                                                                                                                                                                          |
| `agent`                            | `Object` | An object describing the [elastic agent](#elastic-agent-object).                                                                                                                                                                                                                                     |
| `environment`                      | `String` | The `environment` that this job belongs to. Agents are expected to auto-register using this environment so that they can be assigned to the correct job. See the [environments section](https://docs.gocd.org/current/introduction/concepts_in_go.html#environment) to know more about environments. |
| `elastic_agent_profile_properties` | `Object` | Elastic agent profile associated with the job. It represents the elastic agent configuration for the job  in form of key value pairs.                                                                                                                                                                |
| `cluster_profile_properties`       | `Object` | The field represents the cluster profile associated with elastic profile.                                                                                                                                                                                                                            |
| `job_identifier`                   | `Object` | Job identifier of the job for which this call is being made.                                                                                                                                                                                                                                         |

<p class='response-code-heading'>Response code</p>

The plugin is expected to return status `200` if it can understand the request.

<p class='response-body-heading'>Response Body</p>

The server must return a JSON string response with a boolean — `true` or `false` to indicate whether the agent should be assigned work.
