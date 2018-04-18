### Request key: `link-external`

Any links opened directly from the plugin's front-end will open inside the iframe. For security reasons, the iframe cannot affect the
navigation of the parent GoCD window directly. Instead, the iframe can send a message with the key `link-external` to the parent window to
link to a page outside of GoCD. The parent window will open the page in a new tab.

> An example message from iframe to parent window to link to an external page:

```html
<html>
<head>
  <script src="analytics-endpoint.js"></script>
  <script>
  AnalyticsEndpoint.onInit(function(initialData, transport) {
    ...
    transport.request("link-external", {
      url: "https://url.link.to.external.page"
    })
    .done(function(data) {
      console.log("Navigated to the specified URL!");
    })
    .fail(function(errors) {
      console.log("Something failed: " + errors);
    });
  });

  AnalyticsEndpoint.ensure("v1");
  </script>
</head>
<body>
  ...
</body>
</html>
}
```

The parameter object should contain:

| Key   | Description                          |
|-------|--------------------------------------|
| `url` | The URL that should be navigated to. |
