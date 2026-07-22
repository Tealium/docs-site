---
title: データレイヤー
description: AMPライブラリからのデータレイヤー変数について学びます。
url: https://docs.tealium.com/ja/platforms/amp/data-layer/
---以下のパラメータはTealium AMPライブラリによって生成されます。これらの変数はライブラリからの各トラッキングコールに自動的に含まれ、Tealium Customer Data Hubの構成で使用されます。

以下の表では、一部の変数はページビュー/イベントトラッキングの両方に使用され、一部はそれぞれにのみ使用されます。


<blockquote>
ページビュートラッキングの場合、デフォルトのイベントは`screen_view`です。イベントトラッキングの場合、`tealium_event`変数を使用してイベント名を指定します。
</blockquote>


| パラメータ | 説明 | ページトラッキング | イベントトラッキング | 例 |
| :-- | :-- | :-- | :-- | :-- |
| `amp_hostname` | AMPホスト名 | &#10004; | &#10004; | `example.com` |
| `amp_request_count` | AMPリクエスト数 |  &#10004; | &#10004; |`1` |
| `amp_version` | AMPバージョン番号 |  &#10004; | &#10004; | `1907022322580` |
| `ampdoc_url` | AMPドキュメントURL |  &#10004; | &#10004; | `http://example.com/path/to/file.html` |
| `canonical_hostname` | 正規ホスト名 | &#10004; | &#10004; | `example.ampproject.org` |
| `content_load_ms` | コンテンツのロード時間（ミリ秒） | &#10004; |  | `66` |
| `domain` | URLの完全なドメイン名 | &#10004; | &#10004; | `example.com` |
| `lang` | 言語コード | &#10004; | &#10004; | `en-us` |
| `page_view_id` | ページビューID番号 | &#10004; | | `769` |
| `pathname` | URLのパス、クエリパラメータとドメインを除く | &#10004; | &#10004; | `/path/to/file.html` |
| `referrer` | ファイル名を除いたURLパス | &#10004; | | `http://example.com/path/to/ `|
| `screen_size` | 画面解像度の高さx幅（ピクセル） | &#10004; | | `2560x1440` |
| `scroll_x` | 水平スクロール値（x軸） | | &#10004; | `0` |
| `scroll_y` | 垂直スクロール値（y軸） | | &#10004; | `0` |
| `tealium_visitor_id` | 生成されたuuid（大文字小文字を区別） | &#10004; | &#10004; | `amp-ABc1dEF2gH3IJK4lmn5OPz` |
| `timestamp` | エポックタイムスタンプ（`vars`ブロックで上書き）| &#10004; | &#10004; | `1563305241134` |
| `title` | AMPドキュメントのタイトル（`vars`ブロックで上書き） | &#10004; | &#10004; | `Hello, AMP` |
| `tz` | タイムゾーン | &#10004; | &#10004; | `420` |
| `url` | ページの完全なURL | &#10004; | &#10004; | `http://example.com/path/file.html` |
| `viewport_height` | ブラウザビューポートの高さ（ピクセル） | &#10004; | &#10004; | `1417` |
| `viewport_width` | ブラウザビューポートの幅（ピクセル） | &#10004; | &#10004; | `2560` |
