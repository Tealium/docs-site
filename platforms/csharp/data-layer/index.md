---
title: Data Layer
description: Learn about the data layer variables from the C# library.
url: https://docs.tealium.com/platforms/csharp/data-layer/
---
The following variables are populated by the Tealium C# Library as part of the mobile data layer. These variables are included automatically in each tracking call from the library.

| Parameter | Type | Description  | Example |
| --- | --- | --- | --- |
| `tealium_account` | `string` | Tealium account name used to initialize library| `"companyXYZ"` |
| `tealium_profile` | `string` |Tealium profile name used to initialize library	| `"main"` |
| `tealium_environment` | `string` |Tealium environment used to initialize library |[`"dev"`, `"qa"`, `"prod"`]|
| `tealium_event` |	`string` |Title of event. Populated by eventTitle argument of the Tealium track calls |  `"Some Event"` |
| `tealium_datasource` | 	`string` | 6-char alphanumeric name provided by Tealium Customer Data Hub  |`"abc123"`|
| `tealium_visitor_id` | `string` |Unique device visitor ID that differentiates users (required by Collect Service)  | `"t3aL...1uM"` |
| `tealium_library_name` | `string` |Name of the platform integration library |  `"csharp"` |
| `tealium_library_version` | `string` |Version of the platform integration library | `"1.0.0"` |
| `tealium_random` | `string` |Random 16 digit number generated per event	 |  `"1234567890123456"` |
| `tealium_session_id` | `string` |Unix epoch timestamp in milliseconds, no decimals, of first event (resets after a new session starts/launches)  | `"1496350751928"` |
| `tealium_timestamp_epoch` | `string` |Unix timestamp at UTC  | `"1496350751"` |
