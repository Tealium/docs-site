---
title: Server-side Global Privacy Control
description: This article describes Tealium's server-side support for Global Privacy Control (GPC), a proposed browser standard that allows users to opt out of the sale or sharing of their personal data.
url: https://docs.tealium.com/consent/server-side/server-side-support-gpc/
---
[Global Privacy Control](https://globalprivacycontrol.org/) (GPC) provides a global way to opt out of the sale or sharing of personal data at the browser level. For more information about GPC, see [About Global Privacy Control]().

The needs and requirements of our customers vary widely, so we intend to provide a flexible foundation for our customers to build upon.

This article describes Tealium&#39;s server-side support for GPC. For information on client-side support, see [Client-side Global Privacy Control]()

## Server-side support
 
Tealium server-side customers can add the GPC event-level attribute `global_privacy_control_opt_out`, populated on each event with the Global Privacy Control header (`Sec-GPC`). 

Possible values for the `global_privacy_control_opt_out` attribute are `true` (`Sec-GPC: 1`) or `false` (`Sec-GPC:0`). When the GPC header isn&#39;t present in the incoming event, the `global_privacy_control_opt_out` attribute will not be defined in the payload. No event-level attribute is added automatically to customer configurations, but the GPC event-level attribute populates as appropriate when added. 

To use the server-side signal, add a new event attribute **Universal Variable** as a string or boolean. The new attribute can then be enriched to Visitor Profiles as appropriate and used to [enforce the decision]() at the points of activation.
