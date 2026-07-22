---
title: GDPR関数
description: TealiumがJavaScript用に提供するGDPR関数のリファレンスガイド。
url: https://docs.tealium.com/ja/platforms/javascript/api/gdpr-functions/
---
以下の `utag.gdpr` 関数が利用可能です：

| 関数 | 説明 |
| --- | --- |
| [`dns.getDnsState()`](#utaggdprdnsgetdnsstate) | `dns` 同意クッキーの値を返します。 |
| [`dns.setDnsState()`](#utaggdprdnssetdnsstate) | `dns` 同意クッキーの値を構成します。 |
| [`getCategories()`](#utaggdprgetcategories) | タグのグループ化に利用可能なコンプライアンスカテゴリのリストを `Array` で返します。|
| [`getCategoryLanguage()`](#utaggdprgetcategorylanguage) | アクティブな言語でのカテゴリ名と説明を含む `Object` を返します。 |
| [`getConsentState()`](#utaggdprgetconsentstate) | ユーザーが与えた同意を全面的、拒否、同意なし、または部分的な同意として返します。 |
| [`getCookieValues()`](#utaggdprgetcookievalues) | 同意クッキーを表す `Object` を返します。 |
| [`getLanguage()`](#utaggdprgetlanguage) | 同意マネージャーのコンテンツを表示するために使用される言語を `String` で返します。 |
| [`getSelectedCategories()`](#utaggdprgetselectedcategories) | 顧客が選択したカテゴリを `Array` で返します。 |
| [`setAllCategories()`](#utaggdprsetallcategories) | すべてのカテゴリを同意したか拒否したかの同意状態に構成し、（オプションで）同意を追跡するためにCollect APIを呼び出します。 |
| [`setConsentValue()`](#utaggdprsetconsentvalue) | 同意クッキーの値を有効または無効に構成します。 |
| [`setCookie()`](#utaggdprsetcookie) | クッキー `Object` に直接書き込む内部関数。 |
| [`setCookieValue()`](#utaggdprsetcookievalue) | 同意クッキーの個々の値を構成します。 |
| [`setPreferencesFromList()`](#utaggdprsetpreferencesfromlist) | カテゴリのリストに対して同意状態を `allowed` に構成します。 |
| [`setPreferencesValues()`](#utaggdprsetpreferencesvalues) | カテゴリとその同意状態の `Object` からクッキーの値を構成します。 |
| [`showConsentPreferences()`](#utaggdprshowconsentpreferences) | プリファレンスマネージャーのポップアップを表示します。 |
| [`showDoNotSellBanner()`](#utaggdprshowdonotsellbanner) | CCPAバナーを表示します。 | 
| [`showDoNotSellPrompt()`](#utaggdprshowdonotsellprompt) | CCPAバナーを表示します。 |
| [`showExplicitConsent()`](#utaggdprshowexplicitconsent) | 明示的な同意のポップアップを表示します。 |
| [`updateConsentCookie()`](#utaggdprupdateconsentcookie) | 隠されたウェブビューを使用してアプリからモバイル同意を更新します。 |


## `utag.gdpr.dns.getDnsState()`

`dns` 同意クッキーの値（`true` または `false`）を返します。


## `utag.gdpr.dns.setDnsState()`

`dns` 同意クッキーの値を構成します。認識される値：`true`、`false`、`1`、`0`、`"true"`、`"false"`。

例：
```js
utag.gdpr.dns.setDnsState(true);
```

## `utag.gdpr.getCategories()`

タグのグループ化に利用可能なコンプライアンスカテゴリのリストを `Array` で返します。パラメータが提供されない場合、すべてのカテゴリが返されます。パラメータとして `true` または `1` を渡すと、Tealium Consent Preference Managerインターフェースで有効（アクティブ）なカテゴリのみが返されます。

```js
utag.gdpr.getCategories(onlyEnabledCats)
```

| パラメータ | タイプ | 説明 |
| --- | --- | --- |
| `onlyEnabledCats` | `Boolean` | （オプション）`true` または `1` に構成すると、有効（アクティブ）なカテゴリが返されます。 |


以下の例は、`utag.gdpr.getCategories()` がすべてのカテゴリを返すときの結果を示しています：  
```js
["analytics", "affiliates", "display_ads", "search", "email", "personalization", "social", "big_data", "misc", "cookiematch", "cdp", "mobile", "engagement", "monitoring", "crm"]
```

以下の例は、`utag.gdpr.getCategories()` が有効なカテゴリを返すときの結果を示しています：    
```js
["analytics", "affiliates", "personalization"]
```

## `utag.gdpr.getCategoryLanguage()`

アクティブな言語でのカテゴリ名と説明を含む `Object` を返します。カテゴリの言語は、`getLanguage()` 関数が返す言語です。

カテゴリに関する詳細情報は、[同意の構成を管理する](https://docs.tealium.com/iq-tag-management/consent-management/consent-preferences-dialog/manage#categories)を参照してください。

```js
utag.gdpr.getCategoryLanguage(category)
```

| パラメータ | タイプ | 説明 |
| --- | --- | --- |
| `category` | `String` | カテゴリの名前。 |

以下の例は、言語が英語の場合に `utag.gdpr.getCategoryLanguage("analytics")` によって返される `Object` を示しています：

```js
{name: "Cookies that help us improve our website", notes: "These cookies help us understand how people use our website."}
```
以下の例は、言語がポーランド語の場合に `utag.gdpr.getCategoryLanguage("analytics")` によって返される `Object` を示しています：

```js
{name: "Pliki cookie dotyczące wydajności", notes: "Te pliki cookie gromadzą informacje o tym, jak odw…dynie w celu ulepszania działania naszej witryny."}
```

## `utag.gdpr.getConsentState()`

以下の2つのデータタイプのいずれかを返します：

* 同意状態（全面的、拒否、または同意なし）を示す数値。
* 部分的な同意の場合、カテゴリ別の同意を指定する `Object` の `Array`。

全面的、拒否、または同意がない場合、以下の同意状態の値のいずれかが返されます：

| 同意状態 | 同意値 | 説明 |
|---| --- | --- |
| 全面的 | `1` | 全面的な同意が与えられました（クッキー上の `consent:true`）。 |
| 拒否 | `-1` | 同意が拒否されました（クッキー上の `consent:false`）。 |
| なし | `0` | 同意が与えられていません（クッキーが存在しない）。 |

部分的な同意が与えられた場合、`Object` の `Array` が返されます。各 `Object` は同意カテゴリを表します。`Array` 内の各 `Object` では、`"ct"` キーが同意値（`1`/`0`）を表し、`"name"` キーが同意カテゴリを指定します。

```js
utag.gdpr.getConsentState()
```

以下の例は、部分的な同意のために返される `Object` の `Array` を示しています：

```js
[{"ct":"1","name":"analytics"},
{"ct":"0","name":"affiliates"},
{"ct":"0","name":"display_ads"},
{"ct":"0","name":"search"},
{"ct":"0","name":"email"},
{"ct":"0","name":"personalization"},
{"ct":"0","name":"social"},
{"ct":"0","name":"big_data"},
{"ct":"0","name":"misc"},
{"ct":"0","name":"cookiematch"},
{"ct":"0","name":"cdp"},
{"ct":"0","name":"mobile"},
{"ct":"0","name":"engagement"},
{"ct":"0","name":"monitoring"},
{"ct":"0","name":"crm"}]
```

## `utag.gdpr.getCookieValues()`


<blockquote>
この関数を直接使用する代わりに、クッキーを読み取るために `getCookieValues()` 関数を呼び出す `utag.gdpr.getConsentState()` のような関数を使用することをお勧めします。
</blockquote>


同意クッキーをキーと値のペアとして表す `Object` を返します。この関数はデフォルトのクッキー名前空間（`CONSENTMGR`）を使用するか、`window.utag_cfg_ovrd.cmcookiens` で提供された値を使用します。逆の関数（クッキーに書き込む）は `utag.gdpr.setCookie()` です。

```js
utag.gdpr.getCookieValues()
```

以下の例は、部分的な同意のために `utag.gdpr.getCookieValues()` によって返される `Array` を示しています：  

```js
{
    "c1":"1",
    "c2":"0",
    "c3":"0",
    "c4":"0",
    "c5":"0",
    "c6":"0",
    "c7":"0",
    "c8":"0",
    "C9":"0",
    "c10":"0",
    "c11":"0",
    "c12":"0",
    "c13":"0",
    "c14":"0",
    "c15":"0",
    "ts":"1586965568213",
    "consent":"true"
}
```
以下の例は、全面的な同意のために `utag.gdpr.getCookieValues()` によって返される `Array` を示しています：  
```js
utag.gdpr.getCategories(true)

{"consent":"true","ts":"1587026030058"}
```

## `utag.gdpr.getLanguage()`

同意マネージャーのコンテンツを表示するために使用される言語を `String` で返します。データレイヤーで構成された言語、ブラウザからの言語、またはデフォルトの言語の優先順位によります。

```js
utag.gdpr.getLanguage()
```

以下の例は、言語が英語（イギリス）の場合に返される `String` を示しています：

```js
"en-gb"
```

## `utag.gdpr.getSelectedCategories()`

顧客が選択したカテゴリを含む `Array` を返します。

```js
utag.gdpr.getSelectedCategories()
```
次の例は、`utag.gdpr.getSelectedCategories()`によって返される`Array`を示しています：

```js
["analytics", "personalization"]
```

## `utag.gdpr.setAllCategories()`

すべてのカテゴリを同意したか拒否したかの同じ同意状態に構成し、（オプションで）同意を追跡するためにCollect APIを呼び出します。

```js
utag.gdpr.setAllCategories(state, noCollect)
```

| パラメータ | タイプ | 説明 |
| --- | --- | --- |
| `state` | `Boolean` | すべてのカテゴリに対する同意を許可するには`true`を構成し、同意を拒否するには`false`を構成します。 |
| `noCollect` | `Boolean` | （オプション）同意を追跡するためにCollect APIを呼び出さないようにするには`true`を構成します。 |

次の例は、すべてのカテゴリに対する同意を指定し、Collect APIへの呼び出しはありません：  
```js
utag.gdpr.setAllCategories(true,true)
```

次の例は、すべてのカテゴリに対する同意を拒否し、同意を追跡するためにCollect APIを呼び出します：
```js
utag.gdpr.setAllCategories(false)
```

## `utag.gdpr.setConsentValue()`

同意クッキーの値を有効または無効に構成します。この関数は同意のタイムスタンプを更新し、Collect APIへの追跡呼び出しを生成し、キュー`utag.gdpr.queue`に保持されているタグを再生します。


<blockquote>
`utag.gdpr.setConsentValue()`は個々のカテゴリの同意値を変更しません。同意値は関連するAPI呼び出し（`setPreferencesFromList()`または`setPreferencesValues()`）を介して無効にする必要があります。
</blockquote>


```js
utag.gdpr.setConsentValue(_response)
```

| パラメータ | タイプ | 説明 |
| --- | --- | --- |
| `_response` | `Boolean` | 同意を有効にするには`true`を構成し、同意を無効にするには`false`を構成します。 |

次の例は、クッキーの値を`"consent:true"`に構成し、タイムスタンプを更新します：  
```js
utag.gdpr.setConsentValue(true)
```
次の例は、クッキーの値を`"consent:false"`に構成し、タイムスタンプを更新します：  
```js
utag.gdpr.setConsentValue(0)
```

## `utag.gdpr.setCookie()`


<blockquote>
この関数を直接呼び出すことはお勧めしません。
</blockquote>


クッキー`Object`に直接書き込む内部関数です。同意状態、タイムスタンプ、部分的な同意のためのさまざまなカテゴリを表すために`Object`を使用します。自動的に正しいクッキー名と有効期限を使用します。

```js
utag.gdpr.setCookie(onlyEnabledCats)
```

| パラメータ | タイプ | 説明 |
| --- | --- | --- |
| `cookieData` | `Object` | 同意クッキーに保存されているデータを表すキー値のリスト。 |

例：

```js
var object = {"c6":"1","c1":"0","c2":"0","ts":1587133550264,"consent":"false","c3":"0","c4":"0","c5":"0","c7":"0","c8":"0","c9":"0","c10":"0","c11":"0","c12":"0","c13":"0","c14":"0","c15":"0"}

utag.gdpr.setCookie(object)
```

## `utag.gdpr.setCookieValue()`

同意クッキーの個々の値を構成します。


<blockquote>
この関数は、`setConsentValue()`などの他の高レベルの関数によって使用されます。この方法は慎重に使用し、初期のニーズを満たさない場合にのみ使用してください。
</blockquote>


```js
utag.gdpr.setCookieValue(key, value);
```

| パラメータ | タイプ | 説明 |
| --- | --- | --- |
| `key` | `String` | クッキーに構成されるキー。`consent`、`ts`、または`c`値表現によって指定されたカテゴリのいずれかに構成します。例えば、Analyticsの場合は`c1`、Affiliatesの場合は`c2`など。 |
| `value` | `String` | クッキーのキーに構成する値。 |

次の例は、同意クッキーを`"consent:false"`に構成します：  
```js
utag.gdpr.setCookieValue("consent", false);
```

次の例は、同意クッキーを`"c1:0"`に構成します：  
```js
utag.gdpr.setCookieValue("c1", 0);
```

## `utag.gdpr.setPreferencesFromList()`

パラメータで渡されたカテゴリのリストに対する同意状態を`allowed`に構成します。リストに含まれていないカテゴリの同意状態は`declined`に構成されます。これは部分的な同意のために使用されます。この関数は`setPreferencesValues()`関数に依存し、`getSelectedCategories()`の逆の機能を提供します。

```js
utag.gdpr.setPreferencesFromList(list)
```

| パラメータ | タイプ | 説明 |
| --- | --- | --- |
| `List` |`Array` | 有効なカテゴリの`Array`。 |

次の例は、同意クッキーの`"analytics"`カテゴリの同意状態を構成します：

```js
utag.gdpr.setPreferencesFromList(["analytics"])
```

## `utag.gdpr.setPreferencesValues()`

カテゴリとその同意状態の`Object`からクッキーの構成値を構成します。この関数は主に`setPreferencesFromList()`関数によって呼び出されます。この関数は、キュー`utag.gdpr.queue`に保持されているタグを再生します。

```js
utag.gdpr.setPreferencesValues(state, noCollect)
```

| パラメータ | タイプ | 説明 |
| --- | --- | --- |
| `state` | `Object` | `category:consentState`の形式のキー値ペア。 |
| `noCollect` | `Boolean` | （オプション）同意を追跡するためにCollect APIを呼び出さないようにするには`true`を構成します。 |

次の例は、`"analytics"`、`"affiliates"`、`"personalization"`カテゴリのクッキー値を構成します：  
```js
Var cats = {"analytics":"1","affiliates":"0","personalization":"0"}
utag.gdpr.setPreferencesValues(cats)
```

## `utag.gdpr.showConsentPreferences()`

同意の構成ポップアップを表示します。この関数は、ページ内のカスタマイズで定義されたCSS、HTML、JavaScriptを注入します。明示的な同意のJavaScriptリスナーから呼び出されるか、ユーザーが構成を変更したいページの任意のポイントから呼び出されます。

```js
utag.gdpr.showConsentPreferences(_lang)
```

| パラメータ | タイプ | 説明 |
| --- | --- | --- |
| `_lang` | `String` | オプション。ISO形式で指定された言語、例えば`en`や`en-gb`。 |

次の例は、デフォルトの言語またはデータレイヤーで構成された言語で同意を表示します：  
```js
utag.gdpr.showConsentPreferences()
```

次の例は、フランス語で同意を表示します：  
```js
utag.gdpr.showConsentPreferences("fr-fr")
```

## `utag.gdpr.showDoNotSellBanner()`

CCPAバナーを表示します。デフォルトでは、この関数は強制ルールが`true`に評価されたときに呼び出されます。

```js
utag.gdpr.showDoNotSellBanner(_lang)
```

| パラメータ | タイプ | 説明 |
| --- | --- | --- |
| `_lang` | `String` | オプション。ISO形式で指定された言語、例えば`en`や`en-gb`。 |

次の例は、デフォルトの言語またはデータレイヤーで構成された言語でCCPAバナーを表示します：  

```js
utag.gdpr.showDoNotSellBanner()
```

次の例は、フランス語でOpt-outバナーを表示します：  
```js
utag.gdpr.showDoNotSellBanner("fr-fr")
```

## `utag.gdpr.showDoNotSellPrompt()`

Opt-outポップアップを表示します。バナーを使用していない場合は、この関数をサイトのバナーに統合して、訪問が同意構成を変更する方法を提供します。

```js
utag.gdpr.showDoNotSellPrompt(_lang)
```

| パラメータ | タイプ | 説明 |
| --- | --- | --- |
| `_lang` | `String` | オプション。ISO形式で指定された言語、例えば`en`や`en-gb`。 |

次の例は、デフォルトの言語またはデータレイヤーで構成された言語でCCPAポップアップを表示します：  

```js
<a href="javascript: utag.gdpr.showDoNotSellPrompt()">同意を変更</a>
```

次の例は、フランス語でOpt-out Modelポップアップを表示します：  
```js
<a href="javascript: utag.gdpr.showDoNotSellPrompt('fr-fr')">同意を変更</a>
```

## `utag.gdpr.showExplicitConsent()`

明示的な同意ポップアップを表示します。この関数は、ページ内のカスタマイズで定義されたCSS、HTML、JavaScriptを注入します。明示的な同意が構成されている場合、Tealium Universal Tag `utag.js`によって`DOM READY`イベント時にネイティブに呼び出されます。

```js
utag.gdpr.showExplicitConsent(_lang)
```

| パラメータ | タイプ | 説明 |
| --- | --- | --- |
| `_lang` | `String` | （オプション）ISO形式で指定された言語、例えば`en`や`en-gb`。 |

次の例は、デフォルトの言語またはデータレイヤーで構成された言語で明示的な同意を表示します：   
```js
utag.gdpr.showExplicitConsent()
```
次の例は、フランス語で明示的な同意を表示します：  
```js
utag.gdpr.showExplicitConsent("fr-fr")
```

## `utag.gdpr.updateConsentCookie()`

隠されたwebviewを使用してアプリからモバイル同意を更新します。

```js
utag.gdpr.updateConsentCookie()
```

