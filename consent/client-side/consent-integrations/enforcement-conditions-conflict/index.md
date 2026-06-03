---
title: Handling conflicts in enforcement conditions
description: This article describes how consent integrations handles conflicts in the conditional enforcement of purpose groups and exemptions, while adhering to privacy by design and privacy by default principles.
url: https://docs.tealium.com/consent/client-side/consent-integrations/enforcement-conditions-conflict/
---
## Privacy principles

We built consent integrations with strict adherence to privacy by design and privacy by default principles. Consent integrations ensures that data activation for your business complies with relevant policies and regulations, and protects against data leaks caused by user error or misconfiguration. These principles require that data processing and activation are allowed only when explicit consent or clear conditions are met.

## How Consent integrations handles conflicts in enforcement conditions

* **When at least one consent integration or exemption is active**: No data processing is allowed without a specific signal from your consent management platform (CMP).
* **When two or more enforcement rules overlap for integrations**: Tealium iQ does not load, and no tags fire.
* **When an integration overlaps exemptions**: If a single integration overlaps with any number of exemptions, the integration is enforced and the exemptions are disregarded.

In ambiguous scenarios, such as when two integrations are active and both of their enforcement rules evaluate to `true`, consent integrations withholds data processing and activation to protect against potential data leaks. This behavior may result in the loss of data from blocked tags, but it is a precautionary measure to mitigate the risk of data leaks.

The following table shows how consent integrations handles conflicts depending on the number of active exemptions and integrations:

| Exemptions | Integrations | Conflict Handling |
|----------------|------------------|-----------------------|
| 0   | 0  | Block all data processing |
| 1&#43;  | 0  | Allow all data processing |
| Any | 1  | Apply purpose-specific blocking |
| Any | 2&#43; | Block all data processing |
