---
title: Handling conflicts in enforcement conditions
description: This article describes how consent orchestration handles conflicts in the conditional enforcement of purpose groups and exemptions, while adhering to privacy by design and privacy by default principles.
url: https://docs.tealium.com/consent/server-side/consent-orchestration/enforcement-conditions-conflict/
---
## Privacy principles

Consent orchestration processes and activates data only when explicit consent is granted or clear conditions are met. It ensures compliance with relevant policies and regulations, protecting against data leaks caused by user error or misconfiguration.

## How consent orchestration handles conflicts in enforcement conditions

Conflicts in consent orchestration arise when multiple enforcement rules for components, such as purpose groups and exemptions, overlap or contradict each other. These conflicts are more common when you have multiple consent policies or complex enforcement rules. Here&#39;s how consent orchestration manages these conflicts to ensure data protection.

When an event meets the following conditions:

* **A purpose group and one or more exemptions have enforcement rules that evaluate to `true`**: This creates a conflict because exemptions allow data processing without consent controls, while purpose groups enforce strict rules for data processing. To resolve this conflict, the purpose group is enforced, and exemptions are disregarded. No data processing is allowed without a consent signal.

* **Enforcement rules for multiple purpose groups evaluate to `true`**: When enforcement rules for two or more purpose groups apply, it&#39;s unclear which should be enforced. To prevent accidental data leaks, all data processing is blocked. 

* **Enforcement rules for multiple exemptions evaluate to `true`**: Overlapping exemptions do not conflict with each other. When enforcement rules for only exemptions apply, processing is allowed. However, if an enforcement rule for even one purpose group applies, it takes priority and all exemptions are disregarded.

In ambiguous scenarios, such as where two purpose groups are present and their enforcement rules both evaluate to `true`, consent orchestration withholds data processing and activation to protect against potential data leaks. This may result in the loss of data from blocked activations, but it is a precautionary measure to mitigate the risk of data leaks.

### Example of conflicting enforcement conditions

This example is for illustration purposes only.

Conflicts can arise in complex scenarios such as domain conflicts. For instance, one purpose group might apply to events where the domain contains `A`, while another purpose group applies to events where the domain contains `B`. If an event comes in with a domain that contains both `A` and `B` (such as domain `AB`), both enforcement rules evaluate to true, creating a conflict. In such cases, consent orchestration cannot determine which policy to enforce, resulting in withholding data processing and activation to prevent potential data leaks.

The following table shows how consent orchestration handles conflicts depending on the number of active exemptions and purpose groups:

This table only applies when consent orchestration is active (at least one exemption or purpose group is active, even if no enforcement conditions apply). If no exemption or purpose group is active, consent orchestration remains inactive and will not block any activations.

| **Exemptions** | **Purpose Group** | **Conflict Handling** |
|----------------|------------------|-----------------------|
| 0   | 0  | Block all data processing |
| 1&#43;  | 0  | Allow all data processing |
| Any | 1  | Apply purpose-specific blocking |
| Any | 2&#43; | Block all data processing |
