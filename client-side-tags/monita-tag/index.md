---
title: Monita Tag Setup Guide
description: This article describes how to set up the Monita tag in your Tealium iQ Tag Management account.
url: https://docs.tealium.com/client-side-tags/monita-tag/
---
Monita is a tag monitoring platform. It provides real-time dashboards that show what tags and pixels are airing and what data they are sending. Monita can also send real-time alerts when your business conditions are breached or PII (Personally Identifiable Information) is detected.

Monita’s tag code is designed to be loaded as a library before the page loads. So, instead of using the Tealium tag marketplace to install this tag, use the [JavaScript Extension](https://docs.tealium.com/javascript-code-extension/).

## Tag Configuration

### Monita monitor configuration

Before you install the Monita tag, you must [configure the Monita monitor](https://docs.google.com/document/d/1X--Dyl3Pdnp2JJKzX1ckAx41cGDRkvTaX-AiHrS0QbY/edit) on their site. To configure the Monita monitor, perform the following steps:

1. Sign up for Monita and enter your details in the onboarding screen.
1. Click **Monitoring**.
1. From the **Select Tag Manager** picklist, select **Tealium**.
1. Enter your domain or domains.
1. Click **+ NEW VENDOR**.
1. Select a vendor to monitor.
1. Click **Save**.

The installation guide will appear. Follow its instructions, and copy the code block to a notepad.

### Monita tag configuration

To install the Monita tag, perform the following steps:

1. Go to **Extensions** and click **+ Add Extension**.
1. Click **Advanced** and click **+ Add** next to **JavaScript Code**.
1. Under **Title**, enter `Monita`.
1. Under the **Scope** drop-down, select **Pre Loader**.
1. Click **Edit Load Order** and set the Monita extension to `1`.
1. Copy the code block from Monita into the extension configuration.
1. Save and Publish.