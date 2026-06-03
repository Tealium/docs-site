---
title: Data Layer
description: Learn about the data layer variables from the C# library.
url: https://docs.tealium.com/platforms/csharp/data-layer/
---
The following variables are populated by the Tealium C# Library as part of the mobile data layer. These variables are included automatically in each tracking call from the library.

| Parameter | Type | Description  | Example |
| --- | --- | --- | --- |
| `tealium_account` | `string` | Tealium account name used to initialize library| `&#34;companyXYZ&#34;` |
| `tealium_profile` | `string` |Tealium profile name used to initialize library	| `&#34;main&#34;` |
| `tealium_environment` | `string` |Tealium environment used to initialize library |[`&#34;dev&#34;`, `&#34;qa&#34;`, `&#34;prod&#34;`]|
| `tealium_event` |	`string` |Title of event. Populated by eventTitle argument of the Tealium track calls |  `&#34;Some Event&#34;` |
| `tealium_datasource` | 	`string` | 6-char alphanumeric name provided by Tealium Customer Data Hub  |`&#34;abc123&#34;`|
| `tealium_visitor_id` | `string` |Unique device visitor ID that differentiates users (required by Collect Service)  | `&#34;t3aL...1uM&#34;` |
| `tealium_library_name` | `string` |Name of the platform integration library |  `&#34;csharp&#34;` |
| `tealium_library_version` | `string` |Version of the platform integration library | `&#34;1.0.0&#34;` |
| `tealium_random` | `string` |Random 16 digit number generated per event	 |  `&#34;1234567890123456&#34;` |
| `tealium_session_id` | `string` |Unix epoch timestamp in milliseconds, no decimals, of first event (resets after a new session starts/launches)  | `&#34;1496350751928&#34;` |
| `tealium_timestamp_epoch` | `string` |Unix timestamp at UTC  | `&#34;1496350751&#34;` |
