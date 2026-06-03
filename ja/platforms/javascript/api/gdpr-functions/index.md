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

`dns` 同意クッキーの値を構成します。認識される値：`true`、`false`、`1`、`0`、`&#34;true&#34;`、`&#34;false&#34;`。

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
[&#34;analytics&#34;, &#34;affiliates&#34;, &#34;display_ads&#34;, &#34;search&#34;, &#34;email&#34;, &#34;personalization&#34;, &#34;social&#34;, &#34;big_data&#34;, &#34;misc&#34;, &#34;cookiematch&#34;, &#34;cdp&#34;, &#34;mobile&#34;, &#34;engagement&#34;, &#34;monitoring&#34;, &#34;crm&#34;]
```

以下の例は、`utag.gdpr.getCategories()` が有効なカテゴリを返すときの結果を示しています：    
```js
[&#34;analytics&#34;, &#34;affiliates&#34;, &#34;personalization&#34;]
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

以下の例は、言語が英語の場合に `utag.gdpr.getCategoryLanguage(&#34;analytics&#34;)` によって返される `Object` を示しています：

```js
{name: &#34;Cookies that help us improve our website&#34;, notes: &#34;These cookies help us understand how people use our website.&#34;}
```
以下の例は、言語がポーランド語の場合に `utag.gdpr.getCategoryLanguage(&#34;analytics&#34;)` によって返される `Object` を示しています：

```js
{name: &#34;Pliki cookie dotyczące wydajności&#34;, notes: &#34;Te pliki cookie gromadzą informacje o tym, jak odw…dynie w celu ulepszania działania naszej witryny.&#34;}
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

部分的な同意が与えられた場合、`Object` の `Array` が返されます。各 `Object` は同意カテゴリを表します。`Array` 内の各 `Object` では、`&#34;ct&#34;` キーが同意値（`1`/`0`）を表し、`&#34;name&#34;` キーが同意カテゴリを指定します。

```js
utag.gdpr.getConsentState()
```

以下の例は、部分的な同意のために返される `Object` の `Array` を示しています：

```js
[{&#34;ct&#34;:&#34;1&#34;,&#34;name&#34;:&#34;analytics&#34;},
{&#34;ct&#34;:&#34;0&#34;,&#34;name&#34;:&#34;affiliates&#34;},
{&#34;ct&#34;:&#34;0&#34;,&#34;name&#34;:&#34;display_ads&#34;},
{&#34;ct&#34;:&#34;0&#34;,&#34;name&#34;:&#34;search&#34;},
{&#34;ct&#34;:&#34;0&#34;,&#34;name&#34;:&#34;email&#34;},
{&#34;ct&#34;:&#34;0&#34;,&#34;name&#34;:&#34;personalization&#34;},
{&#34;ct&#34;:&#34;0&#34;,&#34;name&#34;:&#34;social&#34;},
{&#34;ct&#34;:&#34;0&#34;,&#34;name&#34;:&#34;big_data&#34;},
{&#34;ct&#34;:&#34;0&#34;,&#34;name&#34;:&#34;misc&#34;},
{&#34;ct&#34;:&#34;0&#34;,&#34;name&#34;:&#34;cookiematch&#34;},
{&#34;ct&#34;:&#34;0&#34;,&#34;name&#34;:&#34;cdp&#34;},
{&#34;ct&#34;:&#34;0&#34;,&#34;name&#34;:&#34;mobile&#34;},
{&#34;ct&#34;:&#34;0&#34;,&#34;name&#34;:&#34;engagement&#34;},
{&#34;ct&#34;:&#34;0&#34;,&#34;name&#34;:&#34;monitoring&#34;},
{&#34;ct&#34;:&#34;0&#34;,&#34;name&#34;:&#34;crm&#34;}]
```

## `utag.gdpr.getCookieValues()`

この関数を直接使用する代わりに、クッキーを読み取るために `getCookieValues()` 関数を呼び出す `utag.gdpr.getConsentState()` のような関数を使用することをお勧めします。

同意クッキーをキーと値のペアとして表す `Object` を返します。この関数はデフォルトのクッキー名前空間（`CONSENTMGR`）を使用するか、`window.utag_cfg_ovrd.cmcookiens` で提供された値を使用します。逆の関数（クッキーに書き込む）は `utag.gdpr.setCookie()` です。

```js
utag.gdpr.getCookieValues()
```

以下の例は、部分的な同意のために `utag.gdpr.getCookieValues()` によって返される `Array` を示しています：  

```js
{
    &#34;c1&#34;:&#34;1&#34;,
    &#34;c2&#34;:&#34;0&#34;,
    &#34;c3&#34;:&#34;0&#34;,
    &#34;c4&#34;:&#34;0&#34;,
    &#34;c5&#34;:&#34;0&#34;,
    &#34;c6&#34;:&#34;0&#34;,
    &#34;c7&#34;:&#34;0&#34;,
    &#34;c8&#34;:&#34;0&#34;,
    &#34;C9&#34;:&#34;0&#34;,
    &#34;c10&#34;:&#34;0&#34;,
    &#34;c11&#34;:&#34;0&#34;,
    &#34;c12&#34;:&#34;0&#34;,
    &#34;c13&#34;:&#34;0&#34;,
    &#34;c14&#34;:&#34;0&#34;,
    &#34;c15&#34;:&#34;0&#34;,
    &#34;ts&#34;:&#34;1586965568213&#34;,
    &#34;consent&#34;:&#34;true&#34;
}
```
以下の例は、全面的な同意のために `utag.gdpr.getCookieValues()` によって返される `Array` を示しています：  
```js
utag.gdpr.getCategories(true)

{&#34;consent&#34;:&#34;true&#34;,&#34;ts&#34;:&#34;1587026030058&#34;}
```

## `utag.gdpr.getLanguage()`

同意マネージャーのコンテンツを表示するために使用される言語を `String` で返します。データレイヤーで構成された言語、ブラウザからの言語、またはデフォルトの言語の優先順位によります。

```js
utag.gdpr.getLanguage()
```

以下の例は、言語が英語（イギリス）の場合に返される `String` を示しています：

```js
&#34;en-gb&#34;
```

## `utag.gdpr.getSelectedCategories()`

顧客が選択したカテゴリを含む `Array` を返します。

```js
utag.gdpr.getSelectedCategories()
```
次の例は、`utag.gdpr.getSelectedCategories()`によって返される`Array`を示しています：

```js
[&#34;analytics&#34;, &#34;personalization&#34;]
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

`utag.gdpr.setConsentValue()`は個々のカテゴリの同意値を変更しません。同意値は関連するAPI呼び出し（`setPreferencesFromList()`または`setPreferencesValues()`）を介して無効にする必要があります。

```js
utag.gdpr.setConsentValue(_response)
```

| パラメータ | タイプ | 説明 |
| --- | --- | --- |
| `_response` | `Boolean` | 同意を有効にするには`true`を構成し、同意を無効にするには`false`を構成します。 |

次の例は、クッキーの値を`&#34;consent:true&#34;`に構成し、タイムスタンプを更新します：  
```js
utag.gdpr.setConsentValue(true)
```
次の例は、クッキーの値を`&#34;consent:false&#34;`に構成し、タイムスタンプを更新します：  
```js
utag.gdpr.setConsentValue(0)
```

## `utag.gdpr.setCookie()`

この関数を直接呼び出すことはお勧めしません。

クッキー`Object`に直接書き込む内部関数です。同意状態、タイムスタンプ、部分的な同意のためのさまざまなカテゴリを表すために`Object`を使用します。自動的に正しいクッキー名と有効期限を使用します。

```js
utag.gdpr.setCookie(onlyEnabledCats)
```

| パラメータ | タイプ | 説明 |
| --- | --- | --- |
| `cookieData` | `Object` | 同意クッキーに保存されているデータを表すキー値のリスト。 |

例：

```js
var object = {&#34;c6&#34;:&#34;1&#34;,&#34;c1&#34;:&#34;0&#34;,&#34;c2&#34;:&#34;0&#34;,&#34;ts&#34;:1587133550264,&#34;consent&#34;:&#34;false&#34;,&#34;c3&#34;:&#34;0&#34;,&#34;c4&#34;:&#34;0&#34;,&#34;c5&#34;:&#34;0&#34;,&#34;c7&#34;:&#34;0&#34;,&#34;c8&#34;:&#34;0&#34;,&#34;c9&#34;:&#34;0&#34;,&#34;c10&#34;:&#34;0&#34;,&#34;c11&#34;:&#34;0&#34;,&#34;c12&#34;:&#34;0&#34;,&#34;c13&#34;:&#34;0&#34;,&#34;c14&#34;:&#34;0&#34;,&#34;c15&#34;:&#34;0&#34;}

utag.gdpr.setCookie(object)
```

## `utag.gdpr.setCookieValue()`

同意クッキーの個々の値を構成します。

この関数は、`setConsentValue()`などの他の高レベルの関数によって使用されます。この方法は慎重に使用し、初期のニーズを満たさない場合にのみ使用してください。

```js
utag.gdpr.setCookieValue(key, value);
```

| パラメータ | タイプ | 説明 |
| --- | --- | --- |
| `key` | `String` | クッキーに構成されるキー。`consent`、`ts`、または`c`値表現によって指定されたカテゴリのいずれかに構成します。例えば、Analyticsの場合は`c1`、Affiliatesの場合は`c2`など。 |
| `value` | `String` | クッキーのキーに構成する値。 |

次の例は、同意クッキーを`&#34;consent:false&#34;`に構成します：  
```js
utag.gdpr.setCookieValue(&#34;consent&#34;, false);
```

次の例は、同意クッキーを`&#34;c1:0&#34;`に構成します：  
```js
utag.gdpr.setCookieValue(&#34;c1&#34;, 0);
```

## `utag.gdpr.setPreferencesFromList()`

パラメータで渡されたカテゴリのリストに対する同意状態を`allowed`に構成します。リストに含まれていないカテゴリの同意状態は`declined`に構成されます。これは部分的な同意のために使用されます。この関数は`setPreferencesValues()`関数に依存し、`getSelectedCategories()`の逆の機能を提供します。

```js
utag.gdpr.setPreferencesFromList(list)
```

| パラメータ | タイプ | 説明 |
| --- | --- | --- |
| `List` |`Array` | 有効なカテゴリの`Array`。 |

次の例は、同意クッキーの`&#34;analytics&#34;`カテゴリの同意状態を構成します：

```js
utag.gdpr.setPreferencesFromList([&#34;analytics&#34;])
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

次の例は、`&#34;analytics&#34;`、`&#34;affiliates&#34;`、`&#34;personalization&#34;`カテゴリのクッキー値を構成します：  
```js
Var cats = {&#34;analytics&#34;:&#34;1&#34;,&#34;affiliates&#34;:&#34;0&#34;,&#34;personalization&#34;:&#34;0&#34;}
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
utag.gdpr.showConsentPreferences(&#34;fr-fr&#34;)
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
utag.gdpr.showDoNotSellBanner(&#34;fr-fr&#34;)
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
&lt;a href=&#34;javascript: utag.gdpr.showDoNotSellPrompt()&#34;&gt;同意を変更&lt;/a&gt;
```

次の例は、フランス語でOpt-out Modelポップアップを表示します：  
```js
&lt;a href=&#34;javascript: utag.gdpr.showDoNotSellPrompt(&#39;fr-fr&#39;)&#34;&gt;同意を変更&lt;/a&gt;
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
utag.gdpr.showExplicitConsent(&#34;fr-fr&#34;)
```

## `utag.gdpr.updateConsentCookie()`

隠されたwebviewを使用してアプリからモバイル同意を更新します。

```js
utag.gdpr.updateConsentCookie()
```

