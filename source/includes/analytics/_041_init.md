## init

This message is sent from the GoCD parent window, after the plugin-provided HTML front-end file for the [chosen analytics](#get-analytics)
is loaded into the iframe.

This allows GoCD to provide the data needed by the plugin, without having to have the plugin-provided HTML front-end make an AJAX call to
the server. The plugin is expected to handle this message and render the analytics using the data passed in the message.

> An example message -

```json
{
    "head": {
        "reqId": 1,
        "type": "request",
        "key": "init"
    },
    "body": {
        "initialData": "{'pipelines:['a','b','c']'}"
    }
}
```
