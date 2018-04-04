## Check SCM Connection

> Example request body

```json
{
    "scm-configuration": {
        "SCM_URL": {
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
 
The plugin will receive request with following information.

<p class='request-name-heading'>Request name</p>

`check-scm-connection`

<p class='request-body-heading'>Request parameters</p>

The server will not provide any parameters.

<p class='request-body-heading'>Request headers</p>

The server will not provide any headers.

<p class='request-body-heading'>Request body</p>

This contains information about the SCM configuration provided by the user. The keys in the maps correspond to the keys provided by the plugin, as a part of the response to ["SCM Configuration"](#scm-configuration) message.

> Example response body

```json
{
    "status": "success",
    "messages": [
        "Successfully connected to SCM URL provided"
    ]
}
```

<p class='response-code-heading'>Response code</p>

The plugin is expected to return status `200` if it can understand the request.

<p class='response-body-heading'>Response Body</p>

The plugin is expected to send a response, which contains a status ("success" or "failure"), and a list of error messages. This represents whether a connection was successfully made, to the SCM specified in the request.