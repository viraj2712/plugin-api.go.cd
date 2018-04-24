## SCM View

This message is sent by the server, to get a template to show to the user, to allow information about a SCM to be provided.

<p class='request-name-heading'>Request name</p>

`scm-view`

<p class='request-body-heading'>Request parameters</p>

The server will not provide any parameters.

<p class='request-body-heading'>Request headers</p>

The server will not provide any headers.

<p class='request-body-heading'>Request body</p>

The server will not provide request body.

> Example response body

```json
{
   "displayValue": "JGit",
   "template": "<div class=\"form_item_block\"><label>Message:<span class=\"asterisk\">*</span></label><input type=\"text\" ng-model=\"message\" ng-required=\"true\"></div>"
}
```

<p class='response-code-heading'>Response code</p>

The plugin is expected to return status `200` if it can understand the request.

<p class='response-body-heading'>Response Body</p>

The plugin is expected to return an object containing the view rendering information [scm view response object](#the-scm-view-response-object)