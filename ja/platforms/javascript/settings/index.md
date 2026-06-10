---
title: 構成
description: `utag.js`の挙動を調整する構成について学びましょう。
url: https://docs.tealium.com/ja/platforms/javascript/settings/
---
## 動作原理

`utag.js`の多くの挙動は、`utag.cfg`オブジェクト内の構成で制御されます。これらのデフォルトの挙動は、`utag_cfg_ovrd`という新しいオブジェクトを使用して上書きされます。このオブジェクトを使用するには、`utag.js`の読み込み前にページコード内で構成するか、**Pre Loader**にスコープされた[JavaScript Code Extension]()内で以下のように構成します：

```js
window.utag_cfg_ovrd = window.utag_cfg_ovrd || {};
```

## オプションのリスト

以下の表は、利用可能な構成をまとめたものです：

| 構成 | 説明 |
| ------- | ----------- |
| [`always_set_v_id`](#always_set_v_id)| `utag_main_v_id`クッキーまたは`utag_main`の`v_id`コンポーネントを構成します。デフォルト：`false` |
| [`cmcookiens`](#cmcookiens) | 同意管理クッキー名。 |
| [`consentPeriod`](#consentperiod) | ユーザーの同意構成を保持する日数を構成します。 |
| [`disable_tealium_attribute_override`](#disable_tealium_attribute_override) | システム定義の属性`tealium_*`が受信データによって上書きされるのを防ぎます。 |
| [`dom_complete`](#dom_complete) | DOM完了（ロード）イベントまでタグの実行を遅延させます。 |
| [`domain`](#domain) | クッキーを構成するドメインを上書きします。 |
| [`gdprDLRef`](#gdprdlref) | 同意管理者に使用される言語構成を格納するデータレイヤー変数の名前を指定します。 |
| [`ignoreLocalStorage`](#ignorelocalstorage) | データレイヤーにローカル保存変数を追加しないようにします。 |
| [`ignoreSessionStorage`](#ignoresessionstorage) | データレイヤーにセッション保存変数を追加しないようにします。 |
| [`load_rules_ajax`](#load_rules_ajax) | ページ読み込み後のロードルールを無効にします（レガシー）。 |
| [`load_rules_at_wait`](#load_rules_at_wait) | 拡張機能の後にロードルールを実行します（レガシー）。 |
| [`lowermeta`](#lowermeta)| メタタグの名前と値を小文字にします（レガシー）。 |
| [`lowerqp`](#lowerqp)| クエリ文字列パラメータの名前と値を小文字にします（レガシー）。 |
| [`noload`](#noload) | すべての機能を無効にします。 |
| [`noview`](#noview) | 初回ページ読み込み時の自動トラッキングコールを無効にします。 |
| [`nocookie`](#nocookie) | `utag_main`クッキーを無効にします。 |
| [`nonblocking_tags`](#nonblocking_tags) | すべてのタグを非ブロッキングにして、極端なケースでのパフォーマンスとInteraction to Next Paint (INP)スコアを向上させます。デフォルト：`false`。 |
| [`path`](#path) | 公開パスを指定します。 |
| [`readywait`](#readywait) | DOM-readyブラウザイベントまで操作を停止します。 |
| [`secure_cookie`](#secure_cookie) | [Persist Data Values extension]()および[`utag.loader.SC`](/ja/platforms/javascript/api/cookie-functions/#utagloadersc)メソッドによって構成されるすべての`utag_main`クッキーの属性文字列を`secure`に構成します。 |
| [`session_timeout`](#session_timeout)| セッションの有効期限（ミリ秒単位）を構成します。 |
| [`split_cookie`](#split_cookie)| `utag_main`クッキーをスタンドアロンのクッキーに分割します。デフォルト：`true` |
| [`split_cookie_allowlist`](#split_cookie_allowlist)| 許可された`utag_main`サブクッキーまたはスタンドアロンクッキーの配列。 |
| [`suppress_before_load_rules_with_uids`](#suppress_before_load_rules_with_uids) | UIDによるトラッキングタグの場合、**Before Load Rules**にスコープされた拡張機能をスキップするレガシー動作を強制します。デフォルト：`false`。 |
| [`waittimer`](#waittimer) | タグの読み込み前に遅延する時間（ミリ秒単位）を構成します。|

### `always_set_v_id`

**`utag.js`に`utag_main_v_id`クッキーまたは`utag_main`の`v_id`コンポーネントを構成させる**  
([`utag.js` 4.50](/ja/release-notes/?filter=tealium-universal-tag#tealium-universal-tag-2023-09-01)で新規導入)  
`utag_main`の`v_id`変数は、データプライバシーと同意目的に準拠するためにTealium Collectタグによって構成されます。これを`true`に構成すると、すべての訪問に対してこのクッキーを構成するよう`utag.js`に強制します。（デフォルト：`false`）

```js
window.utag_cfg_ovrd.always_set_v_id = true;
```

### `cmcookiens`

**同意管理クッキー名**  
同意管理クッキーの名前をカスタマイズします。同じドメイン名で複数のプロファイルを持っている場合は、クッキー間の競合や潜在的なデータ漏洩を防ぐために、各プロファイルに固有の同意管理クッキー名を付けます。

```js
window.utag_cfg_ovrd.cmcookiens = &#34;CONSENTMGR_NL-CMB-CG1&#34;;
```

### `consentPeriod`

**同意構成の保持期間**  
GDPRおよびCCPAの同意ステータスを保持する日数を構成します。GDPRの場合は365日、CCPAの場合は395日が組み込みの有効期限です。

```js
window.utag_cfg_ovrd.consentPeriod = 60;
```

### `disable_tealium_attribute_override`

**システム定義の属性の上書きを防ぐ**  

([`utag.js` 4.54](/ja/release-notes/?filter=tealium-universal-tag#tealium-universal-tag-2025-10-22)で新規導入)

`true`に構成すると、この構成は受信データが`tealium_visitor_id`などの`tealium_`で始まるシステム定義の属性を上書きするのをブロックします。

`utag.js`のバージョン4.52および4.53では、この保護はデフォルトで有効になっており、一部のモバイルWebビュー環境で問題が発生していました。バージョン4.54では、保護はオプトインになり、完全な制御が可能です。

（デフォルト：`false`）

```js
window.utag_cfg_ovrd.disable_tealium_attribute_override = true;
```

### `dom_complete`

**DOM完了（ロード）ブラウザイベントまでタグを遅延させる**  
DOM Readyではなく、[document load event](https://developer.mozilla.org/en-US/docs/Web/Events/load)でタグを読み込みます。これにより、DOM Readyにスコープされた拡張機能も遅延されます。（デフォルト：`false`）

```js
window.utag_cfg_ovrd.dom_complete = true;
```

### `domain`

**クッキードメインを上書きする**  
`utag_main`クッキーが構成されるドメインを構成します。たとえば、クッキーを受け入れないルートドメインのサイトの場合、`amazonaws.com`などです。（デフォルト：`location.hostname`のトップレベルドメイン）

```js
window.utag_cfg_ovrd.domain = &#34;mysite.amazonaws.com&#34;;
```

### `gdprDLRef`

**同意管理者で使用する言語構成を上書きする**  
同意管理者で使用される言語を格納するデータレイヤー変数の名前を指定します。

たとえば、データレイヤーに`site_language`という変数が含まれている場合：

```js
window.utag_cfg_ovrd = window.utag_cfg_ovrd || {}
window.utag_cfg_ovrd.gdprDLRef = &#34;site_language&#34;;
```

言語コードを直接構成しないでください。この上書き構成は変数名を期待しており、言語コード値ではありません。

### `ignoreLocalStorage`

**ローカル保存変数を無視する**
ローカル保存変数を無視します。（デフォルト：`false`）

```js
window.utag_cfg_ovrd.ignoreLocalStorage = true;
```


### `ignoreSessionStorage`

**セッション保存変数を無視する**
セッション保存変数を無視します。（デフォルト：`false`）

```js
window.utag_cfg_ovrd.ignoreSessionStorage = true;
```


### `load_rules_ajax`

**ページ読み込み後のロードルールを無効にする（レガシー）**  
`utag.view`および`utag.link`が同じページ読み込み内で呼び出されるたびにロードルールが再処理されるかどうかを制御します。新たにトリガーされたロードルールがページに新しいタグを読み込む可能性があります。`utag.js`の4.2xより前のバージョンの動作を再現するためにこの構成を使用します。（デフォルト：`true`）

```js
window.utag_cfg_ovrd.load_rules_ajax = false;
```

### `load_rules_at_wait`

**拡張機能の後にロードルールを実行する（レガシー）**  
拡張機能の後にロードルールを評価します。`utag.js`の古いバージョンや、`utag.js`の読み込み後にデータレイヤーオブジェクトが構成されるインストールで使用されます。新しいバージョンの`utag.js`では、この構成の代わりに拡張機能の実行順序を使用します。（デフォルト：`false`）

```js
window.utag_cfg_ovrd.load_rules_at_wait = true;
```

### `lowermeta`

**メタタグデータを小文字にする（レガシー）**  
すべてのメタデータ変数名と値を小文字にします。`utag.js`の4.2xより前のバージョンの動作を再現します。（デフォルト：`false`）

例のメタタグ：
```html
&lt;meta content=&#34;Tag Management&#34; property=&#34;Article:Section&#34;&gt;
```

結果の値：
```js
utag.data[&#39;meta.article:section&#39;]=&#34;iq tag management&#34;
```

```js
window.utag_cfg_ovrd.lowermeta = true;
```
### `lowerqp`

**クエリ文字列パラメータ名と値を小文字にする（レガシー）**  
すべてのクエリ文字列変数名と値を小文字にします。これは、`utag.js` バージョン4.2x以前の動作を再現します。（デフォルト：`false`）

例えばクエリ文字列パラメータ： `&amp;RefId=Abc123`
結果の値： `utag.data[&#39;qp.refid&#39;]=&#34;abc123&#34;`

```js
window.utag_cfg_ovrd.lowerqp = true;
```

### `noload`

**すべての操作を停止**  
**Pre Loader** にスコープされた拡張機能の後にすべてのコードの実行が停止します。**DOM Ready** にスコープされた拡張機能は実行されます。これは通常、**Prevent Tag Load** の公開構成を使用して調整されます。（デフォルト：`0`）

```js
window.utag_cfg_ovrd.noload = true;
```

### `noview`

**初期ページロード時の自動トラッキングコールを無効にする**  
初期ページロード時に自動的に発生するトラッキングコールを抑制します。この構成は、シングルページアプリケーションサイトでよく使用されます。（デフォルト：`false`）

```js
window.utag_cfg_ovrd.noview = true;
```

### `nocookie`

**Cookieのオプトアウト**  
訪問がすべてのCookieの使用を明示的にオプトアウトした場合のみ、このオプションを構成してください。（デフォルト：`false`）
このオプションを使用すると、訪問とセッションのカウントが増加し、すべての訪問が「シングルページセッション」のように見えるようになります。

このオプションは、`utag.js` によって構成されるすべてのCookieの保存を無効にし、[Persist Data Value extension]()で構成されるCookieやセッションCookieも含まれます。また、Cookieが利用できない場合には、`ut.visitor_id`、`tealium_visitor_id`、`cp.utag_main_v_id` の変数に新しいタイムスタンプを構成します。

```js
window.utag_cfg_ovrd.nocookie = true
```

### `nonblocking_tags`

**非同期でタグをロード**  
([`utag.js` 4.52](/ja/release-notes/?filter=tealium-universal-tag#tealium-universal-tag-2024-12-18)で新規導入)  
このオプションは、すべてのタグの非ブロッキング動作を有効にし、INPスコアと全体的なページパフォーマンスを向上させることができます。ユーザーのインタラクションを遅くし、INPスコアを低下させるリソース集約型のタグがあるページでこの構成を使用してくださいが、出口リンクのトラッキングを徹底的にテストすることを確認してください。（デフォルト：`false`）

```js
window.utag_cfg_ovrd.nonblocking_tags = true;
```

#### ベストプラクティス

`nonblocking_tags` 構成を使用する際のベストプラクティス：

* ページを測定し、監視し、タグの実装を軽くする前に `nonblocking_tags` 構成の使用を検討してください。
* INPスコアが200ミリ秒を超え、DOMのレンダリングをブロックする必要がないページでのみ `nonblocking_tags` を使用してください。
* 非ブロッキングタグはページを保持せずにロードされるため、重要なナビゲーションや出口イベントの遅延に注意してください（これがINPスコアを改善する理由です）。

### `path`

**公開URLパスを構成**  
タグテンプレートの公開URLパスを構成し、指定されている場合は[公開構成ダイアログ]()の公開URLフィールドを上書きします。公開URLパスの構成は、自己ホスティングおよび[First Party Domains]()の顧客にとって有用です。

```js
window.utag_cfg_ovrd.path = &#39;//tags.example.com/main/prod&#39;;
```

### `readywait`

**DOM-readyまで操作を遅延**  
ブラウザからDOM-ready信号を受信するまで、すべての操作を停止します。**Pre Loader** にスコープされた拡張機能は、`utag.js` がロードされたときに実行されます。（デフォルト：`0`）

```js
window.utag_cfg_ovrd.readywait = true;
```

### `secure_cookie`

**セキュアCookie**  
([`utag.js` 4.48](/ja/release-notes/?filter=tealium-universal-tag#tealium-universal-tag-2021-04-01)で新規導入)  
[Persist Data Values extension]()および[`SC()`](/ja/platforms/javascript/api/cookie-functions/#utag-loader-sc)関数によって構成されるすべての`utag_main`クッキーに対して、属性文字列を`secure`に構成します。セキュアクッキーはHTTPSページでのみ構成およびアクセスが可能です。（デフォルト：`false`）

```js
window.utag_cfg_ovrd.secure_cookie = true;
```

### `session_timeout`

**セッションタイムアウト** 
現在のセッションが期限切れになるまでの待ち時間をミリ秒単位で構成します。これは通常、セッションタイムアウトの公開構成を使用して調整されます。（デフォルト：`1800000` (30分)）

タイムアウトを900000ミリ秒（15分）に構成する例：
```js
window.utag_cfg_ovrd.session_timeout = 900000;
```

### `split_cookie`

**スタンドアロンクッキー**  
([`utag.js` 4.50](/ja/release-notes/?filter=tealium-universal-tag#tealium-universal-tag-2023-09-01)で新規導入)  
`utag_`名前空間のクッキー（組み込みの`utag_main`クッキーなど）がマルチバリュークッキーとして書き込まれるか、[`utag.loader.SC`](/ja/platforms/javascript/api/cookie-functions/#utagloadersc)によってスタンドアロンクッキーとして書き込まれるかを決定します。（デフォルト：`true`）

```js
window.utag_cfg_ovrd.split_cookie = false;
```

### `split_cookie_allowlist`

**`utag_main`サブクッキー**  
([`utag.js` 4.50](/ja/release-notes/?filter=tealium-universal-tag#tealium-universal-tag-2023-09-01)で新規導入)  
許可された`utag_main`サブクッキーの配列を指定します。許可リストは、`split_cookie`が`true`に構成されている場合にのみ適用されます。これは、バージョン4.50以降のデフォルト構成です。

`split_cookie_allowlist`が定義されており、アクティブである場合、以下が適用されます：

* `utag.loader.SC`は`utag_main`クッキーのみを構成します。
* このリストにあるサブクッキーのみが`utag_main`名前空間で構成されます。

`split_cookie_allowlist`が定義されていない場合、または`split_cookie`が`true`でない場合、すべての`utag_`名前空間のクッキーが許可されます。

`ses_id`、`_st`、`_ss`を許可せずにこのオプションを使用すると、訪問とセッションのカウントが増加し、すべての訪問がシングルページセッションのように見えるようになります。

```js
window.utag_cfg_ovrd.split_cookie_allowlist = [&#34;v_id&#34;, &#34;_ss&#34;, &#34;_st&#34;, &#34;ses_id&#34;];
```

### `suppress_before_load_rules_with_uids`

**UIDによるトラッキングタグの場合、Before Load Rules拡張機能をスキップ**  
([`utag.js` 4.52](/ja/release-notes/?filter=tealium-universal-tag#tealium-universal-tag-2024-12-18)で新規導入)  

デフォルトでは、**Before Load Rules**にスコープされた拡張機能は、[UIDによるトラッキングタグ]()の場合でもすべてのトラッキングコールに対して実行されます。以前は、UIDによるトラッキングタグの場合、これらの拡張機能は実行されませんでした。

このオプションを`true`に構成すると、UIDによるトラッキングタグの場合、**Before Load Rules**にスコープされた拡張機能をスキップします（レガシー動作）。（デフォルト：`false`）

```js
window.utag_cfg_ovrd.suppress_before_load_rules_with_uids = true;
```

### `waittimer`

**タイマーでタグを遅延**
DOM Readyイベントの後、タグのロードを待つ時間をミリ秒単位で構成します。（デフォルト：構成なし）

```js
window.utag_cfg_ovrd.waittimer = 1000;
```
