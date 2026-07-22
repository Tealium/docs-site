---
title: Tealiumのクッキー
description: この記事では、Tealium iQタグ管理が使用するクッキーの概要と、追加のクッキーを作成および変更するさまざまな方法について説明します。
url: https://docs.tealium.com/ja/iq-tag-management/data-layer/cookies/
---
## 組み込みクッキー

Tealium Universal Tag（`utag.js`）は、内部使用のためにいくつかのファーストパーティクッキーを維持します。これらの変数は、[Tealium Built-In Data Bundle](https://docs.tealium.com/data-bundles/)を使用してデータレイヤーに追加することができます。

以下の表は、`utag.js`が作成および維持するクッキーをリストしています：

| クッキー変数    | 説明 |
|------------------- | ----------- |
| `utag_main_ses_id`  | セッション開始のUnix/Epochタイムスタンプ（ミリ秒単位）。|
| `utag_main_v_id`    | データプライバシーと同意ルールを遵守するための一意で部分的にランダムな識別子。バージョン4.50以降では、デフォルトでは構成されません。Tealium Collectタグが必要に応じてこのクッキーを書き込みます。詳細については、[`utag.js`バージョン4.50](https://docs.tealium.com/platforms/javascript/version-4-50/)を参照してください。|
| `utag_main__st`     | セッションタイムアウトのUnix/Epochタイムスタンプ（ミリ秒単位）。新しいイベントが発生するたびに値が更新されます。|
| `utag_main__se`| 現在のセッション中のイベント数。 |
| `utag_main__ss`     | ページがセッションの最初のものであるかどうかを示すブール値。`1`の値は、現在のページがセッションで最初に表示されたページであることを意味し、`0`の値は、現在のページがセッションで最初に表示されたページではないことを意味します。|
| `utag_main__pn`     | 現在のセッション中に表示されたページ数。|
| `utag_main__sn`     | この訪問のセッション数。|

### バージョン4.50以降

[`utag.js`のバージョン4.50以降](https://docs.tealium.com/platforms/javascript/version-4-50/)は、`utag_main_`プレフィックスを使用してスタンドアロンのクッキーを作成および管理します。これは、`utag.js`が各値を`utag_main_`で始まるクッキー名を持つクッキーに個別に保存することを意味します。

ブラウザのコンソールでは、これらの個別のクッキーは次のように表示されます：

![](https://docs.tealium.com/images/iq-tag-management/data-layer/utag-separate-cookies.png)

このデフォルトの動作を上書きし、`utag.js`にすべての`utag_main`クッキーを単一のマルチバリュークッキーに保存するように強制するには、[`split_cookie`](https://docs.tealium.com/platforms/javascript/settings/#split_cookie)構成を使用します。デフォルトのスタンドアロンクッキー動作を使用する場合、[`split_cookie_allowlist`](https://docs.tealium.com/platforms/javascript/settings/#split_cookie_allowlist)構成を使用して構成できるクッキーを制限します。


<blockquote>
`utag.js`のバージョン4.50から、`utag_main`の`v_id`変数は、データプライバシーと同意目的を遵守するためにTealium Collectタグによって構成されます。この動作を上書きして、すべての訪問に対してこのクッキーを生成するには、[`always_set_v_id`](https://docs.tealium.com/platforms/javascript/settings/#always_set_v_id)構成を有効にします。
</blockquote>


### バージョン4.49以前

`utag.js`のバージョン4.49以前は、いくつかの区切られたキー値ペアを持つ単一のマルチバリュークッキーである`utag_main`を作成および維持します。

ブラウザのコンソールでは、この単一のマルチバリュークッキーは次のように表示されます：

![](https://docs.tealium.com/images/iq-tag-management/data-layer/utag-multivalue-cookie.png)

## クッキー関数

`utag.js`は、クッキーの読み取りと書き込みを容易にする2つのクッキー関数を使用します。詳細については、[cookie functions](https://docs.tealium.com/platforms/javascript/api/cookie-functions/)を参照してください。

構成できるクッキーを制限するには、[`split_cookie_allowlist`](https://docs.tealium.com/platforms/javascript/settings/#split_cookie_allowlist)構成を使用します。この構成は、タグとカスタム関数が未宣言のクッキーを構成しないようにします。また、[`utag.loader.SC`](https://docs.tealium.com/platforms/javascript/api/cookie-functions/#utagloadersc)が未宣言のクッキーを書き込むのを防ぎます。

## 拡張機能からのクッキー

### データ値の永続化

**Persist Data Value**拡張機能は、iQタグ管理インターフェースからクッキーを構成するために使用できます。クッキーは、`utag_main`プレフィックスの有無に関係なく構成できます。

詳細については、[Persist Data Value extension](https://docs.tealium.com/persist-data-value-extension/)を参照してください。

### Split Segmentation

**Split Segmentation**拡張機能は、通常はA/Bテストのために訪問のセグメントを作成するために使用されます。拡張機能は、セグメント名をクッキーに保存します。

詳細については、[Split Segmentation extension](https://docs.tealium.com/split-segmentation-extension/)を参照してください。

### Privacy Manager

**Privacy Manager**拡張機能は、`OPTOUTMULTI`という名前のクッキーを使用して、訪問のプライバシー構成を次回のサイト訪問時に保存します。

詳細については、[Privacy Manager extension](https://docs.tealium.com/privacy-manager-extension/)を参照してください。

## タグからのクッキー

タグマーケットプレイスの一部のタグは、匿名識別子やその他の情報を永続化するために[cookie functions](https://docs.tealium.com/platforms/javascript/api/cookie-functions/)を使用します。

### Tealium Collectタグのクッキー

Tealium Collectタグは、以下のクッキーを生成します：

| クッキー変数    | 説明 |
|------------------- | ----------- |
| `utag_main_v_id`    | データプライバシーと同意ルールを遵守するための一意で部分的にランダムな識別子。バージョン4.50以降では、デフォルトでは構成されません。Tealium Collectタグが必要に応じてこのクッキーを書き込みます。詳細については、[`utag.js`リリースノートバージョン4.50](https://docs.tealium.com/platforms/javascript/version-4-50/)を参照してください。|
|`utag_main_dc_group`|  サンプルサイズ構成を使用して、どのイベントがサンプリングされるかを決定するためのランダムな数値。 |
| `utag_main_dc_visit` | Tealium Collectタグが発火したセッション数。|
| `utag_main_dc_event` | Tealium Collectタグが発火したイベント数。|
| `utag_main_dc_region` | 訪問セッションが保存されているAudienceStream地域、HTTPレスポンスヘッダーから収集。このクッキーは、[data layer enrichment](https://docs.tealium.com/data-layer-enrichment/)のエンドポイントを決定するために使用されます。 |

詳細については、[Tealium Collect tag](https://docs.tealium.com/tealium-collect-tag/)を参照してください。

### サードパーティタグからのクッキー

一部のサードパーティタグは、識別子やその他のデータを保存するクッキーを生成します。

これらのクッキーはTealiumによって制御されず、[`split_cookie_allowlist`](https://docs.tealium.com/platforms/javascript/settings/#split_cookie_allowlist)構成やTealium iQタグ管理の他の機能によって制限されません。

## Consent Managerからのクッキー

**Consent Manager**は、`CONSENTMGR`という名前のクッキーを使用して、訪問の同意構成を保存します。

[consent management](https://docs.tealium.com/about-consent-management/)について詳しく学びましょう。

`CONSENTMGR`クッキーの名前を変更するには、まず`cmGeneral`テンプレートのバージョン2.0.1以降を使用していることを確認し、次に以下のコードを持つJavaScript Code拡張機能を**All Tags - Before Load Rules**にスコープ指定します：

```js
utag.gdpr.cmcookiens = 'NEW_COOKIE_NAME';
```


<blockquote>
同意クッキーの保持期間を変更するには、[`consentPeriod`](https://docs.tealium.com/platforms/javascript/settings/#consentperiod)構成を使用します。
</blockquote>


## Web Companionからのクッキー

[Web Companion](https://docs.tealium.com/web-companion/)は、最後にサイトを訪れたときに表示していた公開環境（Prod、QA、Dev、またはCustom）を保存するためにクッキーを使用します。サイトのデフォルトの公開環境を表示してもクッキーは構成されません。

最後に表示した公開環境は、次のクッキーに保存されます。ここで、`{account}`と`{profile}`はあなたのアカウントとプロファイルに置き換えられます：`utag_env_{account}_{profile}`

ブラウザのクッキーをクリアすると、Web Companionは表示していた公開環境を保存せず、表示する環境を再選択する必要があります。
