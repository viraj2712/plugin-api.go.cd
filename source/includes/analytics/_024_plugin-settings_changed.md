## Plugin Settings Changed

This is a notification message to the plugin on update of plugin settings.

Everytime the plugin settings change, GoCD would send this message to plugin with the updated plugin settings.

<p class='request-name-heading'>Request name</p>

`go.plugin-settings.plugin-settings-changed`

<p class='request-body-heading'>Request body</p>

The request body will be a JSON which would be a map of the plugin settings. 

> An example request body

```json
{
  "server_url": "https://build.go.cd",
  "username": "view",
  "password": "password"
}
```

<p class='response-code-heading'>Response code</p>

The server is expected to return status `200` if it could process the request.

<p class='response-body-heading'>Response Body</p>

Can be left blank, the server does not parse any response body returned.
