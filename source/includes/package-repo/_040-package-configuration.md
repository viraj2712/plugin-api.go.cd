## Package Configuration
 
 This message is sent by the server, when it wants to know what properties need to be stored in the configuration, for this plugin and for this package. It also uses this information to create a view, for the user to provide information about the package.
 
The plugin will receive a request with following information.

<p class='request-name-heading'>Request name</p>

`package-configuration`

<p class='request-body-heading'>Request parameters</p>

The server will not provide any parameters.

<p class='request-body-heading'>Request headers</p>

The server will not provide any headers.

<p class='request-body-heading'>Request body</p>

The server will not provide request body.

> Example response body

```json
{
  "Field_1": {
    "display-name": "Package Spec",
    "display-order": "0",
    "default-value": "DEF",
    "secure": false,
    "part-of-identity": true,
    "required": true
  },
  "Field_2": {
    "display-name": "Field 2",
    "display-order": "1",
    "default-value": "ABC",
    "secure": true,
    "part-of-identity": true,
    "required": false
  }
}
```

<p class='response-code-heading'>Response code</p>

The plugin is expected to return status `200` if it can understand the request.

<p class='response-body-heading'>Response Body</p>

The plugin is expected to return an object containing the configuration property along with [package configuration object](#the-package-configuration-response-object)
