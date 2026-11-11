---
title: プリロード済み属性
description: この記事では、プリロード済み属性について説明します。
url: https://docs.tealium.com/ja/server-side/attributes/preloaded/
---
## 仕組み

利便性を高めるため、Customer Data Platform（CDP）とEvent Streamingには、イベント、訪問、訪問に関する一連のプリロード済み属性が用意されています。各属性は、訪問や訪問ごとに有用な情報を判断するのに役立つ統計情報を収集するよう構成されています。これらの属性には、[Tealium Collectタグ](https://docs.tealium.com/tealium-collect-tag/)から取得される標準イベントデータ以外の追加データは必要ありません。


<blockquote>
プリロード済み属性は変更できませんが、複製して、そのコピーを変更できます。複製には、元の属性のすべてのエンリッチメントとルールが含まれます。
</blockquote>


## 訪問属性

| 訪問属性 | ID | タイプ | 説明 | エンリッチメント |
|-----|-----|-----|-----|-----|
|平均訪問時間（分）| 26 | 数値 | 平均訪問時間（分）。| 訪問終了時に、`Average visit duration in minutes`の比率を、`Total time spent on site in minutes`を`Lifetime visit count`で割った値に構成します。 |
|週あたりの平均訪問回数| 29 | 数値 | 週あたりの平均訪問回数。| 新規訪問時に、`Weeks since first visit`が`1`以上の場合、`Average visits per week`の比率を、`Lifetime visit count`を`Weeks since first visit`で割った値に構成します。 |
|ファン| 30 | バッジ | 訪問が3回以上訪問しており、参照元経由の訪問よりも直接訪問の回数が多いことを示します。| 新規訪問時に、`Total direct visits`が`Total referred visits`より大きい場合、訪問に`Fan`バッジを割り当てます。 |
|初回訪問| 23 | 日付 | 初回訪問の日付。| 新規訪問の場合、`First visit_copy`を`Last event timestamp`に構成します。 |
|頻繁に訪問する訪問| 31 | バッジ | 訪問が週平均2回以上訪問していることを示します。| 新規訪問時に、`Average visits per week`が`2`未満の場合は訪問から`Frequent visitor`バッジを削除し、`Average visits per week`が`2`以上の場合は訪問に`Frequent visitor`を割り当てます。 |
|直近イベントのURL | 17 | 文字列 | 訪問の直近イベントのURL。 | 任意のイベント発生時に、文字列`Last event URL`を`Current URL`に構成します。 |
|直近の訪問 | 24 | 日付 | 直近の訪問日。| 訪問終了時に、`Last visit`を直近イベントのタイムスタンプに構成します。 |
|これまでに使用したブラウザータイプ| 57 | 集計 | 各ブラウザータイプが使用された回数の集計。| 訪問終了時に、`Active browser types`に存在する場合、集計`Lifetime browser types used`のすべての値を`1`ずつ増加させます。 |
|これまでに使用したブラウザータイプ（お気に入り）| 56 | 文字列 | 「これまでに使用したブラウザータイプ」属性の中で最もよく使用された項目。| 「これまでに使用したブラウザータイプ」から自動生成されます。 |
|これまでに使用したブラウザーバージョン | 63 | 集計 | 使用されたブラウザーバージョンの集計。| 訪問終了時に、`Active browser versions`に存在する場合、集計`Lifetime browser versions used`のすべての値を`1`ずつ増加させます。 |
|これまでに使用したブラウザーバージョン（お気に入り）| 62 | 文字列 | 「これまでに使用したブラウザーバージョン」属性の中で最もよく使用された項目。| 「これまでに使用したブラウザーバージョン」から自動生成されます。|
|これまでに使用したデバイス| 55 | 集計 | 使用されたデバイスの集計。| 訪問終了時に、`Active devices`に存在する場合、集計`Lifetime devices used`のすべての値を`1`ずつ増加させます。 |
|これまでに使用したデバイス（お気に入り） | 54 | 文字列 | 「これまでに使用したデバイス」属性の中で最もよく使用された項目。| 「これまでに使用したデバイス」から自動生成されます。|
|これまでのイベント数 | 22 | 数値 | ユーザーによってトリガーされたイベントの合計数。| 任意のイベント発生時に、数値`Lifetime event count`を`1`増加させます。 |
|これまでに使用したオペレーティングシステム| 59 | 集計 | 使用されたオペレーティングシステムの集計。| 訪問終了時に、`Active operating systems`に存在する場合、集計`Lifetime operating systems used`のすべての値を`1`ずつ増加させます。 |
|これまでに使用したオペレーティングシステム（お気に入り） | 58 | 文字列 | 「これまでに使用したオペレーティングシステム」属性の中で最もよく使用された項目。| 「これまでに使用したオペレーティングシステム」から自動生成されます。 |
|これまでに使用したプラットフォーム | 61 | 集計 | 使用されたプラットフォームの集計。| 訪問終了時に、`Active platforms`に存在する場合、集計`Lifetime platforms used`のすべての値を`1`ずつ増加させます。 |
|これまでに使用したプラットフォーム（お気に入り） | 60 | 文字列 | 「これまでに使用したプラットフォーム」属性の中で最もよく使用された項目。| 「これまでに使用したプラットフォーム」から自動生成されます。|
|これまでの訪問回数 | 21 | 数値 | ユーザーがサイトを訪問した合計回数。| <ul><li>訪問終了時に、`Average visit duration in minutes`の比率を、`Total time spent on site in minutes`を`Lifetime visit count`で割った値に構成します。</li><li>新規訪問時に、`Weeks since first visit`が`1`以上の場合、`Average visits per week`の比率を、`Lifetime visit count`を`Weeks since first visit`で割った値に構成します。</li></ul> |
|再訪問| 27 | ブール値 | 訪問が再訪問であることを示します。| 新規訪問時に、`Lifetime visit count`が`1`より大きい場合、`Returning visitor`を`true`に構成します。 |
|直接訪問の合計回数| 15 | 数値 | 直接訪問の合計回数。| 新規訪問時に、`Referring URL`が空であるか、`Referring URL`が`Current URL`と等しい場合、数値`Total direct visits`を`1`増加させます。 |
|参照元経由の訪問の合計回数 | 16 | 数値 | 参照元経由の訪問の合計回数。| 新規訪問時に、`Referring URL`が空ではなく、かつ`Referring URL`が`Current URL`と等しくない場合、数値`Total referred visits`を`1`増加させます。|
|サイトで費やした合計時間（分）| 25 | 数値 | ユーザーによるすべての訪問時間の合計。| 訪問終了時に、数値`Total time spent on site in minutes`を`Visit duration `の分だけ増加させます。 |
|バッジなし| 32 | バッジ | 訪問にバッジが割り当てられていないことを示します。 | 新規訪問の場合、訪問に`Unbadged`バッジを割り当てます。 |
|初回訪問からの週数| 28 | 数値 | 初回訪問から経過した週数。| 新規訪問時に、`Weeks since first visit`が`1`以上の場合、`Average visits per week`の比率を、`Lifetime visit count`を`Weeks since first visit`で割った値に構成します。 |
## 訪問属性

| 訪問属性 | ID | 型 | 説明 | エンリッチメント |
|-----|-----|-----|-----|-----|
|アクティブなブラウザーの種類 |44 | 文字列 | 訪問が現在使用しているブラウザー。 | <ul><li>任意のイベントで、`User Agent` に `Firefox`、`Safari`、`MSIE`、`Edg`、Opera のいずれも含まれていない場合、文字列 `Active browser version` を `Active browser type` に構成します。</li><li>任意のイベントで `User Agent` が `Chrome` の場合、文字列 `Active browser version` を `Active browser type` に構成します。</li><li>任意のイベントで `User Agent` が `Firefox` の場合、文字列 `Active browser version` を `Active browser type` に構成します。</li><li>任意のイベントで `User Agent` が `Opera` の場合、文字列 `Active browser version` を `Active browser type` に構成します。</li><li>任意のイベントで、文字列セット `Active browser types` に `Active browser type` を追加します。</li></ul> |
|アクティブなブラウザーの種類 |49 |文字列セット | この訪問で使用されたブラウザーの種類を重複排除したリスト。 | 訪問終了時に `Active browser types when visit ended.` に含まれている場合、集計 `Lifetime browser types used` のすべての該当値を `1` ずつ増加させます。 |
|アクティブなブラウザーのバージョン |48 | 文字列 | 訪問が現在使用しているブラウザーのバージョン。 | 任意のイベントで、文字列セット `Active browser versions` に `Active browser version` を追加します。 |
|アクティブなブラウザーのバージョン |53 | 文字列セット | この訪問で使用されたブラウザーのバージョンを重複排除したリスト。 | 訪問終了時に `Active browser versions` に含まれている場合、集計 `Lifetime browser versions used` のすべての該当値を `1` ずつ増加させます。 |
|アクティブなデバイス |46 | 文字列 | 訪問が現在使用しているデバイス。 | 任意の訪問で、文字列セット `Active devices` に `Active device` を追加します。 |
|アクティブなデバイス |51 | 文字列セット | この訪問で使用されたデバイスを重複排除したリスト。 | 訪問終了時に `Active devices` に含まれている場合、集計 `Lifetime devices used` のすべての該当値を `1` ずつ増加させます。 |
|アクティブなオペレーティングシステム |45 | 文字列 | 訪問が現在使用しているオペレーティングシステム。 | 任意のイベントで、文字列セット `Active operating systems` に `Active operating system` を追加します。 |
|アクティブなオペレーティングシステム |50 | 文字列セット | オペレーティングシステムを重複排除したリスト。 | 訪問終了時に `Active operating systems` に含まれている場合、集計 `Lifetime operating systems used` のすべての該当値を `1` ずつ増加させます。 |
|アクティブなプラットフォーム |47 | 文字列 | 訪問が現在使用しているプラットフォーム。 | 任意のイベントで、文字列セット `Active platforms` に `Active platform` を追加します。 |
|アクティブなプラットフォーム |52 | 文字列セット | アクティブなプラットフォームを重複排除したリスト。 | 訪問終了時に `Active platforms` に含まれている場合、集計 `Lifetime platforms used` のすべての該当値を `1` ずつ増加させます。 |
|直接訪問 |14 | ブール値 | ユーザーがサイトに直接移動したことを示します。 | 新規訪問時に `Referring URL` が空であるか、`Referring URL` が `Current URL` と等しい場合、ブール値 `Direct visit` を `true` に構成します。 |
|入口URL |5 | 文字列 | 最初に訪問したページのURL。 | 新規訪問時に文字列 `Entry URL` を `Current URL` に構成します。 |
|イベント数 |7 | 数値 | この訪問におけるイベントの合計数。 | 任意のイベントで、数値 `Event count` を `1` 増加させます。 |
|離脱URL |6 | 文字列 | 最後に訪問したページのURL。 | 訪問終了時に文字列 `Exit URL` を `Current URL` に構成します。 |
|参照元からの訪問 |13 | ブール値 | ユーザーが別のサイトから参照されたことを示します。 | 新規訪問時に `Referring URL` が空ではなく、かつ `Referring URL` が `Current URL` と等しくない場合、ブール値 `Referred visit` を `true` に構成します。 |
|訪問時間 |12 | 数値 | この訪問の継続時間。 | 訪問終了時に、数値 `Total time spent on site in minutes` を `Visit duration` の値だけ増加させます。 |
|訪問終了日時 |11 | 日付 | この訪問の終了日時。 | 任意のイベントで、数値 `Visit duration` を `Visit end` と `Visit start` の差（分単位）に構成します。 |
|訪問開始日時 |10 | 日付 | この訪問の開始日時。 | 任意のイベントで、数値 `Visit duration` を `Visit end` と `Visit start` の差（分単位）に構成します。 |

## イベント属性

| イベント属性 | ID | 型 | 説明 | エンリッチメント |
|-----|-----|-----|-----|-----|
|クライアントIP |74 |文字列 |訪問のIPv4アドレス。 | |
|クライアントIPv6 |83 |文字列 |訪問のIPv6アドレス。訪問がIPv6アドレスを持ち、そのネットワークインフラストラクチャがアドレスを送信できる必要があります。詳細については、[IPv6のサポート](#support-for-ipv6)を参照してください。 | |
|現在のURL |4 |文字列 |現在のページのURL。 | <ul><li>新規訪問時に文字列 `Entry URL` を `Current URL` に構成します。</li><li>訪問終了時に文字列 `Exit URL` を `Current URL` に構成します。</li><li>任意のイベントで文字列 `Last event URL` を `Current URL` に構成します。</li></ul> |
|ドメイン |35 |文字列 |現在のページのドメイン。 | |
|event_name |64 |文字列 |この属性は非推奨です。代わりに `tealium_event` を使用してください。 |
|最終イベントのタイムスタンプ |8 |文字列 |最終イベントのタイムスタンプ。 | <ul><li>新規訪問時に日付 `Visit start` を `Last event timestamp` に構成します。</li><li>任意のイベントで日付 `Visit end` を `Last event timestamp` に構成します。</li><li>新規訪問の場合、日付 `First visit` を `Last event timestamp` に構成します。</li><li>訪問終了時に日付 `Last visit` を `Last event timestamp` に構成します。</li></ul> |
|ページタイトル |38 |文字列 |現在のページのタイトル。 | |
|パス名 |36 |文字列 |現在のページのパス名。 | |
|platform |40 |文字列 |クライアントのプラットフォーム。 | |
|クエリ文字列 |37 |文字列 |現在のページのクエリ文字列。 | |
|参照元URL |3 |文字列 |前のページのURL。 | |
|tealium_account |66 |文字列 |アカウント名。 | |
|tealium_datasource |70 |文字列 |データソースキー。 | |
|tealium_environment |67 |文字列 |パブリッシュ環境。 | |
|tealium_event |75 |文字列 |Tealiumイベント名（`view` または `link`）。 | |
|tealium_event_type |78 |文字列 |ディスパッチされるTealiumイベントの種類（`view` または `event`）。 | |
|tealium_firstparty_visitor_id |76 |文字列 |ファーストパーティCookieによって提供される訪問ID。 | |
|tealium_library_name |68 |文字列 |ライブラリ名。 | |
|tealium_library_version |69 |文字列 |ライブラリのバージョン。 | |
|tealium_profile |79 |文字列 |アカウントプロファイル。 | |
|tealium_random |65 |数値 |この値は、プラットフォームがイベントごとに生成した乱数です。想定される値は16桁の数字です。16桁未満の場合は、先頭にゼロがエンリッチメントされます。 | |
|tealium_session_id |71 |数値 |この値は、最初のページビュー、イベント、またはライブラリの起動が完了した時点のエポックタイムスタンプ（ミリ秒単位）です。Web上で30分間アクティビティがない場合、この値はリセットされます。 | |
|tealium_thirdparty_visitor_id |77 |文字列 |サードパーティCookieによって提供される訪問ID。 | |
|tealium_timestamp_epoch |73 |数値 |この値は、イベントが発生した時刻（秒単位）です。イベントがキューに入れられた場合、この値はイベントが最初に発生した時刻になります。 | |
|tealium_visitor_id |72 |文字列 |この値は生成されたUUIDであり、CDPでは大文字と小文字が区別されます。この値は以前、`vdata` 呼び出しで `tealium_vid` と呼ばれていました。 | |
|ユーザーエージェント |2 |文字列 |ユーザーエージェント文字列。 | |
### IPv6 のサポート

このセクションでは、IPv6 をサポートするコンポーネントと、IPv6 アドレスを利用できない場合にフォールバックを構成する方法について説明します。

**タグのホスト名**

| ホスト名 | IPv4 サポート | IPv6 サポート |
|----------|--------------|--------------|
| `tags.tiqcdn.com` | ✓ | ✓ |
| `tags.tiqcdn.cn` | ✓ | ✓ |
| `tags-eu.tiqcdn.com` | ✓ | ✗ |

**ファーストパーティドメイン**

ファーストパーティドメインでの IPv6 サポートは、構成が作成された時期によって異なります。

* ファーストパーティドメイン機能のリリース前に作成された構成は、IPv6 をサポートします。
* 機能のリリース後に製品 UI から作成された構成は、デフォルトでは IPv6 をサポートしません。IPv6 を有効にするには、ドメインの A レコードと同じディストリビューションを参照する AAAA DNS レコードを追加します。

**その他のコンポーネント**

以下のコンポーネントは IPv6 をサポートしていません。

* Tealium Collect タグおよび Collect HTTP API（`collect.tealiumiq.com` および `collect-<region>.tealiumiq.com`）
* ファーストパーティ Collect ドメイン
* Tealium v1、v2、v3 API（`platform.tealiumapis.com`）
* コネクタおよび外部ファイルのインポート

IPv6 アドレスを利用できない場合に、IPv4 アドレスをフォールバックとして使用する属性を作成するには、ナレッジベースの記事「[IPv6 使用時のフォールバックの構成](https://support.tealiumiq.com/en/support/solutions/articles/36000521207)」を参照してください。

## 例

以下の例は、プリロード済み属性の使用方法を示しています。

* **Frequent visitor** バッジを使用してオーディエンスを作成し、コネクタでそのオーディエンスにアクションを実行して、「いつもご利用いただきありがとうございます」というメールを該当する訪問に送信します。
* **Lifetime operating systems used (favorite)** 属性を使用して、ページ上の特定のダウンロード項目の配置を変更し、関連性の高いアプリが最初に表示されるようにします。
* **Total Direct Visits** と **Total Referred Visits** を使用して、訪問の直接訪問数と参照元経由の訪問数の比率を計算し、各訪問または訪問について把握します。