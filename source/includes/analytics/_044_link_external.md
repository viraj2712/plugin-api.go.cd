## go.cd.analytics.v1.link-external

The iframe can send a message with the key `go.cd.analytics.v1.link-external` to the parent window to link to a page outside of GoCD. The parent window would open the page in a new tab.

> An example message from iframe to parent window to link to an external page -

```json
{
    "head": {
        "reqId": 1,
        "type": "request",
        "key": "go.cd.analytics.v1.link-external"
    },
    "body": {
        "url": "https://url.link.to.external.page"
    }
}
```
