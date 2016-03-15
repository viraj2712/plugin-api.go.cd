## Get Settings View

This is an optional message that the plugin may implement, should users want to configure the plugin from the GoCD admin page.

<p class='request-name-heading'>Request name</p>

`go.plugin-settings.get-view`

<p class='request-body-heading'>Request body</p>

The server will not provide a request body.

<p class='response-code-heading'>Response code</p>

The plugin is expected to return status `200` if it could understand the request.

<p class='response-body-heading'>Response Body</p>

A JSON [settings view object](#the-get-settings-view-object)
