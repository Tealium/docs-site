---
title: Vendor Integrations
description: A vendor integration is a pre-built remote command module that installs the vendor SDK and defines native code handlers for the vendor's API.
url: https://docs.tealium.com/platforms/remote-commands/vendor-integrations/
---
## Requirements

Implementing a vendor integration requires the following:

* **Vendor remote command module**  
In your app build scripts, replace the vendor SDK with the Tealium remote command module. The remote command module handles the vendor SDK installation and setup for you.
See the [list of remote command vendor integrations](/platforms/remote-commands/integrations/).

* **Configuration** (Choose one of the following)
  * **JSON File**  
  A JSON file, loaded locally or hosted remotely, containing the vendor settings, data mappings, and event triggers. See the [JSON file specification](/platforms/remote-commands/json-file/).
  * **Remote Command Tag**  
  A tag in iQ Tag Management that offers configuration options for the vendor&#39;s API (for use with the Tag Management module).

## How it works

The following diagram illustrates how vendor integrations and custom remote commands trigger functionality in your native app. Beginning with a visitor purchase tracked in your app, the Tealium SDK triggers remote commands in apps like Firebase, Facebook, or your own custom remote command. The remote command can trigger any native method available in the SDK, such as logging a purchase in Firebase, tracking an event in Facebook App Events, or displaying a custom notification in your app.

![](/images/platforms/remote-commands/remote_commands_data_flow_diagram.png)