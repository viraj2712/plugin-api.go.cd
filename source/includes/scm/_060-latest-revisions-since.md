## Latest Revisions Since

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
    },
    "scm-data": {
        "dataKeyOne": "data-value-one",
        "dataKeyTwo": "data-value-two"
    },
    "flyweight-folder": "/var/lib/go-server/pipelines/flyweight-for-this-material",
    "previous-revision": {
        "revision": "revision-1",
        "timestamp": "2011-07-14T19:43:37.100Z",
        "data": {
          "dataKeyOne": "data-value-one",
          "dataKeyTwo": "data-value-two"
        }
    }
}
```

The plugin will receive request with following information.

<p class='request-name-heading'>Request name</p>

`latest-revisions-since`

<p class='request-body-heading'>Request parameters</p>

The server will not provide any parameters.

<p class='request-body-heading'>Request headers</p>

The server will not provide any headers.

<p class='request-body-heading'>Request body</p>

This request is very similar to the request of the ["Latest Revision" message](#latest-revision). This contains information about the SCM configuration provided by the user. The keys in the maps correspond to the keys provided by the plugin, as a part of the response to ["SCM Configuration"](#scm-configuration) messages.

Along with that information, this request contains information about the previous revision of the SCM that GoCD knows about. Compare the "previous-revision" data of the example request shown below, with the response of the ["Latest Revision" message](#latest-revision) to understand this.

<aside class="notice">
  <strong>Note:</strong> It is prudent to validate these details before using them, because direct editing of GoCD's configuration XML file does not cause <a href="#validate-scm-configuration">Validate SCM Configuration</a> to be sent to the plugin. So, the information sent to this call might not be validated by the plugin.
</aside>

> Example response body

```json
{
    "revisions" : [
        {
            "revision": "revision-2",
            "timestamp": "2011-07-14T19:45:37.100Z",
            "user": "some-user",
            "revisionComment": "comment 2",
            "data": {
                "dataKeyOne": "data-value-one-1",
                "dataKeyTwo": "data-value-two-2"
            },
            "modifiedFiles": [
                {
                    "fileName": "file-2",
                    "action": "modified"
                }
            ]
        }
    ],
    "scm-data": {
        "dataKeyOne": "data-value-one",
        "dataKeyTwo": "data-value-three"
    }
}
```

<p class='response-code-heading'>Response code</p>

The plugin is expected to return status `200` if it can understand the request.

<p class='response-body-heading'>Response Body</p>

Just as with the "Latest Revision" message, the plugin is expected to send a response, which contains information about the latest revision it can find of the SCM specified by the information in the request. The difference here, is that it needs to find a revisions of the SCM which is greater than the one specified in the request - previous-revision. It can send an empty response ({}) to specify that it could not find revisions (for instance, if there has been no change, and the latest revision is still the one specified in the request).

Almost all the fields expected in this response are explained in this [part of the user documentation](https://docs.gocd.org/current/extension_points/scm_extension.html#scm-information-display). The extra map, named "data" in the response, can be filled with custom key-value pairs, which will be made available to the agent, as environment variables, when a job contains this plugin as a material.