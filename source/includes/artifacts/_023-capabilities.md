## Get Plugin Capabilities

This message is a request to the plugin to provide plugin capabilities. Currently the plugin does not support any capabilities, so plugins should return an empty JSON as a response. In the future, based on these capabilities GoCD would enable or disable the plugin features for a user.

<p class='request-name-heading'>Request name</p>

`cd.go.artifact.get-capabilities`

<p class='request-body-heading'>Request body</p>

Server sends request an `Empty` request body.

<p class='response-code-heading'>Response Body</p>

The plugin is expected to return status `200` if it can understand the request, with an empty response body
