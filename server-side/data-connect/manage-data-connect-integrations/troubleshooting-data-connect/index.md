---
title: Troubleshooting
description: This article describes how to troubleshoot issues in Data Connect.
url: https://docs.tealium.com/server-side/data-connect/manage-data-connect-integrations/troubleshooting-data-connect/
---
## Payload sizes

The Tealium Events V2 app automatically sends data to Tealium in batches of 500 events, even if your Workato recipe step sends more than 500 events to Tealium in one call.

In the rare case where the payload size for 500 events is too large, the Tealium endpoint returns a 413 error code. In this case, use a **Repeat Action** loop with the Tealium Events V2 app to break your data into smaller payload sizes.

To use the **Repeat Action** loop:

1. Click **&#43;** to see a list of actions.
1. Select **Repeat action**.
1. Set the loop repeat mode to **Batch of items**.
1. Set the **Batch size** to less than 500, but to as large as possible without getting the 413 error code. You need to determine this size by experimentation.
