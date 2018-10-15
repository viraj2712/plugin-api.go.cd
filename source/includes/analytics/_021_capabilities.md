## Get Plugin Capabilities

This message is a request to the plugin to provide plugin capabilities. The capabilities should be a list of analytics supported by the plugin. Based on the type of supported analytics, GoCD decides the page on which to render the analytics, e.g analytics of type `pipeline` will show up on the GoCD pipeline dashboard.

<p class='request-name-heading'>Request name</p>

`go.cd.analytics.get-capabilities`

<p class='request-body-heading'>Request body</p>

Server sends request with `Empty` request body.

<p class='response-code-heading'>Response Body</p>

> An example response body:

```json
{
    "supported_analytics": [
        {
            "id": "pipeline_duration",
            "title": "Pipeline Duration",
            "type": "pipeline"
        },
        {
            "id": "pipelines_with_longest_average_wait_time",
            "title": "Pipelines With The Longest Average Wait Times",
            "type": "dashboard"
        }
    ]
}
```

The response body should contain the <code>supported_analytics</code> field which is a collection of analytics metrics. Each analytics metric has following JSON elements:

<p class='attributes-table-follows'></p>

| Key     | Type     | Description                                                                                                 |
|---------|----------|-------------------------------------------------------------------------------------------------------------|
| `id`    | `String` | Unique identifier for an analytics. The id will be used by GoCD to fetch a specific metric from the plugin. |
| `title` | `String` | The title for analytics.                                                                                    |
| `type`  | `String` | The type of the analytics which defines the position of analytics in GoCD.                                  |

Valid types of analytics metric are as follows:

<p class='attributes-table-follows'></p>

| Type        | Scope                                                                                          |
|-------------|------------------------------------------------------------------------------------------------|
| `dashboard` | Dashboard level analytics will be displayed at the global level in the GoCD application.       |
| `pipeline`  | Pipeline level analytics will be displayed on each pipeline in the GoCD application.           |
| `agent`     | Agent level analytics can be viewed on the agents page in the GoCD application for each agent. |
| `vsm`       | VSM analytics can be viewed on the Value Stream Map(VSM) page in the GoCD application.         |

<aside class="info">
  <strong>Note</strong>: Any other analytics type apart from above mentioned types will be ignored.
</aside>


The plugin is expected to return status `200` if it can understand the request.
