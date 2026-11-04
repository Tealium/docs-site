---
title: 構成
description: `utag.js` の動作を調整するために利用できる構成について説明します。
url: https://docs.tealium.com/ja/platforms/javascript/settings/
---
## 仕組み

`utag.js` の多くの動作は、`utag.cfg` オブジェクトの構成によって制御されます。これらの構成で制御されるデフォルトの動作は、`utag_cfg_ovrd` という新しいオブジェクトを使用して上書きできます。このオブジェクトを使用するには、`utag.js` を読み込む前のページコード内、またはスコープを **Pre Loader** に構成した [JavaScript Code Extension](https://docs.tealium.com/advanced-javascript-code-extension/) 内で、次のように構成します。

```js
window.utag_cfg_ovrd = window.utag_cfg_ovrd || {};
```

## オプション一覧

利用可能な構成を次の表にまとめます。

| 構成 | 説明 |
| ------- | ----------- |
| [`always_set_v_id`](#always_set_v_id)| `utag_main_v_id` Cookie、または `utag_main` の `v_id` コンポーネントを構成します。デフォルト：`false` |
| [`cmcookiens`](#cmcookiens) | 同意管理Cookieの名前です。 |
| [`consentPeriod`](#consentperiod) | ユーザーの同意構成を保持する日数を構成します。 |
| [`disable_tealium_attribute_override`](#disable_tealium_attribute_override) | システム定義属性 `tealium_*` が受信データによって上書きされないようにします。 |
| [`dom_complete`](#dom_complete) | DOM Complete（load）イベントまでタグを遅延させます。 |
| [`domain`](#domain) | Cookieの構成に使用するドメインを上書きします。 |
| [`gdprDLRef`](#gdprdlref) | 同意マネージャーで使用する言語構成を格納するデータレイヤー変数の名前を指定します。 |
| [`ignoreLocalStorage`](#ignorelocalstorage) | ローカル保存変数をデータレイヤーに追加しません。 |
| [`ignoreSessionStorage`](#ignoresessionstorage) | セッション保存変数をデータレイヤーに追加しません。 |
| [`load_rules_ajax`](#load_rules_ajax) | ページ読み込み後のロードルールを無効にします（レガシー）。 |
| [`load_rules_at_wait`](#load_rules_at_wait) | 拡張機能の実行後にロードルールを実行します（レガシー）。 |
| [`lowermeta`](#lowermeta)| メタタグの名前と値を小文字に変換します（レガシー）。 |
| [`lowerqp`](#lowerqp)| クエリ文字列パラメータの名前と値を小文字に変換します（レガシー）。 |
| [`noload`](#noload) | すべての機能を無効にします。 |
| [`noview`](#noview) | 初回ページ読み込み時の自動トラッキング呼び出しを無効にします。 |
| [`nocookie`](#nocookie) | `utag_main` Cookieを無効にします。 |
| [`noconsole`](#noconsole) | `utag.DB` のコンソール出力を抑制します。 |
| [`nonblocking_tags`](#nonblocking_tags) | すべてのタグをノンブロッキングにして、極端なケースでのパフォーマンスと Interaction to Next Paint（INP）スコアを改善します。デフォルト：`false`。 |
| [`path`](#path) | パブリッシュパスを指定します。 |
| [`readywait`](#readywait) | ブラウザの DOM Ready イベントまで処理を停止します。 |
| [`secure_cookie`](#secure_cookie) | [Persist Data Values拡張機能](https://docs.tealium.com/persist-data-value-extension/)および [`utag.loader.SC`](https://docs.tealium.com/ja/platforms/javascript/api/cookie-functions/#utagloadersc) メソッドによって構成されるすべての `utag_main` Cookieについて、属性文字列を `secure` に構成します。 |
| [`session_timeout`](#session_timeout)| セッションの有効期限（ミリ秒単位）を構成します。 |
| [`split_cookie`](#split_cookie)| `utag_main` Cookieを独立したCookieに分割します。デフォルト：`true` |
| [`split_cookie_allowlist`](#split_cookie_allowlist)| 許可された `utag_main` サブCookieまたは独立したCookieの配列です。 |
| [`suppress_before_load_rules_with_uids`](#suppress_before_load_rules_with_uids) | UIDでタグをトラッキングするときに、スコープが **Before Load Rules** に構成された拡張機能をスキップするレガシー動作を強制します。デフォルト：`false`。 |
| [`waittimer`](#waittimer) | タグを読み込む前の遅延時間（ミリ秒単位）を構成します。 |

### `always_set_v_id`

**`utag.js` に `utag_main_v_id` Cookie、または `utag_main` の `v_id` コンポーネントを強制的に構成させる**  
（[`utag.js` 4.50](https://docs.tealium.com/ja/release-notes/?filter=tealium-universal-tag#tealium-universal-tag-2023-09-01) で追加）  
`utag_main` の `v_id` 変数は、データプライバシーおよび同意の目的に準拠するよう、Tealium Collectタグによって構成されます。この構成を `true` にすると、`utag.js` はすべての訪問に対してこのCookieを強制的に構成します。（デフォルト：`false`）

```js
window.utag_cfg_ovrd.always_set_v_id = true;
```

### `cmcookiens`

**同意管理Cookieの名前**  
同意管理Cookieの名前をカスタマイズします。同じドメイン名で複数のプロファイルを使用している場合は、Cookie間の競合や潜在的なデータ漏洩を防ぐため、各プロファイルに一意の同意管理Cookie名を指定してください。

```js
window.utag_cfg_ovrd.cmcookiens = "CONSENTMGR_NL-CMB-CG1";
```

### `consentPeriod`

**同意構成の保持期間**  
GDPRおよびCCPAの同意ステータスを保持する日数を構成します。組み込みの有効期限は、GDPRでは365日、CCPAでは395日です。

```js
window.utag_cfg_ovrd.consentPeriod = 60;
```

### `disable_tealium_attribute_override`

**システム定義属性の上書きを防止する**  

（[`utag.js` 4.54](https://docs.tealium.com/ja/release-notes/?filter=tealium-universal-tag#tealium-universal-tag-2025-10-22) で追加）

この構成を `true` にすると、`tealium_visitor_id` と `tealium_event` を除き、`tealium_` で始まるシステム定義属性が受信データによって上書きされるのを防ぎます。  

`utag.js` バージョン4.52および4.53では、この保護がデフォルトで有効になっていたため、一部のモバイルWebView環境で問題が発生していました。バージョン4.54では、この保護はオプトイン方式になり、完全に制御できるようになりました。

（デフォルト：`false`）

```js
window.utag_cfg_ovrd.disable_tealium_attribute_override = true;
```

### `dom_complete`

**DOM Complete（load）ブラウザイベントまでタグを遅延させる**  
DOM Readyではなく、[ドキュメントのloadイベント](https://developer.mozilla.org/en-US/docs/Web/Events/load)でタグを読み込みます。これにより、スコープがDOM Readyに構成された拡張機能も遅延します。（デフォルト：`false`）

```js
window.utag_cfg_ovrd.dom_complete = true;
```

### `domain`

**Cookieドメインを上書きする**  
`utag_main` Cookieを構成するドメインを指定します。Cookieを受け付けないルートドメイン上のサイトで役立ちます。たとえば、`amazonaws.com` です。（デフォルト：`location.hostname` のトップレベルドメイン）

```js
window.utag_cfg_ovrd.domain = "mysite.amazonaws.com";
```

### `gdprDLRef`

**同意マネージャーの言語構成を上書きする**  
同意マネージャーで使用する言語を格納するデータレイヤー変数の名前を指定します。

たとえば、データレイヤーに `site_language` という名前の変数が含まれている場合は、次のように構成します。

```js
window.utag_cfg_ovrd = window.utag_cfg_ovrd || {}
window.utag_cfg_ovrd.gdprDLRef = "site_language";
```


<blockquote>
言語コードを直接構成しないでください。この上書き構成では、言語コードの値ではなく変数名が必要です。
</blockquote>


### `ignoreLocalStorage`

**ローカル保存変数を無視する**  
すべてのローカル保存変数を無視します。（デフォルト：`false`）

```js
window.utag_cfg_ovrd.ignoreLocalStorage = true;
```


### `ignoreSessionStorage`

**セッション保存変数を無視する**  
すべてのセッション保存変数を無視します。（デフォルト：`false`）

```js
window.utag_cfg_ovrd.ignoreSessionStorage = true;
```


### `load_rules_ajax`

**ページ読み込み後のロードルールを無効にする（レガシー）**  
同じページ読み込み内で `utag.view` および `utag.link` が呼び出されるたびに、ロードルールを再処理するかどうかを制御します。新たにトリガーされたロードルールによって、新しいタグがページに読み込まれる場合があります。この構成は、4.2xより前のバージョンの `utag.js` の動作を再現するために使用します。（デフォルト：`true`）

```js
window.utag_cfg_ovrd.load_rules_ajax = false;
```

### `load_rules_at_wait`

**拡張機能の実行後にロードルールを実行する（レガシー）**  
拡張機能の実行後にロードルールを評価します。古いバージョンの `utag.js`、および `utag.js` の読み込み後にデータレイヤーオブジェクトへデータが構成される環境で使用します。新しいバージョンの `utag.js` では、この構成の代わりに拡張機能の実行順序を使用します。（デフォルト：`false`）

```js
window.utag_cfg_ovrd.load_rules_at_wait = true;
```
### `lowermeta`

**メタタグデータを小文字に変換（レガシー）**  
すべてのメタデータ変数名と値を小文字に変換します。4.2xより前のバージョンの`utag.js`の動作を再現します。（デフォルト：`false`）

メタタグの例：
```html
<meta content="Tag Management" property="Article:Section">
```

結果の値：
```js
utag.data['meta.article:section']="iq tag management"
```

```js
window.utag_cfg_ovrd.lowermeta = true;
```

### `lowerqp`

**クエリ文字列のパラメータ名と値を小文字に変換（レガシー）**  
すべてのクエリ文字列変数名と値を小文字に変換します。4.2xより前のバージョンの`utag.js`の動作を再現します。（デフォルト：`false`）

クエリ文字列パラメータの例：`&RefId=Abc123`  
結果の値：`utag.data['qp.refid']="abc123"`

```js
window.utag_cfg_ovrd.lowerqp = true;
```

### `noload`

**すべての処理を停止**  
**Pre Loader**をスコープとする拡張機能の実行後に、すべてのコードの実行を停止します。**DOM Ready**をスコープとする拡張機能は引き続き実行されます。通常、この構成は**Prevent Tag Load**のパブリッシュ構成を使用して調整します。（デフォルト：`0`）

```js
window.utag_cfg_ovrd.noload = true;
```

### `noview`

**初回ページ読み込み時の自動トラッキング呼び出しを無効化**  
初回ページ読み込み時に自動的に行われるトラッキング呼び出しを抑止します。この構成は、シングルページアプリケーションのサイトでよく使用されます。（デフォルト：`false`）

```js
window.utag_cfg_ovrd.noview = true;
```

### `nocookie`

**Cookieのオプトアウト**  
訪問がすべてのCookieを明示的にオプトアウトした場合にのみ、このオプションを構成してください。（デフォルト：`false`）  

<blockquote>
このオプションを使用すると訪問数とセッション数が実際より多くなり、すべての訪問が「単一ページセッション」のように見えます。
</blockquote>


このオプションは、[Persist Data Value拡張機能](https://docs.tealium.com/persist-data-value-extension/)で構成されたCookieやセッションCookieを含め、`utag.js`による_すべての_Cookieの保存を無効にします。また、Cookieを使用できない場合、変数`ut.visitor_id`、`tealium_visitor_id`、`cp.utag_main_v_id`に新しいタイムスタンプを構成します。

```js
window.utag_cfg_ovrd.nocookie = true
```

### `noconsole`

**デバッグコンソール出力を抑止**  
`utag.DB`のデバッグメッセージがブラウザコンソールに表示されないようにします。デバッグ出力は引き続き`utag.db_log`配列に書き込まれます。（デフォルト：`false`）

```js
window.utag_cfg_ovrd.noconsole = true;
```

### `nonblocking_tags`

**タグを非同期で読み込む**  
（[`utag.js` 4.52](https://docs.tealium.com/ja/release-notes/?filter=tealium-universal-tag#tealium-universal-tag-2024-12-18)で新しく追加）  
このオプションを使用すると、すべてのタグでノンブロッキング動作が有効になり、INPスコアとページ全体のパフォーマンスを改善できる可能性があります。ユーザー操作を遅延させてINPスコアを低下させる、リソース負荷の高いタグを含むページでこの構成を使用してください。ただし、離脱リンクのトラッキングを十分にテストしてください。（デフォルト：`false`）

```js
window.utag_cfg_ovrd.nonblocking_tags = true;
```

#### ベストプラクティス

`nonblocking_tags`構成では、次のベストプラクティスに従ってください。

* `nonblocking_tags`構成の使用を検討する前に、ページを測定および監視し、タグ実装を軽量化してください。
* `nonblocking_tags`は、INPが200ミリ秒を超える原因となるリソース負荷の高いタグを含み、DOMのレンダリングをブロックする必要がないページでのみ使用してください。
* ノンブロッキングタグはトラッキングのためにページを停止させずに読み込まれるため、重要なナビゲーションイベントや離脱イベントで発生するナビゲーションの遅延を考慮してください（これがINPスコアを改善できる理由です）。

### `path`

**パブリッシュURLのパス**  
タグテンプレートのパブリッシュURLパスを構成し、指定されている場合は[Publish Configurationダイアログ]()のPublish URLsフィールドを上書きします。パブリッシュURLパスの構成は、セルフホスティングおよび[First Party Domains]()を利用するお客様に役立ちます。

```js
window.utag_cfg_ovrd.path = '//tags.example.com/main/prod';
```

### `readywait`

**DOM Readyまで処理を遅延**  
ブラウザからDOM Readyシグナルを受信するまで、すべての処理を停止します。**Pre Loader**をスコープとする拡張機能は、`utag.js`の読み込み時に引き続き実行されます。（デフォルト：`0`）

```js
window.utag_cfg_ovrd.readywait = true;
```

### `secure_cookie`

**セキュアCookie**  
（[`utag.js` 4.48](https://docs.tealium.com/ja/release-notes/?filter=tealium-universal-tag#tealium-universal-tag-2021-04-01)で新しく追加）  
[Persist Data Values拡張機能](https://docs.tealium.com/persist-data-value-extension/)および[`SC()`](https://docs.tealium.com/ja/platforms/javascript/api/cookie-functions/#utag-loader-sc)関数によって構成されるすべての`utag_main` Cookieで、属性文字列を`secure`に構成します。セキュアCookieは、HTTPSページでのみ構成およびアクセスできます。（デフォルト：`false`）

```js
window.utag_cfg_ovrd.secure_cookie = true;
```

### `session_timeout`

**セッションタイムアウト**  
現在のセッションが期限切れになるまでの待機時間をミリ秒単位で構成します。通常、この値はSession Timeoutのパブリッシュ構成構成を使用して調整します。（デフォルト：`1800000`（30分））

タイムアウトを900000ミリ秒（15分）に構成する例：
```js
window.utag_cfg_ovrd.session_timeout = 900000;
```

### `split_cookie`

**スタンドアロンCookie**  
（[`utag.js` 4.50](https://docs.tealium.com/ja/release-notes/?filter=tealium-universal-tag#tealium-universal-tag-2023-09-01)で新しく追加）  
`utag_`名前空間のCookie（組み込みの`utag_main` Cookieなど）を、[`utag.loader.SC`](https://docs.tealium.com/ja/platforms/javascript/api/cookie-functions/#utagloadersc)によって複数値Cookieとして書き込むか、スタンドアロンCookieとして書き込むかを指定します。（デフォルト：`true`）

```js
window.utag_cfg_ovrd.split_cookie = false;
```

### `split_cookie_allowlist`

**`utag_main`サブCookie**  
（[`utag.js` 4.50](https://docs.tealium.com/ja/release-notes/?filter=tealium-universal-tag#tealium-universal-tag-2023-09-01)で新しく追加）  
許可する`utag_main`サブCookieの配列を指定します。許可リストは、`split_cookie`が`true`に構成されている場合にのみ適用されます。これはバージョン4.50以降のデフォルト構成です。

`split_cookie_allowlist`が定義され、有効になっている場合は、以下が適用されます。

* `utag.loader.SC`は`utag_main` Cookieのみを構成します。
* このリストに含まれるサブCookieのみが`utag_main`名前空間に構成されます。

`split_cookie_allowlist`が定義されていない場合、または`split_cookie`が`true`ではない場合は、`utag_`名前空間のすべてのCookieが許可されます。


<blockquote>
このオプションで`ses_id`、`_st`、`_ss`を許可しない場合、訪問数とセッション数が実際より多くなり、すべての訪問が単一ページセッションのように見えます。
</blockquote>


```js
window.utag_cfg_ovrd.split_cookie_allowlist = ["v_id", "_ss", "_st", "ses_id"];
```

### `suppress_before_load_rules_with_uids`

**UIDによるタグのトラッキング時にBefore Load Rules拡張機能をスキップ**  
（[`utag.js` 4.52](https://docs.tealium.com/ja/release-notes/?filter=tealium-universal-tag#tealium-universal-tag-2024-12-18)で新しく追加）

デフォルトでは、**Before Load Rules**をスコープとする拡張機能は、[UIDによるタグのトラッキング](https://docs.tealium.com/tracking-functions/)時を含め、すべてのトラッキング呼び出しで実行されます。以前は、UIDによるタグのトラッキング時にこれらの拡張機能は実行されませんでした。

UIDによるタグのトラッキング時に、**Before Load Rules**をスコープとする拡張機能をスキップするには、このオプションを`true`に構成します（レガシー動作）。（デフォルト：`false`）

```js
window.utag_cfg_ovrd.suppress_before_load_rules_with_uids = true;
```


### `waittimer`

**タイマーを使用してタグを遅延**  
DOM Readyイベントの後、タグを読み込むまでの待機時間をミリ秒単位で構成します。（デフォルト：未構成）

```js
window.utag_cfg_ovrd.waittimer = 1000;
```