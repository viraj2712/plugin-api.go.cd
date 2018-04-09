## go.cd.analytics.v1.fetch-analytics

The iframe can send a message with key `go.cd.analytics.v1.fetch-analytics` to [fetch analytics](#get-analytics) from the plugin. The message body should specify the `pluginId`, `type` of metric, the id of the `metric` and additional params required by the plugin to fetch the analytics data. Upon recieving this message the parent window would make a GoCD API request to fetch the analytics from the plugin, upon recieving the response data the same would be passed to the iframe as a new message. 


> An example message from iframe to parent window to fetch analytics -

```json
{
    "head": {
        "reqId": 1,
        "type": "request",
        "key": "go.cd.analytics.v1.fetch-analytics"
    },
    "body": {
        "pluginId": "com.my.org.analytics",
        "type": "pipeline",
        "metric": "metric_id",
        "pipeline_name": "my_pipeline" 
    }
}
```

> The API request to GoCD to fetch the analytics

```
https://ci.example.com/go/analytics/com.my.org.analytics/pipeline/metric_id?pipeline_name=my_pipeline
```

> An example response message from parent window to iframe - 


```json
{
    "head": {
        "reqId": 1,
        "type": "response"
    },
    "body": {
        "data": "{'pipelines:['a','b','c']'}"
    }
}
```
