# Javascript Messages

GoCD renders plugin analytics in a <a href='https://developer.mozilla.org/en-US/docs/Web/HTML/Element/iframe' target='_blank'>sandboxed</a> iframe. It is allowed only to run scripts. All other sandbox restrictions apply to the iframe - for instance, it has no access to the GoCD session cookie and cannot make authenticated requests to the GoCD API.

As the iframe runs in a sandbox, cross-origin communication between the parent window and iframe is through the <a href='https://developer.mozilla.org/en-US/docs/Web/API/Window/postMessage' target='_blank'>window.postMessage()</a> method. GoCD allows two way communication between the parent window and the iframe.

GoCD provides a Javascript module named plugin-endpoint.js which exposes an API to handle the cross-origin communication. Please see examples in the [Analytics Skeleton Plugin](https://github.com/gocd-contrib/analytics-skeleton-plugin) to use the plugin-endpoint.js API's.

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

| Key    | Type     | Description                                                                                          |
|--------|----------|------------------------------------------------------------------------------------------------------|
| `head` | `Object` | This represents the metadata of the message.                                                         |
| `body` | `Object` | The body represents the actual payload of the message which differs between different message types. |


The metadata should have the following structure.

<p class='attributes-table-follows'></p>

| Key     | Type      | Description                                                                         |
|---------|-----------|-------------------------------------------------------------------------------------|
| `reqId` | `Integer` | Unique request id. This will be used in the response as well.                       |
| `type`  | `String`  | The type of message, can be one of `request` or `response`.                         |
| `key`   | `String`  | The message key which identifies the type of message. See below for supported keys. |

GoCD currently supports the following messages with the `keys`,

* [init](#init)
* [go.cd.analytics.v1.fetch-analytics](#go-cd-analytics-v1-fetch-analytics)
* [go.cd.analytics.v1.link-to](#go-cd-analytics-v1-link-to)
* [go.cd.analytics.v1.link-external](#go-cd-analytics-v1-link-external)
