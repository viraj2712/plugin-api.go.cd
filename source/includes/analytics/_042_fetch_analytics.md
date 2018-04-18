### Request key: `fetch-analytics`

> An example message from iframe to parent window to fetch analytics:

```html
<html>
<head>
  <script src="analytics-endpoint.js"></script>
  <script>
  AnalyticsEndpoint.onInit(function(initialData, transport) {
    ...
    transport.request("fetch-analytics", {
      type: "pipeline",
      metric: "pipeline_duration",

      user_defined_param1: "my_pipeline",
      user_defined_param2: "something_else"
    })
      .done(function(data) {
        var dataObject = JSON.parse(data);
        console.log("Done! Got: " + dataObject);
      })
      .fail(function(errors) {
        console.log("Something failed: " + errors);
      });
  });

  AnalyticsEndpoint.ensure("v1");
  </script>
</head>
<body>
  ...
</body>
</html>
```

> The API request to GoCD to fetch the analytics (for above example):

```
https://ci.example.com/go/analytics/plugin_id/pipeline/pipeline_duration?user_defined_param1=my_pipeline&user_defined_param2=something_else
```

The plugin front-end in the iframe can send a message with key `fetch-analytics` to [get analytics](#get-analytics)
from its plugin back-end in the GoCD server. This message can be used to implement drill-downs and other navigation between charts.

Upon receiving this message, the parent window will make a GoCD API request to the plugin's [get analytics](#get-analytics) API to fetch the
specified analytics from the plugin. Upon receiving the response data, it will be passed to the plugin front-end in the iframe as a response
to the `fetch-analytics` call.

<aside class='notice'>
  <strong>Note:</strong> The response will only contain the <code>data</code> part, and will not contain the <code>view_path</code> parameter, if sent by the plugin as a response to <a href="#get-analytics">the get-analytics</a> call.
</aside>

The parameter object should contain these keys:

| Key                   | Description                                                                                                                   |
|-----------------------|-------------------------------------------------------------------------------------------------------------------------------|
| `type`                | Type of the metric. Usually `pipeline` or `dashboard`. Depends on the [capabilities](#get-plugin-capabilities) of the plugin. |
| `metric`              | The ID of the metric as defined by the plugin in its [capabilities](#get-plugin-capabilities).                        |
| `user_defined_param1` | Any plugin-author-defined parameters (optional).                                                                              |
| `user_defined_param2` | Any plugin-author-defined parameters (optional).                                                                              |
