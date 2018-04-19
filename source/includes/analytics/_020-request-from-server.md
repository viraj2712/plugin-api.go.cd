# Requests from the GoCD server

In order to implement an analytics extension point the following messages must be implemented by the plugin.

* [Get Capabilities](#get-plugin-capabilities)
* [Get Static Assets](#get-static-assets)
* [Get Analytics](#get-analytics)
* [Plugin Settings Changed](#plugin-settings-changed)

These are general purpose messages that a plugin must implement to allow users to configure the plugin through the browser.

* [Get Plugin Icon](#get-plugin-icon)
* [Get Settings View](#get-settings-view)
* [Get Plugin Configuration](#get-plugin-configuration)
* [Validate Plugin Configuration](#validate-plugin-configuration)
