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
| `tealium_account` | Tealium account identifier | `"my_account"` |
| `tealium_profile` | Tealium profile identifier | `"my_profile"` |
| `tealium_environment` | Tealium environment | `"prod"` |
| `tealium_datasource` | Data source identifier, if configured | `"abc123"` |
| `tealium_library_name` | Name of the Tealium library | `"tealium-prism-swift"` |
| `tealium_library_version` | Version of the Tealium library | `"0.4.0"` |
| `tealium_visitor_id` | Unique visitor identifier | `"612040730c8c11ed"` |
| `enabled_modules` | List of enabled module IDs | `["AppData", "Lifecycle"]` |
| `enabled_modules_versions` | Versions of enabled modules | `["1.0.0", "1.0.0"]` |
| `tealium_random` | Random 16-digit number for event deduplication | `"7715219888555792"` |

## Install

The TealiumData module is part of the Tealium Prism core SDK. No separate installation is required.



The module is included with `prism-core`, which is a transitive dependency of all other Prism modules.


The module is included in `TealiumPrismCore`. Add it as a Swift Package Manager dependency using the repo URL `https://github.com/Tealium/tealium-prism-swift`, or add it to your Podfile for CocoaPods:

```ruby
pod 'tealium-prism/Core'
```

To install the full Prism library instead:

```ruby
pod 'tealium-prism'
```



## Initialize

The TealiumData module initializes automatically.


<blockquote>
This module is always active and cannot be disabled. Calling `setEnabled(false)` has no effect.
</blockquote>

