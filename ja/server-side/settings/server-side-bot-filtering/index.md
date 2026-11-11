---
title: サーバーサイドのボットフィルタリング
description: この記事では、Tealiumがサーバーサイド環境でボットトラフィックを除外する仕組みについて説明します。
url: https://docs.tealium.com/ja/server-side/settings/server-side-bot-filtering/
---
サーバーサイドのボットフィルタリングは、Tealiumのサーバーサイド製品を通じて収集されるデータの正確性を維持するために不可欠です。

この記事では、サーバーサイドのボットフィルタリングについて説明します。クライアントサイドのボットフィルタリングについて詳しくは、[client-side-bot-filtering](https://docs.tealium.com/client-side-bot-filtering/)を参照してください。

## 仕組み

ボットトラフィックとは、サイトまたはアプリへの人間以外によるアクセスを指します。Tealiumのサーバーサイド製品は、各イベントのユーザーエージェントを既知のボットのリストと比較し、ボットトラフィックを自動的に除外します。除外されたイベントは処理されず、使用量にもカウントされません。

## ボットとして認識されるユーザーエージェント

Tealiumは、ユーザーエージェントを既知のパターンのリストと照合してボットを識別します。ユーザーエージェントに以下のいずれかの語句が含まれている場合（大文字と小文字は区別されません）、ボットと見なされます。

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

## サーバーサイドのボットフィルタリングのカスタマイズ

内部トラフィックまたはボットトラフィックが原因で、特定のイベントがサーバーサイドに送信されないようにする必要がある場合は、次の方法を使用できます。

* [Collectタグ](https://docs.tealium.com/tealium-collect-tag/)に[ロードルール](https://docs.tealium.com/manage-load-rules/)を追加し、タグが読み込まれる条件を制限します。
* ユーザーエージェントに基づいてCollectタグの読み込みを停止するクライアントサイドの方法を使用します。

クライアントサイドのボットフィルタリングについて詳しくは、[client-side-bot-filtering](https://docs.tealium.com/client-side-bot-filtering/)を参照してください。

## Customer Data Platform（CDP）でのサーバーサイドフィルタリングの有効化

特定のユーザーエージェントパターンやIPアドレスの除外など、より高度なフィルタリングを行うには、CDPでサーバーサイドフィルタリングを有効にできます。構成方法については、[サポートにお問い合わせください](https://docs.tealium.com/support/)。