## Latest Revision

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
  },
  "package-configuration": {
    "PACKAGE_SPEC": {
      "value": "sample-package-1.0"
    }
  }
}
```
 
<p class='request-name-heading'>Request name</p>

`latest-revision`

<p class='request-body-heading'>Request parameters</p>

The server will not provide any parameters.

<p class='request-body-heading'>Request headers</p>

The server will not provide any headers.

<p class='request-body-heading'>Request body</p>

This contains information about both the [repository-level configuration](#the-repository-configuration-response-object) and [package-level configuration](#the-package-configuration-response-object) provided by the user. The keys in the maps correspond to the keys provided by the plugin, as a part of the response to ["Repository Configuration"](#repository-configuration) and ["Package Configuration"](#package-configuration) messages.

<aside class="notice">
  <strong>Note:</strong> It is prudent to validate these details before using them, because direct editing of GoCD's configuration XML file does not cause <a href="#validate-package-configuration">Validate Package Configuration</a> message to be sent to the plugin. So, the information sent to this call might not be validated by the plugin.
</aside>

> Example response body

```json
{
  "revision": "abc-10.2.1.rpm",
  "timestamp": "2011-07-14T19:43:37.100Z",
  "user": "some-user",
  "revisionComment": "comment",
  "trackbackUrl": "http://localhost:9999",
  "data": {
    "VERSION": "5.3.0",
    "LOCATION": "http://www.sample.org/location/of/package",
    "DATA-THREE": "data-three-value"
  }
}
```

<p class='response-code-heading'>Response code</p>

The plugin is expected to return status `200` if it can understand the request.

<p class='response-body-heading'>Response Body</p>

The plugin is expected to send a response, which contains information about the latest revision it can find of the package specified by the information in the request. It can send an empty response (`{}`) to specify that it could not find a suitable package.

Almost all the fields expected in this response are explained in this [part of the user documentation](https://docs.gocd.org/current/extension_points/package_repository_extension.html#package-information-display). The extra map, named "data" in the response, can be filled with custom keys and values, which will be made available to the agent, as environment variables, when a job contains this plugin as a material.
