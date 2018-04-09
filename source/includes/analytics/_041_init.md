## init

On [fetching analytics](#get-analytics) from the plugin the parent window loads an iframe and posts a message with the key `init` and passes the data returned by the plugin. The plugin is expected to handle this message and render the analytics using the data passed in the message. 

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
