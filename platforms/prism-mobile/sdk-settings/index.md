---
title: SDK settings
description: Configure Tealium Prism SDK runtime settings from your mobile profile.
url: https://docs.tealium.com/platforms/prism-mobile/sdk-settings/
---
SDK settings let you configure Prism SDK runtime behavior remotely from Tealium, without changing your app code. Settings are delivered to the SDK through the remote configuration file and take effect on the next remote settings refresh or app startup.

## Add SDK settings

To add and configure SDK settings remotely:

1. Log in to your mobile profile and go to **SDK Settings**.
3. Select **Add Setting** and adjust the settings.
4. Save and publish your changes.

The SDK picks up the new settings on the next remote settings refresh or at the next app startup if a settings URL is configured in `TealiumConfig`.

## Available settings

| Setting | Description |
| :--- | :--- |
| `max_queue_size` | The maximum number of dispatches the queue can hold. The queue uses FIFO order: when the limit is reached, the oldest dispatch is removed to make room for the new one. |
| `queue_expiration` | The expiration time for dispatches in the queue. A dispatch that is not sent within this time is removed from the queue. |
| `log_level` | The minimum log level for messages emitted by the SDK. |
| `remote_settings_refresh_interval` | The minimum time between remote settings refreshes. A refresh also occurs at every app startup when a settings URL is provided in `TealiumConfig`. |
| `visitor_identity_key` | The data layer key the SDK checks to perform automatic visitor switching. |
