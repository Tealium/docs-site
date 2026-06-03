---
title: Frequency capping example
description: This article provides a usage example of frequency capping.
url: https://docs.tealium.com/server-side/connectors/frequency-capping/example/
---
This example shows two cooldown groups and one connector containing four actions.

|**Action Name**| **Cooldown Group**| **Cooldown Hours**| **Priority Number**| **Additional Delay**|
|---| ---| ---| ---| ---|
|A| Group 1| 48 hours| 40| —|
|B| Group 1| 48 hours| 30| 2 hours|
|C| Default| 24 hours| 1| —|
|D| No Cooldown| —| —| —|

In this scenario, cooldown periods are applied to the actions as follows:

* **Group 1**
    * If Action A evaluates to true before Action B, only Action A triggers.
    * The 48-hour cooldown starts, during which neither Action A nor B trigger.
    * If Action B evaluates to true before Action A, only Action B triggers after the configured 2-hour delay.
    * The 48-hour cooldown then starts, during which neither Action A nor B trigger.
    * If Actions A and B evaluate to true at the same time, only Action A triggers because it has the highest priority number.
    * During the cooldown period, both actions are suppressed.
    * Suppressed actions are not queued to run when the cooldown expires. They trigger only if their conditions evaluate to true again after the cooldown ends.

* **Default**
    * When Action C evaluates to true, it triggers immediately.
    * The 24-hour cooldown starts, during which Action C does not trigger again.

* **No Cooldown**
    * Action D triggers immediately whenever its condition evaluates to true because it is not assigned to a cooldown group.
