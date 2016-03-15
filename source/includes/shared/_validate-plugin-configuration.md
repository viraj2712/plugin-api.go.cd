## Validate Plugin Configuration

If a plugin requires any configuration, this message must be implemented in order to validate the configuration.

<p class='request-name-heading'>Request name</p>

`go.plugin-settings.validate-configuration`

<p class='request-body-heading'>Request body</p>

> An example validation request body

```json
{
  "plugin-settings": {
      "server_url": {
        "value": "http://localhost.com"
      },
      "username": {
        "value": "user"
      },
      "password": {
        "value": "password"
      }
  }
}
```

The request body will contain a JSON with an attribute `plugin-settings`, which contains an object with the configuration keys and values that the plugin is expected to validate.

<p class='response-code-heading'>Response code</p>

The plugin is expected to return status `200` if could understand the request.

<p class='response-body-heading'>Response Body</p>

> The plugin should respond with JSON array response for each configuration key that has a validation error

```json
[
  {
   "key": "server_url",
   "message": "Server URL cannot be localhost"
  }
]
```

If any of the input keys have a validation error on them, the plugin is expected to return a list of [validation error objects](#the-validation-error-object). If the configuration is valid, the plugin should return an empty JSON array.
