## Validate SCM Configuration

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

`validate-scm-configuration`

<p class='request-body-heading'>Request parameters</p>

The server will not provide any parameters.

<p class='request-body-heading'>Request headers</p>

The server will not provide any headers.

<p class='request-body-heading'>Request body</p>

This contains information about the SCM configuration provided by the user. The keys in the maps correspond to the keys provided by the plugin, as a part of the response to ["SCM Configuration"](#scm-configuration) message.

> Example response body

```json
[
    {
        "key": "SCM_URL",
        "message": "SCM URL not specified"
    },
    {
        "key": "RANDOM",
        "message": "Unsupported key(s) found : RANDOM. Allowed key(s) are : SCM_URL, USERNAME, PASSWORD"
    }
]
```

<p class='response-code-heading'>Response code</p>

The plugin is expected to return status `200` if it can understand the request.

<p class='response-body-heading'>Response Body</p>

The plugin is expected to send a response, which contains a list of errors in the SCM configuration, one message for every key in the request. It can also send an empty list, ie [], if the configuration is valid.
