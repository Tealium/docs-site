---
title: Client-side bot filtering
description: This article describes how to filter out bot traffic in client-side environments.
url: https://docs.tealium.com/iq-tag-management/administration/client-side-bot-filtering/
---
Bot filtering on the client-side ensures that only valid, human-generated data is collected, preserving the integrity of your analytics and other data-driven processes.

This article focuses on client-side bot filtering. For details on server-side bot filtering, see [server-side-bot-filtering](https://docs.tealium.com/server-side-bot-filtering/).

## How it works

There are two methods for filtering bots on the client-side using their user agent. 

* Prevent utag from loading when bots are detected.
* Prevent tags from loading when bots are detected.

These methods prevent the loading of tags and the `utag.js` script when bots are detected, ensuring that bot traffic does not interfere with data collection. Both methods preserve vendor tags and Collect tag data integrity (as no `i.gif` requests are sent server-side).

## Prevent utag from loading when bots are detected

This method uses a regular expression (regex) pattern to detect bots and prevent the `utag.js` script from loading. A legitimate crawler, or bot, has a unique user agent that you can use to identify it. By identifying bots through their user agent values, you can control the request for `utag.js` and prevent it from loading. Note that this method requires an implementation outside of Tealium.

### Implementation steps

**Source code that loads the `utag.js`**

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

Update the source code above with the following:

1. Replace `<account>/<profile>/<environment>` in the `utag.js` directory path with your Tealium iQ account information. For more details, see [code-center](https://docs.tealium.com/code-center/).
1. Replace the bot list pattern value under `utag_cfg_ovrd.botList` with either the [bot list pattern below](#bot-list-pattern) or any other regex patterns that can be used to match user agent values.
1. Replace the existing `utag.js` script loader tag on your site with the updated version. Ensure that only one `utag.js` is initiated on the page to avoid any issues or duplication of the Tealium instance. For more information on the `utag.js` loader script, see [Universal Tag (utag.js)](https://docs.tealium.com/platforms/javascript/install#universal-tag-utagjs)

## Prevent tags from loading when bots are detected

This method involves using a JavaScript Code extension scoped to PreLoader to stop all tags from loading on the page if a bot is detected. It can be implemented within minutes.

### Implementation steps

1. Create a Preloader-scoped [javascript-code-basic-extension](https://docs.tealium.com/javascript-code-basic-extension/).
1. Paste the following code into the extension:
    ```javascript
    utag_cfg_ovrd = window.utag_cfg_ovrd || {};
    utag_cfg_ovrd.botList = 'UPDATE_BOT_LIST_PATTERN_HERE'.toLowerCase();
    utag_cfg_ovrd.user_agent_regex = new RegExp(utag_cfg_ovrd.botList, 'i');

    // Block utag.js activities if a bot is detected
    if (utag_cfg_ovrd.user_agent_regex.test(navigator.userAgent)) {
    utag_cfg_ovrd.noload = true;
    }
    ```
1. Replace the entire line containing `utag_cfg_ovrd.botList` with either the [bot list pattern below](#bot-list-pattern) or any other regex patterns that can be used to match user agent values.
1. Add or remove bots if needed.
1. Save and publish.

## How to test client-side bot filtering

To ensure that the client-side bot filtering is working as expected:

1. Navigate to your website.
1. Open the Developer Tools JavaScript console.
1. Click the **Customize and control DevTools** icon.
1. Click **More tools > Network conditions**.
1. Under **User agent**, clear **Use browser default**.
1. Manually set a custom user agent to test with.
1. In the Console, enter `(utag_cfg_ovrd.user_agent_regex.test(navigator.userAgent))`:
    * If the console returns `true`, the bot detection is working as expected.
    * If you receive a console error **Cannot read property 'test' of undefined**, it's either the code is not working or is not present.

## Bot list pattern

The bot list regex pattern provided is the same for both methods. To ensure the proper functionality of your bot filters, update both scripts with the latest bot list before usage. You can do so by replacing the value of `utag_cfg_ovrd.botList` in the destination scripts with the updated list provided below, or any other regex patterns that can be used to match user agent values.

The bot list may require periodic updates to include new bot patterns or to refine the existing list. When updating the bot list:

* Ensure that the `utag_cfg_ovrd.botList` value in the JavaScript extension is updated with the new bot list pattern.
* If you have customized the on-page `utag.js` loader script, you'll also need to update it with the new bot list pattern. This might require development resources if the loader file has been manually modified.

We recommend that you regularly review and audit the bot list to ensure it’s blocking the bots you intend to exclude.

```javascript
utag_cfg_ovrd.botList = 'bot|google|aolbuild|baidu|bing|msn|duckduckgo|teoma|slurp|yandex|ktxn|360Spider|404checker|404enemy|80legs|Abonti|Aboundex|Acunetix|ADmantX|AfD-Verbotsverfahren|AhrefsBot|AIBOT|AiHitBot|Aipbot|Alexibot|Alligator|AllSubmitter|AlphaBot|Anarchie|Apexoo|archive.org_bot|ASPSeek|Asterias|Attach|autoemailspider|BackDoorBot|Backlink-Ceck|backlink-check|BacklinkCrawler|BackStreet|BackWeb|Badass|Bandit|Barkrowler|BatchFTP|Battleztar\ Bazinga|BBBike|BDCbot|BDFetch|BetaBot|Bigfoot|Bitacle|Blackboard|Black\ Hole|BlackWidow|BLEXBot|Blow|BlowFish|Boardreader|Bolt|BotALot|Brandprotect|Brandwatch|Bubing|Buddy|BuiltBotTough|BuiltWith|Bullseye|BunnySlippers|BuzzSumo|Calculon|CATExplorador|CazoodleBot|CCBot|Cegbfeieh|CheeseBot|CherryPicker|CheTeam|ChinaClaw|Chlooe|Claritybot|Cliqzbot|Cloud\ mapping|coccocbot-web|Cogentbot|cognitiveseo|Collector|com.plumanalytics|Copier|CopyRightCheck|Copyscape|Cosmos|Craftbot|crawler4j|crawler.feedback|crawl.sogou.com|CrazyWebCrawler|Crescent|CSHttp|Curious|Custo|DatabaseDriverMysqli|DataCha0s|DBLBot|demandbase-bot|Demon|Deusu|Devil|Digincore|DigitalPebble|DIIbot|Dirbuster|Disco|Discobot|Discoverybot|DittoSpyder|DnyzBot|DomainAppender|DomainCrawler|DomainSigmaCrawler|DomainStatsBot|Dotbot|Download\ Wonder|Dragonfly|Drip|DTS\ Agent|EasyDL|Ebingbong|eCatch|ECCP/1.0|Ecxi|EirGrabber|EMail\ Siphon|EMail\ Wolf|EroCrawler|evc-batch|Evil|Exabot|Express\ WebPictures|ExtLinksBot|Extractor|ExtractorPro|Extreme\ Picture\ Finder|EyeNetIE|Ezooms|FDM|FemtosearchBot|FHscan|Fimap|Firefox/7.0|FlashGet|Flunky|Foobot|Freeuploader|FrontPage|FyberSpider|Fyrebot|GalaxyBot|Genieo|GermCrawler|Getintent|GetRight|GetWeb|Gigablast|Gigabot|G-i-g-a-b-o-t|Go-Ahead-Got-It|Gotit|GoZilla|Go!Zilla|Grabber|GrabNet|Grafula|GrapeFX|GrapeshotCrawler|GridBot|GT::WWW|Haansoft|HaosouSpider|Harvest|Havij|HEADMasterSEO|Heritrix|Hloader|HMView|HTMLparser|HTTP::Lite|HTTrack|Humanlinks|HybridBot|Iblog|IDBot|Id-search|IlseBot|Image\ Fetch|Image\ Sucker|IndeedBot|Indy\ Library|InfoNaviRobot|InfoTekies|instabid|Intelliseek|InterGET|Internet\ Ninja|InternetSeer|internetVista\ monitor|ips-agent|Iria|IRLbot|Iskanie|IstellaBot|JamesBOT|Jbrofuzz|JennyBot|JetCar|JikeSpider|JOC\ Web\ Spider|Joomla|Jorgee|JustView|Jyxobot|Kenjin\ Spider|Keyword\ Density|Kozmosbot|Lanshanbot|Larbin|LeechFTP|LeechGet|LexiBot|Lftp|LibWeb|Libwhisker|Lightspeedsystems|Likse|Linguee|Linkdexbot|LinkextractorPro|LinkpadBot|LinkScan|LinksManager|LinkWalker|LinqiaMetadataDownloaderBot|LinqiaRSSBot|LinqiaScrapeBot|Lipperhey|Litemage_walker|Lmspider|LNSpiderguy|Ltx71|lwp-request|LWP::Simple|lwp-trivial|Magnet|Mag-Net|magpie-crawler|Mail.RU_Bot|Majestic12|MarkMonitor|MarkWatch|Masscan|Mass\ Downloader|Mata\ Hari|MauiBot|Meanpathbot|Mediatoolkitbot|mediawords|MegaIndex.ru|Metauri|MFC_Tear_Sample|Microsoft\ Data\ Access|Microsoft\ URL\ Control|MIDown\ tool|MIIxpc|Mister\ PiX|MJ12bot|Mojeek|Mr.4x3|MSFrontPage|MSIECrawler|Msrabot|MS\ Web\ Services\ Client\ Protocol|muhstik-scan|Musobot|Name\ Intelligence|Nameprotect|Navroad|NearSite|Needle|Nessus|NetAnts|Netcraft|netEstate\ NE\ Crawler|NetLyzer|NetMechanic|NetSpider|Nettrack|Net\ Vampire|Netvibes|NetZIP|NextGenSearchBot|Nibbler|NICErsPRO|Niki-bot|Nikto|NimbleCrawler|Ninja|Nmap|NPbot|Nutch|oBot|Octopus|Offline\ Explorer|Offline\ Navigator|Openfind|OpenLinkProfiler|Openvas|OpenVAS|OrangeBot|OrangeSpider|OutclicksBot|OutfoxBot|PageAnalyzer|Page\ Analyzer|PageGrabber|page\ scorer|PageScorer|Panscient|Papa\ Foto|Pavuk|pcBrowser|PECL::HTTP|PeoplePal|PHPCrawl|Picscout|Picsearch|PictureFinder|Pimonster|Pi-Monster|Pixray|PleaseCrawl|plumanalytics|Pockey|POE-Component-Client-HTTP|Probethenet|ProPowerBot|ProWebWalker|Psbot|Pump|PxBroker|PyCurl|QueryN\ Metasearch|Quick-Crawler|RankActive|RankActiveLinkBot|RankFlex|RankingBot|RankingBot2|Rankivabot|RankurBot|RealDownload|Reaper|RebelMouse|Recorder|RedesScrapy|ReGet|RepoMonkey|Ripper|RocketCrawler|Rogerbot|s1z.ru|SalesIntelligent|SBIder|ScanAlert|Scanbot|scan.lol|Scrapy|Screaming|ScreenerBot|Searchestate|SearchmetricsBot|Semrush|SemrushBot|SEOkicks|SEOlyticsCrawler|Seomoz|SEOprofiler|seoscanners|SeoSiteCheckup|SEOstats|sexsearcher|Shodan|Siphon|SISTRIX|Sitebeam|SiteExplorer|Siteimprove|SiteLockSpider|SiteSnagger|SiteSucker|Site\ Sucker|Sitevigil|Slackbot-LinkExpanding|SlySearch|SmartDownload|SMTBot|Snake|Snapbot|Snoopy|SocialRankIOBot|sogouspider|Sogou\ web\ spider|Sosospider|Sottopop|SpaceBison|Spammen|SpankBot|Spanner|Spbot|Spinn3r|SputnikBot|Sqlmap|Sqlworm|Sqworm|Steeler|Stripper|Sucker|Sucuri|SuperBot|SuperHTTP|Surfbot|SurveyBot|Suzuran|Swiftbot|sysscan|Szukacz|T0PHackTeam|T8Abot|tAkeOut|Teleport|TeleportPro|Telesoft|Telesphoreo|Telesphorep|The\ Intraformant|TheNomad|TightTwatBot|Titan|Toata|Toweyabot|Tracemyfile|Trendiction|Trendictionbot|trendiction.com|trendiction.de|True_Robot|Turingos|Turnitin|TurnitinBot|TwengaBot|Twice|Typhoeus|UnisterBot|URLy.Warning|URLy\ Warning|Vacuum|Vagabondo|VB\ Project|VCI|VeriCiteCrawler|VidibleScraper|Virusdie|VoidEYE|Voil|Voltron|Wallpapers/3.0|WallpapersHD|WASALive-Bot|WBSearchBot|Webalta|WebAuto|Web\ Auto|WebBandit|WebCollage|Web\ Collage|WebCopier|WEBDAV|WebEnhancer|Web\ Enhancer|WebFetch|Web\ Fetch|WebFuck|Web\ Fuck|WebGo\ IS|WebImageCollector|WebLeacher|WebmasterWorldForumBot|webmeup-crawler|WebPix|Web\ Pix|WebReaper|WebSauger|Web\ Sauger|Webshag|WebsiteExtractor|WebsiteQuester|Website\ Quester|Webster|WebStripper|WebSucker|Web\ Sucker|WebWhacker|WebZIP|WeSEE|Whack|Whacker|Whatweb|Who.is\ Bot|Widow|WinHTTrack|WiseGuys\ Robot|WISENutbot|Wonderbot|Woobot|Wotbox|Wprecon|WPScan|WWW-Collector-E|WWW-Mechanize|WWW::Mechanize|WWWOFFLE|x09Mozilla|x22Mozilla|Xaldon_WebSpider|Xaldon\ WebSpider|Xenu|xpymep1.exe|YandexBot|YoudaoBot|Zade|Zauba|zauba.io|Zermelo|Zeus|zgrab|Zitebot|ZmEu|ZoominfoBot|ZumBot|ZyBorg|Phantom'.toLowerCase();
```
