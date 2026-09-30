---
title: 構成
description: `utag.js`の挙動を調整する構成について学びます。
url: https://docs.tealium.com/ja/platforms/javascript/settings/
---
## 動作原理

`utag.js`の多くの挙動は、`utag.cfg`オブジェクト内の構成で制御されます。これらのデフォルトの挙動は、`utag_cfg_ovrd`という新しいオブジェクトを使用して上書きされます。このオブジェクトを使用するには、`utag.js`をロードする前にページコードで構成するか、**Pre Loader**にスコープされた[JavaScript Code Extension](https://docs.tealium.com/advanced-javascript-code-extension/)内で以下のように構成します：

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
| [`gdprDLRef`](#gdprdlref) | 同意管理者が使用する言語構成を格納するデータレイヤー変数の名前を指定します。 |
| [`ignoreLocalStorage`](#ignorelocalstorage) | ローカル保存変数をデータレイヤーに追加しないようにします。 |
| [`ignoreSessionStorage`](#ignoresessionstorage) | セッション保存変数をデータレイヤーに追加しないようにします。 |
| [`load_rules_ajax`](#load_rules_ajax) | ページロード後のロードルールを無効にします（レガシー）。 |
| [`load_rules_at_wait`](#load_rules_at_wait) | 拡張機能の後でロードルールを実行します（レガシー）。 |
| [`lowermeta`](#lowermeta)| メタタグの名前と値を小文字にします（レガシー）。 |
| [`lowerqp`](#lowerqp)| クエリ文字列パラメータの名前と値を小文字にします（レガシー）。 |
| [`noload`](#noload) | すべての機能を無効にします。 |
| [`noview`](#noview) | 初回ページロード時の自動トラッキングコールを無効にします。 |
| [`nocookie`](#nocookie) | `utag_main`クッキーを無効にします。 |
| [`noconsole`](#noconsole) | `utag.DB`コンソール出力を抑制します。 |
| [`nonblocking_tags`](#nonblocking_tags) | すべてのタグを非ブロッキングにして、極端なケースでのパフォーマンスとInteraction to Next Paint (INP)スコアを向上させます。デフォルト：`false`。 |
| [`path`](#path) | 公開パスを指定します。 |
| [`readywait`](#readywait) | DOM-readyブラウザイベントまで操作を停止します。 |
| [`secure_cookie`](#secure_cookie) | [Persist Data Values extension](https://docs.tealium.com/persist-data-value-extension/)および[`utag.loader.SC`](https://docs.tealium.com/ja/platforms/javascript/api/cookie-functions/#utagloadersc)メソッドによって構成されるすべての`utag_main`クッキーの属性文字列を`secure`に構成します。 |
| [`session_timeout`](#session_timeout)| セッションの有効期限（ミリ秒単位）を構成します。 |
| [`split_cookie`](#split_cookie)| `utag_main`クッキーを独立したクッキーに分割します。デフォルト：`true` |
| [`split_cookie_allowlist`](#split_cookie_allowlist)| 許可された`utag_main`サブクッキーまたは独立したクッキーの配列。 |
| [`suppress_before_load_rules_with_uids`](#suppress_before_load_rules_with_uids) | UIDによるトラッキングタグの場合、**Before Load Rules**にスコープされた拡張機能をスキップするレガシー動作を強制します。デフォルト：`false`。 |
| [`waittimer`](#waittimer) | タグのロード前に遅延する時間（ミリ秒単位）を構成します。|

### `always_set_v_id`

**`utag.js`に`utag_main_v_id`クッキーまたは`utag_main`の`v_id`コンポーネントを構成させる**  
([`utag.js` 4.50](https://docs.tealium.com/ja/release-notes/?filter=tealium-universal-tag#tealium-universal-tag-2023-09-01)で新規導入)  
`utag_main`の`v_id`変数は、データプライバシーと同意目的に準拠するためにTealium Collectタグによって構成されます。これを`true`に構成すると、`utag.js`はすべての訪問に対してこのクッキーを構成するように強制します。（デフォルト：`false`）

```js
window.utag_cfg_ovrd.always_set_v_id = true;
```

### `cmcookiens`

**同意管理クッキー名**  
同意管理クッキー名をカスタマイズします。同じドメイン名で複数のプロファイルを持っている場合は、クッキー間の競合や潜在的なデータ漏洩を防ぐために、各プロファイルに固有の同意管理クッキー名を構成してください。

```js
window.utag_cfg_ovrd.cmcookiens = "CONSENTMGR_NL-CMB-CG1";
```

### `consentPeriod`

**同意構成保持期間**  
GDPRおよびCCPAの同意ステータスを保持する日数を構成します。GDPRの組み込み有効期限は365日、CCPAの有効期限は395日です。

```js
window.utag_cfg_ovrd.consentPeriod = 60;
```

### `disable_tealium_attribute_override`

**システム定義の属性の上書きを防ぐ**  

([`utag.js` 4.54](https://docs.tealium.com/ja/release-notes/?filter=tealium-universal-tag#tealium-universal-tag-2025-10-22)で新規導入)

`true`に構成すると、この構成は受信データが`tealium_visitor_id`および`tealium_event`を除く`tealium_`で始まるシステム定義の属性を上書きするのをブロックします。

`utag.js`のバージョン4.52および4.53では、この保護はデフォルトで有効になっており、一部のモバイルWebビュー環境で問題を引き起こしました。バージョン4.54では、保護はオプトインになり、完全な制御が可能です。

（デフォルト：`false`）

```js
window.utag_cfg_ovrd.disable_tealium_attribute_override = true;
```

### `dom_complete`

**DOM完了（ロード）ブラウザイベントまでタグを遅延させる**  
[ドキュメントロードイベント](https://developer.mozilla.org/en-US/docs/Web/Events/load)ではなく、DOM Readyでタグをロードします。これにより、DOM Readyにスコープされた拡張機能も遅延されます。（デフォルト：`false`）

```js
window.utag_cfg_ovrd.dom_complete = true;
```

### `domain`

**クッキードメインを上書きする**  
`utag_main`クッキーが構成されるドメインを構成します。たとえば、`amazonaws.com`のようなルートドメインでクッキーを受け入れないサイトに便利です。（デフォルト：`location.hostname`のトップレベルドメイン）

```js
window.utag_cfg_ovrd.domain = "mysite.amazonaws.com";
```

### `gdprDLRef`

**同意管理者で使用する言語構成を上書きする**  
同意管理者で使用する言語を格納するデータレイヤー変数の名前を指定します。

たとえば、データレイヤーに`site_language`という変数が含まれている場合：

```js
window.utag_cfg_ovrd = window.utag_cfg_ovrd || {}
window.utag_cfg_ovrd.gdprDLRef = "site_language";
```


<blockquote>
言語コードを直接構成しないでください。この上書き構成は変数名を期待しており、言語コード値ではありません。
</blockquote>


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

**ページロード後のロードルールを無効にする（レガシー）**  
同じページロード内で`utag.view`および`utag.link`が呼び出されるたびにロードルールが再処理されるかどうかを制御します。新たにトリガーされたロードルールがページに新しいタグをロードする可能性があります。`utag.js`の4.2xより前のバージョンの動作を再現するためにこの構成を使用します。（デフォルト：`true`）

```js
window.utag_cfg_ovrd.load_rules_ajax = false;
```

### `load_rules_at_wait`

**拡張機能の後でロードルールを実行する（レガシー）**  
拡張機能の後でロードルールを評価します。`utag.js`の古いバージョンや、`utag.js`のロード後にデータレイヤーオブジェクトが入力されるインストールで使用されます。新しいバージョンの`utag.js`では、この構成の代わりに拡張機能の実行順序を使用します。（デフォルト：`false`）

```js
window.utag_cfg_ovrd.load_rules_at_wait = true;
```
### `lowermeta`

**メタタグデータを小文字にする（レガシー）**  
すべてのメタデータ変数名と値を小文字にします。`utag.js`のバージョン4.2x以前の動作を再現します。（デフォルト：`false`）

メタタグの例：
```html
<meta content="iQ Tag Management" property="Article:Section">
```

結果の値：
```js
utag.data['meta.article:section']="iq tag management"
```

```js
window.utag_cfg_ovrd.lowermeta = true;
```

### `lowerqp`

**クエリ文字列パラメータ名と値を小文字にする（レガシー）**  
すべてのクエリ文字列変数名と値を小文字にします。`utag.js`のバージョン4.2x以前の動作を再現します。（デフォルト：`false`）

クエリ文字列パラメータの例：`&RefId=Abc123`
結果の値：`utag.data['qp.refid']="abc123"`

```js
window.utag_cfg_ovrd.lowerqp = true;
```

### `noload`

**すべての操作を停止**  
**Pre Loader**にスコープされた拡張機能の後でコードの実行が停止します。**DOM Ready**にスコープされた拡張機能は実行されます。通常、**Prevent Tag Load**の公開構成を使用して調整されます。（デフォルト：`0`）

```js
window.utag_cfg_ovrd.noload = true;
```

### `noview`

**初回ページロード時の自動トラッキングコールを無効にする**  
初回ページロード時に自動的に発生するトラッキングコールを抑制します。この構成は、シングルページアプリケーションサイトでよく使用されます。（デフォルト：`false`）

```js
window.utag_cfg_ovrd.noview = true;
```

### `nocookie`

**Cookieのオプトアウト**  
訪問がすべてのCookieの使用を明示的にオプトアウトした場合のみ、このオプションを構成してください。（デフォルト：`false`）

<blockquote>
このオプションを使用すると、訪問数とセッション数が増加し、すべての訪問が「シングルページセッション」のように見えます。
</blockquote>


このオプションは、`utag.js`によって構成されるすべてのCookieの保存を無効にします。これには、[Persist Data Value extension](https://docs.tealium.com/persist-data-value-extension/)で構成されるCookieやセッションCookieも含まれます。また、Cookieが利用できない場合には、`ut.visitor_id`、`tealium_visitor_id`、`cp.utag_main_v_id`の変数に新しいタイムスタンプを構成します。

```js
window.utag_cfg_ovrd.nocookie = true
```

### `noconsole`

**デバッグコンソール出力を抑制**  
ブラウザコンソールに表示される`utag.DB`デバッグメッセージの出現を防ぎます。デバッグ出力は`utag.db_log`配列に引き続き書き込まれます。（デフォルト：`false`）

```js
window.utag_cfg_ovrd.noconsole = true;
```

### `nonblocking_tags`

**タグを非同期でロード**  
（[`utag.js` 4.52](https://docs.tealium.com/ja/release-notes/?filter=tealium-universal-tag#tealium-universal-tag-2024-12-18)で新設）  
すべてのタグの非ブロッキング動作を有効にします。これにより、INPスコアと全体的なページパフォーマンスが向上します。リソースを多く消費するタグがユーザーのインタラクションを遅延させ、INPスコアを低下させるページでこの構成を使用してくださいが、退出リンクのトラッキングが正しく機能するか十分にテストしてください。（デフォルト：`false`）

```js
window.utag_cfg_ovrd.nonblocking_tags = true;
```

#### ベストプラクティス

`nonblocking_tags`構成を使用する際のベストプラクティス：

* ページを測定し、監視し、タグの実装を軽量化することを検討してから`nonblocking_tags`構成を使用してください。
* INPスコアが200ミリ秒を超え、DOMレンダリングをブロックする必要がないページでのみ`nonblocking_tags`を使用してください。
* 非ブロッキングタグはページを保持せずにロードされるため、重要なナビゲーションや退出イベントの遅延を考慮してください（これがINPスコアを改善する理由です）。