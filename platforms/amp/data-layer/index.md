---
title: Data Layer
description: Learn about the data layer variables from the AMP library.
url: https://docs.tealium.com/platforms/amp/data-layer/
---The following parameters are populated by the Tealium AMP Library. These variables are included automatically in each tracking call from the library and are used in your Tealium Customer Data Hub configuration.

In the following table, some variables are used for both page view/event tracking, while some are only used for each.

For page view tracking, the default event is `screen_view`. For event tracking, specify an event name using the variable `tealium_event`.

| Parameter | Description | Page Tracking | Event Tracking | Example |
| :-- | :-- | :-- | :-- | :-- |
| `amp_hostname` | AMP hostname | &amp;#10004; | &amp;#10004; | `example.com` |
| `amp_request_count` | AMP request count |  &amp;#10004; | &amp;#10004; |`1` |
| `amp_version` | AMP version number |  &amp;#10004; | &amp;#10004; | `1907022322580` |
| `ampdoc_url` | AMP document URL |  &amp;#10004; | &amp;#10004; | `http://example.com/path/to/file.html` |
| `canonical_hostname` | Canonical hostname | &amp;#10004; | &amp;#10004; | `example.ampproject.org` |
| `content_load_ms` | Time in milliseconds to load the content | &amp;#10004; |  | `66` |
| `domain` | The full domain name of the URL | &amp;#10004; | &amp;#10004; | `example.com` |
| `lang` | Language code | &amp;#10004; | &amp;#10004; | `en-us` |
| `page_view_id` | Page view ID number | &amp;#10004; | | `769` |
| `pathname` | Path of the URL, excluding the query parameters and domain | &amp;#10004; | &amp;#10004; | `/path/to/file.html` |
| `referrer` | URL path without the file name | &amp;#10004; | | `http://example.com/path/to/ `|
| `screen_size` | Screen resolution height x width (pixels) | &amp;#10004; | | `2560x1440` |
| `scroll_x` | Horizontal scrolling value (x-axis) | | &amp;#10004; | `0` |
| `scroll_y` | Vertical scrolling value (y-axis) | | &amp;#10004; | `0` |
| `tealium_visitor_id` | Generated uuid (case-sensitive) | &amp;#10004; | &amp;#10004; | `amp-ABc1dEF2gH3IJK4lmn5OPz` |
| `timestamp` | Epoch timestamp (overridden in the `vars` block)| &amp;#10004; | &amp;#10004; | `1563305241134` |
| `title` | AMP document&#39;s title (overridden in the `vars` block) | &amp;#10004; | &amp;#10004; | `Hello, AMP` |
| `tz` | Time zone | &amp;#10004; | &amp;#10004; | `420` |
| `url` | The full URL of the page | &amp;#10004; | &amp;#10004; | `http://example.com/path/file.html` |
| `viewport_height` | Browser viewport height (pixels) | &amp;#10004; | &amp;#10004; | `1417` |
| `viewport_width` | Browser viewport width (pixels) | &amp;#10004; | &amp;#10004; | `2560` |
