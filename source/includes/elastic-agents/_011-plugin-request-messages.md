# Requests from the GoCD server

In order to implement an elastic agent extension point the following messages must be implemented by the plugin.

* [Get Plugin Icon](#get-plugin-icon)
* [Capabilities](#get-plugin-capabilities)
* [Create Agent](#create-agent)
* [Should Assign Work](#should-assign-work)
* [Server Ping](#server-ping)
* [Job Completion](#job-completion)
* [Migrate Config](#migrate-config)

These are general purpose messages that a plugin must implement to allow users to configure the plugin through the browser.

* [Get Cluster Profile View](#get-cluster-profile-view)
* [Get Cluster Profile Metadata](#get-cluster-profile-metadata)
* [Validate Cluster Profile](#validate-cluster-profile)

These are messages that a plugin must implement in order to allow users to configure elastic profiles through the browser.

* [Get Elastic Agent Profile View](#get-elastic-agent-profile-view)
* [Get Elastic Agent Profile Metadata](#get-elastic-agent-profile-metadata)
* [Validate Elastic Agent Profile](#validate-elastic-agent-profile)

If a plugin supports supports status reports, apart from the above, the plugin must implement the following messages. The plugin should use the [Capabilities](#get-plugin-capabilities) to expose this feature.

* [Agent Status Report](#get-agent-status-report)
* [Get Cluster Status Report](#get-cluster-status-report)
* [Plugin Status Report](#get-plugin-status-report)
