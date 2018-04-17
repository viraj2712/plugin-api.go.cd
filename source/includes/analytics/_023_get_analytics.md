## Get Analytics

This message is a request to the plugin to fetch analytics for display.

Analytics is currently supported on the pipeline dashboard and the analytics dashboard. On a request to render analytics, GoCD sends a message to the plugin to fetch analytics. The plugin is expected to respond with a JSON which contains a path to an HTML which would render the analytics and the relevant data for rendering the analytics.

The `view_path` should refer to the HTML which should be part of the [static assets](#get-static-assets) returned by the plugin. GoCD, on receiving the response, will load the HTML specified in the `view_path` in an iframe and pass the relevant `data`. The HTML is responsible for building the visualization using the provided data. See the [Javascript Messages](#javascript-messages) section below for more information.


<p class='request-name-heading'>Request name</p>

`go.cd.analytics.get-analytics`

<p class='request-body-heading'>Request body</p>

> An example request body -

```json
{
    "type": "pipeline",
    "id": "analytics_for_pipeline",
    "params": {
      "pipeline_name": "my_pipeline"
    }
}
```

<p class='attributes-table-follows'></p>

| Key            | Type     | Description                                                                                |
|----------------|----------|--------------------------------------------------------------------------------------------|
| `type`         | `String` | The type of the analytics as defined in the [Plugin Capabilities](#get-plugin-capabilities)|
| `id`           | `String` | The id of the analytics as defined in the [Plugin Capabilities](#get-plugin-capabilities)  |
| `params`       | `Object` | This is a hash of optional params the plugin would require to generate analytics. For analytics of type `pipeline`, GoCD will send the pipeline name as a param `pipeline_name`. |


<p class='response-code-heading'>Response Body</p>

> An example response body —

```json
{
    "data": "{\"failed_count\":10, \"passed_count\": 34}",
    "view_path": "pipeline_analytics.html"
}
```

The response body should contain the following JSON elements:

<p class='attributes-table-follows'></p>

| Key         | Type     | Description                                                          |
|-------------|----------|----------------------------------------------------------------------|
| `data`      | `String` | The data as `json` string used to build the analytics.               |
| `view_path` | `String` | The path to the HTML file which will render the requested analytics. |


The plugin is expected to return status `200` if it can understand the request.
