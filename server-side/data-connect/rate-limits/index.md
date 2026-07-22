---
title: Rate limits
description: This article describes Data Connect rate limits.
url: https://docs.tealium.com/server-side/data-connect/rate-limits/
---
Data Connect uses the following rate limits:

* The Tealium Events app has the following limits:
  * Rate limit of 500 events/second.
  * Records rate limit of 500 records/second. Larger file sizes are broken down into batches of 500 records each.
<blockquote>
If your Data Connect usage exceeds the above rates, your connection will be throttled.
</blockquote>

* Workato JSON import file size maximum: 10 MB.
* Data Connect requests size maximum: 2.5 MB.


<blockquote>
To reduce costs and increase processing efficiency, maximize the file batches according to the limits above and minimize the number of Workato [tasks](https://docs.tealium.com/workato-glossary/) you need to accomplish your business goals.
</blockquote>

