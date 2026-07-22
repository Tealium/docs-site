---
title: クライアントサイドのボットフィルタリング
description: この記事では、クライアントサイドの環境でボットのトラフィックをフィルタリングする方法について説明します。
url: https://docs.tealium.com/ja/iq-tag-management/administration/client-side-bot-filtering/
---
クライアントサイドのボットフィルタリングにより、有効な人間が生成したデータのみが収集され、分析や他のデータ駆動型プロセスの整合性が保たれます。

この記事では、クライアントサイドのボットフィルタリングに焦点を当てています。サーバーサイドのボットフィルタリングの詳細については、[server-side-bot-filtering](https://docs.tealium.com/server-side-bot-filtering/)を参照してください。

## 仕組み

クライアントサイドでボットをフィルタリングするための2つの方法があり、それらはユーザーエージェントを使用します。

* ボットが検出されたときにutagの読み込みを防ぐ。
* ボットが検出されたときにタグの読み込みを防ぐ。

これらの方法は、ボットが検出されたときにタグと`utag.js`スクリプトの読み込みを防ぎ、ボットのトラフィックがデータ収集に干渉するのを防ぎます。両方の方法とも、ベンダータグとCollectタグのデータの整合性を保つ（サーバーサイドに`i.gif`リクエストが送信されない）。

## ボットが検出されたときにutagの読み込みを防ぐ

この方法では、正規表現（regex）パターンを使用してボットを検出し、`utag.js`スクリプトの読み込みを防ぎます。正当なクローラー、またはボットは、それを識別するために使用できるユニークなユーザーエージェントを持っています。ボットをそのユーザーエージェントの値を通じて識別することで、`utag.js`のリクエストを制御し、その読み込みを防ぐことができます。この方法は、Tealiumの外部での実装を必要とします。

### 実装手順

**`utag.js`を読み込むソースコード**

```html
<!-- Tealium Universal Tag -->
<script type="text/javascript">
  utag_cfg_ovrd = window.utag_cfg_ovrd || {};
  utag_cfg_ovrd.isabot = false;
  
  // Update the Bot List Pattern below
  utag_cfg_ovrd.botList = 'UPDATE_BOT_LIST_PATTERN_HERE'.toLowerCase();
  utag_cfg_ovrd.user_agent_regex = new RegExp(utag_cfg_ovrd.botList, 'i');
  
  // Detect if the userAgent matches a bot
  if (utag_cfg_ovrd.user_agent_regex.test(navigator.userAgent)) {
    utag_cfg_ovrd.isabot = true;
  }
  
  // Prevent loading utag.js if a bot is detected
  if (!utag_cfg_ovrd.isabot) {
    (function(a, b, c, d) {
      a = '//tags.tiqcdn.com/utag/<account>/<profile>/<environment>/utag.js';
      b = document;
      c = 'script';
      d = b.createElement(c);
      d.src = a;
      d.type = 'text/java' + c;
      d.async = true;
      a = b.getElementsByTagName(c)[0];
      a.parentNode.insertBefore(d, a);
    })();
  }
</script>
```

上記のソースコードを以下のように更新します：

1. `utag.js`のディレクトリパス中の`<account>/<profile>/<environment>`を、あなたのTealium iQアカウント情報に置き換えます。詳細については、[code-center](https://docs.tealium.com/code-center/)を参照してください。
1. `utag_cfg_ovrd.botList`の下のボットリストパターンの値を、[下記のボットリストパターン](#bot-list-pattern)またはユーザーエージェントの値と一致するために使用できる他の正規表現パターンのいずれかに置き換えます。
1. サイト上の既存の`utag.js`スクリプトローダータグを更新したバージョンに置き換えます。Tealiumインスタンスの問題や重複を避けるため、ページ上で`utag.js`が1つだけ起動されるようにします。`utag.js`ローダースクリプトについての詳細は、[Universal Tag (utag.js)](https://docs.tealium.com/ja/platforms/javascript/install#universal-tag-utagjs)を参照してください。

## ボットが検出されたときにタグの読み込みを防ぐ

この方法では、PreLoaderにスコープを持つJavaScript Code拡張を使用して、ボットが検出された場合にページ上のすべてのタグの読み込みを停止します。数分で実装することができます。

### 実装手順

1. Preloader-scopedの[javascript-code-basic-extension](https://docs.tealium.com/javascript-code-basic-extension/)を作成します。
1. 次のコードを拡張に貼り付けます：
    ```javascript
    utag_cfg_ovrd = window.utag_cfg_ovrd || {};
    utag_cfg_ovrd.botList = 'UPDATE_BOT_LIST_PATTERN_HERE'.toLowerCase();
    utag_cfg_ovrd.user_agent_regex = new RegExp(utag_cfg_ovrd.botList, 'i');

    // Block utag.js activities if a bot is detected
    if (utag_cfg_ovrd.user_agent_regex.test(navigator.userAgent)) {
    utag_cfg_ovrd.noload = true;
    }
    ```
1. `utag_cfg_ovrd.botList`を含む全行を、[下記のボットリストパターン](#bot-list-pattern)またはユーザーエージェントの値と一致するために使用できる他の正規表現パターンのいずれかに置き換えます。
1. 必要に応じてボットを追加または削除します。
1. 保存して公開します。

## クライアントサイドのボットフィルタリングのテスト方法

クライアントサイドのボットフィルタリングが期待通りに動作していることを確認するために：

1. あなたのウェブサイトに移動します。
1. 開発者ツールのJavaScriptコンソールを開きます。
1. **DevToolsのカスタマイズと制御**アイコンをクリックします。
1. **その他のツール > ネットワーク条件**をクリックします。
1. **ユーザーエージェント**の下で**ブラウザのデフォルトを使用**のチェックを外します。
1. テスト用のカスタムユーザーエージェントを手動で構成します。
1. コンソールで`(utag_cfg_ovrd.user_agent_regex.test(navigator.userAgent))`を入力します：
    * コンソールが`true`を返す場合、ボットの検出は期待通りに動作しています。
    * コンソールエラー**Cannot read property 'test' of undefined**を受け取った場合、コードが動作していないか、存在していない可能性があります。

## ボットリストパターン

提供されるボットリストの正規表現パターンは、両方の方法で同じです。ボットフィルターの適切な機能を確保するために、使用前に最新のボットリストで両方のスクリプトを更新します。これは、下記に提供される更新リスト、またはユーザーエージェントの値と一致するために使用できる他の正規表現パターンのいずれかで、宛先スクリプトの`utag_cfg_ovrd.botList`の値を置き換えることで行うことができます。

ボットリストは、新しいボットパターンを含めるため、または既存のリストを洗練するために定期的な更新が必要となる場合があります。ボットリストを更新するときには：

* JavaScript拡張の`utag_cfg_ovrd.botList`の値が新しいボットリストパターンで更新されていることを確認します。
* ページ上の`utag.js`ローダースクリプトをカスタマイズしている場合、新しいボットリストパターンでそれも更新する必要があります。ローダーファイルが手動で修正されている場合、これには開発リソースが必要となるかもしれません。

あなたが除外するつもりのボットをブロックしていることを確認するために、定期的にボットリストを見直し、監査することをお勧めします。

```javascript
utag_cfg_ovrd.botList = 'bot|google|aolbuild|baidu|bing|msn|duckduckgo|teoma|slurp|yandex|ktxn|360Spider|404checker|404enemy|80legs|Abonti|Aboundex|Acunetix|ADmantX|AfD-Verbotsverfahren|AhrefsBot|AIBOT|AiHitBot|Aipbot|Alexibot|Alligator|AllSubmitter|AlphaBot|Anarchie|Apexoo|archive.org_bot|ASPSeek|Asterias|Attach|autoemailspider|BackDoorBot|Backlink-Ceck|backlink-check|BacklinkCrawler|BackStreet|BackWeb|Badass|Bandit|Barkrowler|BatchFTP|Battleztar\ Bazinga|BBBike|BDCbot|BDFetch|BetaBot|Bigfoot|Bitacle|Blackboard|Black\ Hole|BlackWidow|BLEXBot|Blow|BlowFish|Boardreader|Bolt|BotALot|Brandprotect|Brandwatch|Bubing|Buddy|BuiltBotTough|BuiltWith|Bullseye|BunnySlippers|BuzzSumo|Calculon|CATExplorador|CazoodleBot|CCBot|Cegbfeieh|CheeseBot|CherryPicker|CheTeam|ChinaClaw|Chlooe|Claritybot|Cliqzbot|Cloud\ mapping|coccocbot-web|Cogentbot|cognitiveseo|Collector|com.plumanalytics|Copier|CopyRightCheck|Copyscape|Cosmos|Craftbot|crawler4j|crawler.feedback|crawl.sogou.com|CrazyWebCrawler|Crescent|CSHttp|Curious|Custo|DatabaseDriverMysqli|DataCha0s|DBLBot|demandbase-bot|Demon|Deusu|Devil|Digincore|DigitalPebble|DIIbot|Dirbuster|Disco|Discobot|Discoverybot|DittoSpyder|DnyzBot|DomainAppender|DomainCrawler|DomainSigmaCrawler|DomainStatsBot|Dotbot|Download\ Wonder|Dragonfly|Drip|DTS\ Agent|EasyDL|Ebingbong|eCatch|ECCP/1.0|Ecxi|EirGrabber|EMail\ Siphon|EMail\ Wolf|EroCrawler|evc-batch|Evil|Exabot|Express\ WebPictures|ExtLinksBot|Extractor|ExtractorPro|Extreme\ Picture\ Finder|EyeNetIE|Ezooms|FDM|FemtosearchBot|FHscan|Fimap|Firefox/7.0|FlashGet|Flunky|Foobot|Freeuploader|FrontPage|FyberSpider|Fyrebot|GalaxyBot|Genieo|GermCrawler|Getintent|GetRight|GetWeb|Gigablast|Gigabot|G-i-g-a-b-o-t|Go-Ahead-Got-It|Gotit|GoZilla|Go!Zilla|Grabber|GrabNet|Grafula|GrapeFX|GrapeshotCrawler|GridBot|GT::WWW|Haansoft|HaosouSpider|Harvest|Havij|HEADMasterSEO|Heritrix|Hloader|HMView|HTMLparser|HTTP::Lite|HTTrack|Humanlinks|HybridBot|Iblog|IDBot|Id-search|IlseBot|Image\ Fetch|Image\ Sucker|IndeedBot|Indy\ Library|InfoNaviRobot|InfoTekies|instabid|Intelliseek|InterGET|Internet\ Ninja|InternetSeer|internetVista\ monitor|ips-agent|Iria|IRLbot|Iskanie|IstellaBot|JamesBOT|Jbrofuzz|JennyBot|JetCar|JikeSpider|JOC\ Web\ Spider|Joomla|Jorgee|JustView|Jyxobot|Kenjin\ Spider|Keyword\ Density|Kozmosbot|Lanshanbot|Larbin|LeechFTP|LeechGet|LexiBot|Lftp|LibWeb|Libwhisker|Lightspeedsystems|Likse|Linguee|Linkdexbot|LinkextractorPro|LinkpadBot|LinkScan|LinksManager|LinkWalker|LinqiaMetadataDownloaderBot|LinqiaRSSBot|LinqiaScrapeBot|Lipperhey|Litemage_walker|Lmspider|LNSpiderguy|Ltx71|lwp-request|LWP::Simple|lwp-trivial|Magnet|Mag-Net|magpie-crawler|Mail.RU_Bot|Majestic12|MarkMonitor|MarkWatch|Masscan|Mass\ Downloader|Mata\ Hari|MauiBot|Meanpathbot|Mediatoolkitbot|mediawords|MegaIndex.ru|Metauri|MFC_Tear_Sample|Microsoft\ Data\ Access|Microsoft\ URL\ Control|MIDown\ tool|MIIxpc|Mister\ PiX|MJ12bot|Mojeek|Mr.4x3|MSFrontPage|MSIECrawler|Msrabot|MS\ Web\ Services\ Client\ Protocol|muhstik-scan|Musobot|Name\ Intelligence|Nameprotect|Navroad|NearSite|Needle|Nessus|NetAnts|Netcraft|netEstate\ NE\ Crawler|NetLyzer|NetMechanic|NetSpider|Nettrack|Net\ Vampire|Netvibes|NextGenSearchBot|Nibbler|NICErsPRO|Niki-bot|Nikto|NimbleCrawler|Ninja|Nmap|NPbot|Nutch|oBot|Octopus|Offline\ Explorer|Offline\ Navigator|Openfind|OpenLinkProfiler|Openvas|OpenVAS|OrangeBot|OrangeSpider|OutclicksBot|OutfoxBot|PageAnalyzer|Page\ Analyzer|PageGrabber|page\ scorer|PageScorer|Panscient|Papa\ Foto|Pavuk|pcBrowser|PECL::HTTP|PeoplePal|PHPCrawl|Picscout|Picsearch|PictureFinder|Pimonster|Pi-Monster|Pixray|PleaseCrawl|plumanalytics|Pockey|POE-Component-Client-HTTP|Probethenet|ProPowerBot|ProWebWalker|Psbot|Pump|PxBroker|PyCurl|QueryN\ Metasearch|Quick-Crawler|RankActive|RankActiveLinkBot|RankFlex|RankingBot|RankingBot2|Rankivabot|RankurBot|RealDownload|Reaper|RebelMouse|Recorder|RedesScrapy|ReGet|RepoMonkey|Ripper|RocketCrawler|Rogerbot|s1z.ru|SalesIntelligent|SBIder|ScanAlert|Scanbot|scan.lol|Scrapy|Screaming|ScreenerBot|Searchestate|SearchmetricsBot|Semrush|SemrushBot|SEOkicks|SEOlyticsCrawler|Seomoz|SEOprofiler|seoscanners|SeoSiteCheckup|SEOstats|sexsearcher|Shodan|Siphon|SISTRIX|Sitebeam|SiteExplorer|Siteimprove|SiteLockSpider|SiteSnagger|SiteSucker|Site\ Sucker|Sitevigil|Slackbot-LinkExpanding|SlySearch|SmartDownload|SMTBot|Snake|Snapbot|Snoopy|SocialRankIOBot|sogouspider|Sogou\ web\ spider|Sosospider|Sottopop|SpaceBison|Spammen|SpankBot|Spanner|Spbot|Spinn3r|SputnikBot|Sqlmap|Sqlworm|Sqworm|Steeler|Stripper|Sucker|Sucuri|SuperBot|SuperHTTP|Surfbot|SurveyBot|Suzuran|Swiftbot|sysscan|Szukacz|T0PHackTeam|T8Abot|tAkeOut|Teleport|TeleportPro|Telesoft|Telesphoreo|Telesphorep|The\ Intraformant|TheNomad|TightTwatBot|Titan|Toata|Toweyabot|Tracemyfile|Trendiction|Trendictionbot|trendiction.com|trendiction.de|True_Robot|Turingos|Turnitin|TurnitinBot|TwengaBot|Twice|Typhoeus|UnisterBot|URLy.Warning|URLy\ Warning|Vacuum|Vagabondo|VB\ Project|VCI|VeriCiteCrawler|VidibleScraper|Virusdie|VoidEYE|Voil|Voltron|Wallpapers/3.0|WallpapersHD|WASALive-Bot|WBSearchBot|Webalta|WebAuto|Web\ Auto|WebBandit|WEBDAV|WebEnhancer|WEB\ Enhancer|WebFetch|WEB\ Fetch|WebFuck|Web\ Fuck|WebGo\ IS|WebImageCollector|WebLeacher|WebmasterWorldForumBot|webmeup-crawler|WebPix|Web\ Pix|WebReaper|WebSauger|Web\ Sauger|Webshag|WebsiteExtractor|WebsiteQuester|Website\ Quester|Webster|WebStripper|WebSucker|Web\ Sucker|WebWhacker|WebZIP|WeSEE|Whack|Whacker|Whatweb|Who.is\ Bot|Widow|WinHTTrack|WiseGuys\ Robot|WISENutbot|Wonderbot|Woobot|Wotbox|Wprecon|WPScan|WWW-Collector-E|WWW-Mechanize|WWW::Mechanize|WWWOFFLE|x09Mozilla|x22Mozilla|Xaldon_WebSpider|Xaldon\ WebSpider|Xenu|xpymep1.exe|YandexBot|YoudaoBot|Zade|Zauba|zauba.io|Zermelo|Zeus|zgrab|Zitebot|ZmEu|ZoominfoBot|ZumBot|ZyBorg|Phantom'.toLowerCase();
```