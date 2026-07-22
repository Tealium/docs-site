---
title: Data Sources: Install and Test
description: Installing and testing the HTTP API is as simple as entering a URL into a browser. If you chose a different platform for your data source, go ahead and add the necessary code according to the installation instructions.
url: https://docs.tealium.com/server-side/getting-started/eventstream-api-hub/install-test/
---
## Send a test event

Events are identified in EventStream by the `tealium_event` attribute. For our test event, we will send an event called `search`.

Using the `GET` method, our test event URL looks like this (line breaks added for readability):

```none
https://collect.tealiumiq.com/event?
tealium_account=your_account
&tealium_profile=your_profile
&tealium_datasource=abc123
&tealium_event=search
```

The corresponding code in Swift (iOS) might look like this:

```swift
var tealConfig = TealiumConfig(
    account: "your_account",
    profile: "your_profile",
    environment: "prod",
    datasource: "abc123")

let tealium = Tealium(config: tealConfig)

// Tracked event "search" automatically results in:
// tealium_event : "search" in the event data
tealium?.trackEventWithTitle("search", dataSources: [:])
```

Let's go to the next step to see how to observe those test events on the **Live Events** screen.