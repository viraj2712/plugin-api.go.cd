## Repository Configuration
 
 This message is sent by the server, when it wants to know what properties need to be stored in the configuration, for this plugin and this
 repository. It also uses this information to create a view, for the user to provide information about the repository.
 
The plugin will receive a request with following information.

<p class='request-name-heading'>Request name</p>

`repository-configuration`

<p class='request-body-heading'>Request parameters</p>

The server will not provide any parameters.

<p class='request-body-heading'>Request headers</p>

The server will not provide any headers.

<p class='request-body-heading'>Request body</p>

The server will not provide request body.

> Example response body

```json
{
  "REPO_URL": {
    "display-name": "Repository URL",
    "display-order": "0"
  },
  "USERNAME": {
    "part-of-identity": false,
    "required": false,
    "display-name": "User",
    "display-order": "1"
  },
  "PASSWORD": {
    "secure": true,
    "part-of-identity": false,
    "required": false,
    "display-name": "Password",
    "display-order": "2"
  }
}
```

<p class='response-code-heading'>Response code</p>

The plugin is expected to return status `200` if it can understand the request.

<p class='response-body-heading'>Response Body</p>

The plugin is expected to return an object containing the configuration property along with [repository configuration object](#the-repository-configuration-response-object)
