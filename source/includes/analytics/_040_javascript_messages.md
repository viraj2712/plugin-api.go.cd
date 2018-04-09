# Javascript Messages

GoCD renders plugin analytics in an iframe. The iframe runs in a <a href='https://developer.mozilla.org/en-US/docs/Web/HTML/Element/iframe' target='_blank'>sandbox</a> and is allowed only to run scripts, all other sandbox restrictions apply to the iframe.

As the iframe runs in a sandbox, cross-origin communication between the parent window and iframe is through the <a href='https://developer.mozilla.org/en-US/docs/Web/API/Window/postMessage' target='_blank'>window.postMessage()</a> method. GoCD allows two way communication between the parent window and the iframe.

> An example message -

```json
{
    "head": {
        "reqId": "",
        "type": "request",
        "key": "init"
    },
    "body": {
        "initialData": "{'pipelines:['a','b','c']'}"
    }
}
```

All messages used in communication between the parent window and iframe should be a JSON with below message body, 

<p class='attributes-table-follows'></p>

| Key            | Type     | Description                                                                                              |
|----------------|----------|----------------------------------------------------------------------------------------------------------|
| `head`         | `Object` | The type represents the metadata of the message.                                                          | 
| `body`         | `Object` | The body represents the actual payload of the message which would differ between different message type. |  


The metadata should have the following structure.

<p class='attributes-table-follows'></p>

| Key            | Type      | Description                                                  |
|----------------|-----------|--------------------------------------------------------------|
| `reqId`        | `Integer` | Unique request Id.                                           | 
| `type`         | `String`  | The type of message, can be one of `request` or `response`.  |  
| `key`          | `String`  | The message key which identifies the type of message.        |

GoCD currently supports the following messages with the `keys`,

* [init](#init)
* [go.cd.analytics.v1.fetch-analytics](#go-cd-analytics-v1-fetch-analytics)
* [go.cd.analytics.v1.link-to](#go-cd-analytics-v1-link-to)
* [go.cd.analytics.v1.link-external](#go-cd-analytics-v1-link-external)

