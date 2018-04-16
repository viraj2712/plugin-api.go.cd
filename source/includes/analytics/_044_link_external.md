## go.cd.analytics.v1.link-external

Any links opened directly from the plugin's front-end will open inside the iframe. For security reasons, the iframe cannot affect the
navigation of the parent GoCD window directly. So, the iframe can send a message with the key `go.cd.analytics.v1.link-external` to the
parent window to link to a page outside of GoCD. The parent window will open the page in a new tab.

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

The head object should contain:

| Key     | Description                                    |
|---------|------------------------------------------------|
| `reqId` | A unique request ID.                           |
| `type`  | Should be: `request`.                          |
| `key`   | Should be: `go.cd.analytics.v1.link-external`. |

The body object should contain:

| Key   | Description                          |
|-------|--------------------------------------|
| `url` | The URL that should be navigated to. |
