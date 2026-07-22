---
title: Data Layer
description: Learn about the data layer variables from the AMP library.
url: https://docs.tealium.com/platforms/amp/data-layer/
---The following parameters are populated by the Tealium AMP Library. These variables are included automatically in each tracking call from the library and are used in your Tealium Customer Data Hub configuration.

In the following table, some variables are used for both page view/event tracking, while some are only used for each.


<blockquote>
For page view tracking, the default event is `screen_view`. For event tracking, specify an event name using the variable `tealium_event`.
</blockquote>


| Parameter | Description | Page Tracking | Event Tracking | Example |
| :-- | :-- | :-- | :-- | :-- |
| `amp_hostname` | AMP hostname | &#10004; | &#10004; | `example.com` |
| `amp_request_count` | AMP request count |  &#10004; | &#10004; |`1` |
| `amp_version` | AMP version number |  &#10004; | &#10004; | `1907022322580` |
| `ampdoc_url` | AMP document URL |  &#10004; | &#10004; | `http://example.com/path/to/file.html` |
| `canonical_hostname` | Canonical hostname | &#10004; | &#10004; | `example.ampproject.org` |
| `content_load_ms` | Time in milliseconds to load the content | &#10004; |  | `66` |
| `domain` | The full domain name of the URL | &#10004; | &#10004; | `example.com` |
| `lang` | Language code | &#10004; | &#10004; | `en-us` |
| `page_view_id` | Page view ID number | &#10004; | | `769` |
| `pathname` | Path of the URL, excluding the query parameters and domain | &#10004; | &#10004; | `/path/to/file.html` |
| `referrer` | URL path without the file name | &#10004; | | `http://example.com/path/to/ `|
| `screen_size` | Screen resolution height x width (pixels) | &#10004; | | `2560x1440` |
| `scroll_x` | Horizontal scrolling value (x-axis) | | &#10004; | `0` |
| `scroll_y` | Vertical scrolling value (y-axis) | | &#10004; | `0` |
| `tealium_visitor_id` | Generated uuid (case-sensitive) | &#10004; | &#10004; | `amp-ABc1dEF2gH3IJK4lmn5OPz` |
| `timestamp` | Epoch timestamp (overridden in the `vars` block)| &#10004; | &#10004; | `1563305241134` |
| `title` | AMP document's title (overridden in the `vars` block) | &#10004; | &#10004; | `Hello, AMP` |
| `tz` | Time zone | &#10004; | &#10004; | `420` |
| `url` | The full URL of the page | &#10004; | &#10004; | `http://example.com/path/file.html` |
| `viewport_height` | Browser viewport height (pixels) | &#10004; | &#10004; | `1417` |
| `viewport_width` | Browser viewport width (pixels) | &#10004; | &#10004; | `2560` |
