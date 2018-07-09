# Requests from the GoCD server

In order to implement an artifact extension point the following messages must be implemented by the plugin.

* [Publish Artifact](#publish-artifact)
* [Fetch Artifact](#fetch-artifact)
* [Capabilities](#get-plugin-capabilities)

These are general purpose messages that a plugin must implement to allow users to configure the plugin through the browser.

* [Get Plugin Icon](#get-plugin-icon)

These are messages that a plugin must implement in order to allow users to configure artifact stores through the browser.

* [Get Store Config Metadata](#get-store-config-metadata)
* [Get Store Config View](#get-store-config-view)
* [Validate Store Config](#validate-store-config)

These are messages that a plugin must implement in order to allow users to configure publishing an artifact through the browser.

* [Get Publish Artifact Metadata](#get-publish-artifact-metadata)
* [Get Publish Artifact View](#get-publish-artifact-view)
* [Validate Publish Artifact Configuration](#validate-publish-artifact-config)

These are messages that a plugin must implement in order to allow users to configure fetching an artifact through the browser.

* [Get Fetch Artifact Metadata](#get-fetch-artifact-metadata)
* [Get Fetch Artifact View](#get-fetch-artifact-view)
* [Validate Fetch Artifact Configuration](#validate-fetch-artifact-config) 
