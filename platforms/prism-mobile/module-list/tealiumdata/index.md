---
title: TealiumData module
description: Adds core Tealium SDK metadata to the data layer for every tracking event.
url: https://docs.tealium.com/platforms/prism-mobile/module-list/tealiumdata/
---
The TealiumData module is a collector that automatically enriches tracking data with core Tealium SDK configuration and metadata. This module is always active and cannot be disabled.

## Data layer

The following variables are added to each tracking call:

| Variable | Description | Example |
| :--- | :--- | :--- |
| `tealium_account` | Tealium account identifier | `&#34;my_account&#34;` |
| `tealium_profile` | Tealium profile identifier | `&#34;my_profile&#34;` |
| `tealium_environment` | Tealium environment | `&#34;prod&#34;` |
| `tealium_datasource` | Data source identifier, if configured | `&#34;abc123&#34;` |
| `tealium_library_name` | Name of the Tealium library | `&#34;tealium-prism-swift&#34;` |
| `tealium_library_version` | Version of the Tealium library | `&#34;0.4.0&#34;` |
| `tealium_visitor_id` | Unique visitor identifier | `&#34;612040730c8c11ed&#34;` |
| `enabled_modules` | List of enabled module IDs | `[&#34;AppData&#34;, &#34;Lifecycle&#34;]` |
| `enabled_modules_versions` | Versions of enabled modules | `[&#34;1.0.0&#34;, &#34;1.0.0&#34;]` |
| `tealium_random` | Random 16-digit number for event deduplication | `&#34;7715219888555792&#34;` |

## Install

The TealiumData module is part of the Tealium Prism core SDK. No separate installation is required.



The module is included with `prism-core`, which is a transitive dependency of all other Prism modules.


The module is included in `TealiumPrismCore`. Add it as a Swift Package Manager dependency using the repo URL `https://github.com/Tealium/tealium-prism-swift`, or add it to your Podfile for CocoaPods:

```ruby
pod &#39;tealium-prism/Core&#39;
```

To install the full Prism library instead:

```ruby
pod &#39;tealium-prism&#39;
```



## Initialize

The TealiumData module initializes automatically.

This module is always active and cannot be disabled. Calling `setEnabled(false)` has no effect.
