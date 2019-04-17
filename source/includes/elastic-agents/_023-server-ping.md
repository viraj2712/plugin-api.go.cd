## Server Ping

Each elastic agent plugin will receive a periodic signal at regular intervals for it to perform any cleanup operations. Plugins may use this message to disable and/or terminate agents at their discretion.

<aside class="warning">
  <strong>Important:</strong> Since this call may potentially make network requests to terminate agents, the server will, in order to improve performance, use multiple threads to deliver the this message. It is important that plugin implementors ensure that their code is thread-safe.
</aside>

<p class='request-name-heading'>Request name</p>

`cd.go.elastic-agent.server-ping`

<p class='request-body-heading'>Request body</p>

> Given the following config XML snippet —

```xml
<elastic>
  <clusterProfiles>
    <clusterProfile id="docker-local" pluginId="cd.go.contrib.elastic-agent.docker">
      <property>
        <key>DockerURI</key>
        <value>https://docker-uri/</value>
      </property>
    </clusterProfile>
    <clusterProfile id="ecs" pluginId="cd.go.contrib.elastic-agent.ecs">
      <property>
        <key>AWS_ACCESS_KEY</key>
        <value>AMSDKFSDOFSFSI</value>
      </property>
      <property>
        <key>AWS_SECRET_KEY</key>
        <value>yshfksdfasd,fmsldgjdflgjgdflgjdlfgjdfl</value>
      </property>
      <property>
        <key>CLUSTER_NAME</key>
        <value>Dev</value>
      </property>
    </clusterProfile>
  </clusterProfiles>
</elastic>
```

> The plugin will receive the following JSON body —

```json
{
  "all_cluster_profile_properties": [
    {
      "DockerURI": "https://docker-uri/"
    },
    {
      "AWS_ACCESS_KEY": "AMSDKFSDOFSFSI",
      "AWS_SECRET_KEY": "yshfksdfasd,fmsldgjdflgjgdflgjdlfgjdfl",
      "CLUSTER_NAME"  : "Dev"
    }
  ]
}
```

| Key                              | Type     | Description                                                       |
| -------------------------------- | -------- | -----------                                                       |
| `all_cluster_profile_properties` | `Array`  | The field represents the list of cluster profiles for the plugin. |

<p class='response-code-heading'>Response code</p>

The plugin is expected to return status `200` if it can understand the request.

<p class='response-body-heading'>Response Body</p>

Can be left blank, the server does not parse any response body returned.
