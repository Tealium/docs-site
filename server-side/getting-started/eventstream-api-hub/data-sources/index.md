---
title: Data sources
description: A data source is any system that sends data to Tealium EventStream. These systems include websites, native mobile apps, or any custom application that can report event data.
url: https://docs.tealium.com/server-side/getting-started/eventstream-api-hub/data-sources/
---
Data sources are platform-specific and provide the necessary code and instructions to complete an installation.

Example types of data sources:

* JavaScript for Web (Tealium iQ Tag Management)
* iOS (Swift)
* Android
* Apple TV
* Roku
* Server-side apps (Python, Java)
* HTTP API

To add Tealium to your website or app, you first create a data source to get the code and instructions to complete the installation. Each data source has a name, description, and data source key that uniquely identifies the platform where it&#39;s installed.

## How it works

Data sources are used to easily identify and keep track of your sites and apps that send data to your account.

Here&#39;s how it works:

1. Choose the platform you want to install on--such as Swift (iOS), Android, or JavaScript for Web--and give it a name such as `mydomain.com` or `MyBrandApp`.
1. Copy the sample code and data source key from the installation instructions. The data source key uniquely identifies the data source you just created.
1. After the code is installed with the data source key, go to **Live Events** to view events coming from that data source.

Example data source:

![](/images/tutorials/eventstream-getting-started-data-source-key.png)

Example installation code:

```swift
var tealConfig = TealiumConfig(
    account: &#34;your_account&#34;,
    profile: &#34;your_profile&#34;,
    environment: &#34;prod&#34;,
    datasource: &#34;abc123&#34;)

let tealium = Tealium(config: tealConfig)
```

The next tutorial demonstrates how to add a data source to your account.