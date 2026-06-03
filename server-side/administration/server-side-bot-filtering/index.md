---
title: Server-side bot filtering
description: This article describes how Tealium filters out bot traffic in server-side environments.
url: https://docs.tealium.com/server-side/administration/server-side-bot-filtering/
---
Server-side bot filtering is essential for maintaining the accuracy of data collected through Tealium server-side products.

This article focuses on server-side bot filtering. For details on client-side bot filtering, see .

## How it works

Bot traffic refers to non-human visits to a site or app. Tealium server-side products automatically filter out bot traffic by comparing the user agent of each event to a list of known bots. Filtered events are not processed and do not count towards your usage.

## User agents recognized as bots

Tealium recognizes bots by matching their user agent against a list of known patterns. If a user agent contains any of the following terms (case-insensitive), it is considered a bot:

```
robot
spider
200PleaseBot
360Spider
4seohuntBot
80legs
AdsBot
AhrefsBot
AlertSite
Alexibot
Applebot
atSpider
autoemailspider
Baiduspider
BecomeBot
Bingbot
BingPreview
Black.Hole
Black Hole
BLEXBot
BlowFish
Bullseye
CatchBot
Catchpoint
CCBot
Cheesebot
citeseerxbot
ContactBot
ContentSmartz
crawler4j
DataCha0s
datagnionbot
DBrowse
DotBot
DuckDuckBot
EmailSiphon
EmailSpider
envolk
Exabot
Facebot
facebookexternalhit
FAST-WebCrawler
FAST Enterprise Crawler
Feedfetcher-Google
Genieo
Gid_Synthetic
gigablast
Gigabot
GingerCrawler
Girafabot
GomezAgent
Googlebot
ia_archiver
ips-agent
Keynote
KHTE
KXTN
linkdexbot
LinkedInBot
Mediapartners-Google
MetaJobBot
Microsearch
MJ12bot
Mnogosearch
msnbot
MSRBot
NaverBot
oBot
PagePeeker
Pingdom
proximic
purebot
Psbot
redditbot
RU_bot
Scanbot
ScoutJet
Scrapy
SeznamBot
SimpleCrawler
SimplePie
Site24x7
SiteLockSpider
Slackbot
Slurp
Sosospider
Sougou
spbot
Speedy Spider
SPEng
Twiceler
Twitterbot
UnwindFetchor
Veoozbot
Voilabot
voyager
WebDataCentreBot
Webmetrics
WhatsApp
Yandex
yanga
Yodaobot
YottaaMonitor
Youdao
zibber
ZyBorg
```

## Customizing server-side bot filtering

If you need to prevent specific events from being sent server-side due to internal or bot traffic, you can:

* Add [load rules]() on the [Collect tag]() to restrict when it loads.
* Use client-side methods to stop the Collect tag from loading based on user agents.
For details on client-side bot filtering, see .
## Enabling server-side filtering in AudienceStream

For more advanced filtering, such as excluding certain user agent patterns or IP addresses, you can enable server-side filtering in AudienceStream. To set this up, contact your Tealium customer success manager for guidance.
