## Publish Artifact

This message is a request to the plugin to publish an artifact to the specified artifact store.


<p class='request-name-heading'>Request name</p>

`cd.go.artifact.publish-artifact`

<p class='request-body-heading'>Request body</p>

> Given the following config XML snippet —

```xml

<artifactStores>
      <artifactStore id="dockerhub" pluginId="cd.go.artifact.docker.registry">
        <property>
          <key>RegistryURL</key>
          <value>https://index.docker.io/v1/</value>
        </property>
        <property>
          <key>Username</key>
          <value>boohoo</value>
        </property>
        <property>
          <key>Password</key>
          <value>password</value>
        </property>
      </artifactStore>
    </artifactStores>
<pipelines group="first">
  <pipeline name="build">
    ...
    <job name="build-job">
      ...
      <artifacts>
        <artifact id="app-image" storeId="dockerhub">
          <configuration>
            <property>
              <key>Image</key>
              <value>gocd/gocd-demo</value>
            </property>
            <property>
              <key>Tag</key>
              <value>v${GO_PIPELINE_COUNTER}</value>
            </property>
          </configuration>
        </artifact>
      </artifacts>
    </job>
    ...
  </pipeline>
</pipelines>
```

> The plugin will receive the following JSON body —

```json
{
  "environment_variables":{
    "GO_PIPELINE_NAME":"build",
    "GO_TRIGGER_USER":"admin",
    "FOO": "bar"
  },
  "artifact_plan":{
    "configuration":{
      "BuildFile":"",
      "Image":"gocd/gocd-demo",
      "Tag":"v${GO_PIPELINE_COUNTER}"
    },
    "id":"app-image",
    "storeId":"dockerhub"
  },
  "artifact_store":{
    "configuration":{
      "RegistryURL":"https://index.docker.io/v1/",
      "Username":"boohoo",
      "Password":"password"
    },
    "id":"dockerhub"
  },
  "agent_working_directory":"/Users/varshavs/gocd/agent/pipelines/build"}
```

The request body will contain the following JSON elements:

<p class='attributes-table-follows'></p>

| Key                      | Type     | Description                                                                                                                                               |
| ------------------------ | -------- | --------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `environment_variables`  | `Object` | A map of the environment variable that were available at the time the job was triggered.                                                                  |
| `artifact_plan`          | `Object` | This mainly contains the configuration properties that inform the plugin about the specific artifact that needs to be pushed.                             |
| `artifact_store`         | `Object` | This section contains the details about the artifact store to which the plugin has to publish the artifact.                                               |
| `agent_working_directory`| `String` | Since the artifact publishing happens on the go-agent side, the working directory is also passed along in the request in case the plugin wants to use it. |

<p class='response-code-heading'>Response code</p>

The plugin is expected to return status `200` if it can understand the request.

<p class='response-body-heading'>Response Body</p>

The plugin is expected to return a json as shown. This json is written into a file called `<plugin-id>.json` on the agent and uploaded as a `Build Artifact` to the GoCD server to a directory called `pluggable-artifact-metadata`. This directory is never removed as part of cleaning GoCD artifacts.

> Plugin response body

```json
{
  "metadata":{
    "image":"gocd/gocd-demo:v23",
    "digest":"sha256:f7840887b6f09f531935329a4ad1f6176866675873a8b3eed6a5894573da8247"
    }
}
```

> The content of plugin-id.json file

```json
{
  "app-image":{
  "image":"gocd/gocd-demo:v23",
  "digest":"sha256:f7840887b6f09f531935329a4ad1f6176866675873a8b3eed6a5894573da8247"
  }
}
```

> *Note: `app-image` is the artifact id specified in the job configuration*
