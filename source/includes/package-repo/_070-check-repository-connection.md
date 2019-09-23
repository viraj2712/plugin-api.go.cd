## Check Repository Connection

The plugin will receive request with following information.

> Example request body

```json
{
  "repository-configuration": {
    "REPO_URL": {
      "value": "http://localhost.com"
    },
    "USERNAME": {
      "value": "user"
    },
    "PASSWORD": {
      "value": "password"
    }
  }
}
```
 
<p class='request-name-heading'>Request name</p>

`check-repository-connection`

<p class='request-body-heading'>Request parameters</p>

The server will not provide any parameters.

<p class='request-body-heading'>Request headers</p>

The server will not provide any headers.

<p class='request-body-heading'>Request body</p>

This contains information about the [repository-level configuration](#the-repository-configuration-response-object) provided by the user. The keys in the maps correspond to the keys provided by the plugin, as a part of the response to ["Repository Configuration"](#repository-configuration) message.

> Example response body

```json
{
  "status": "success",
  "messages": [
    "Successfully connected to repository url provided"
  ]
}
```

<p class='response-code-heading'>Response code</p>

The plugin is expected to return status `200` if it can understand the request.

<p class='response-body-heading'>Response Body</p>

The plugin is expected to send a response, which contains a status ("success" or "failure"), and a list of error messages. This represents whether a connection was successfully made, to the repository specified in the request.
