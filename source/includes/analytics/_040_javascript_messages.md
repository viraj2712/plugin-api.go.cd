# Analytics JS API

> Example HTML:

```html
<html>
  <head>
    <script src="analytics-endpoint.js"></script>
    <script>
      // Your script here
    </script>
  </head>
  ...
</html>
```

> Example load using a Javascript module loading system:

```javascript
const AnalyticsEndpoint = require("analytics-endpoint.js");

// The rest of your script here...
```

GoCD renders analytics plugin content in <a href='https://developer.mozilla.org/en-US/docs/Web/HTML/Element/iframe'
target='_blank'>sandboxed</a> iframes. Within these sandboxed iframes, the plugin content may only execute its own JS code; it has no access
to the parent window context or cookies, and is therefore unable to make authenticated requests on the user's behalf.

Because of this isolation, all communication between the parent GoCD window and the plugin iframe is via the <a
href='https://developer.mozilla.org/en-US/docs/Web/API/Window/postMessage' target='_blank'>window.postMessage()</a> mechanism. To make the
communication easier between GoCD and the sandboxed plugin iframes, GoCD provides the `AnalyticsEndpoint` JS client to provide simple
request-response semantics as an abstraction over the cross-origin/sandbox communication details. Please see examples in the [Analytics
Skeleton Plugin](https://github.com/gocd-contrib/analytics-skeleton-plugin/blob/master/assets/pipeline-chart.html) to see a usage of the
analytics-endpoint.js API's.

**The JS client script is automatically injected into your plugin's static asset root after your plugin is loaded.** Loading the `AnalyticsEndpoint` client in plugin scripts merely involves requiring the file `analytics-endpoint.js`.


## Usage

<p class='request-body-heading'>AnalyticsEndpoint.onInit(callback)</p>

> Example setup:

```html
<html>
<head>
  <script src="analytics-endpoint.js"></script>
  <script>
  AnalyticsEndpoint.onInit(function(initialData, transport) {
    // Your code goes here to render your initial data and
    // any further interactions with the GoCD parent page.
  });

  AnalyticsEndpoint.ensure("v1"); // Finally, set up receiving endpoint
  </script>
</head>
<body>
  ...
</body>
</html>
```

This is the entry point to all plugin code, and will execute once the frame is loaded and `AnalyticsEndpoint.ensure()` has set up the receiving endpoint. The `callback` argument is an initializer function that receives the following parameters:

| Parameter     | Description                                                                                                            |
|---------------|------------------------------------------------------------------------------------------------------------------------|
| **data**      | The initial data from the [`go.cd.analytics.get-analytics`](#get-analytics) JSON payload.                                             |
| **transport** | A [Transport instance](#the-transport-object) to provide a way to send further communication to the parent GoCD frame. |


<p class='request-body-heading'>AnalyticsEndpoint.ensure(version)</p>

This sets up the receiving endpoint for messages from GoCD. The `version` parameter is required, and must be a supported version string. Currently, this is only `"v1"`.

## The Transport Object

The `Transport` object provides an AJAX-like API to facilitate communication with GoCD. It provides a chainable callback setup, similar to
`jQuery.ajax` handlers. It has a `request` method, which takes two parameters:

| Parameter  | Description                                                                                                               |
|------------|---------------------------------------------------------------------------------------------------------------------------|
| requestKey | The request that needs to be sent to the GoCD iframe. Needs to be one of `fetch-analytics`, `link-to` or `link-external`. |
| parameters | A parameter object which depends on the `requestKey` used.                                                                |


The `request method `returns a chainable object to set up `done`, `fail`, and `always` callbacks:

1. `done(function(data) {})`: fires upon successful response from GoCD. Similar to [done() in jQuery](https://api.jquery.com/deferred.done/).
2. `fail(function(errors) {})`: fires upon error response from GoCD. Similar to [fail() in jQuery](https://api.jquery.com/deferred.fail/)
3. `always(function() {})`: fires after response is received, regardless of success/failure. executes after `done()` or `fail()`. Similar to
   [always() in jQuery](https://api.jquery.com/deferred.always/).
