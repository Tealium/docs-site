---
title: トラッキング
description: ユーザー活動の追跡方法について学びます。
url: https://docs.tealium.com/ja/platforms/amp/track/
---
## ビューの追跡

基本的なインストールでは、ユーザーがAMPサイトの画面を開いたり、変更したりするたびに追跡コールが行われます。

この追跡に使用されるデータレイヤーをカスタマイズするには、変数のキーと値のペアで[extra URL Params](https://amp.dev/documentation/components/amp-analytics/?format=websites#extra-url-params) ブロック `extraUrlParams` を追加します：

```html
&lt;amp-analytics type=&#34;tealiumcollect&#34;&gt;
&lt;script type=&#34;application/json&#34;&gt;
{
  &#34;vars&#34;: {
    &#34;account&#34;: &#34;ACCOUNT&#34;,
    &#34;profile&#34;: &#34;PROFILE&#34;,
    &#34;datasource&#34;: &#34;DATASOURCE&#34;
  },
  &#34;extraUrlParams&#34;: {
    &#34;example_param1&#34;: &#34;abc&#34;,
    &#34;example_param2&#34;: 123
  }
}     
&lt;/script&gt;
&lt;/amp-analytics&gt;
```

| パラメータ | タイプ | 説明 |例 |
| --- | --- | --- | --- |
| `account` | `String` |Tealiumのアカウント名 | `&#34;companyXYZ&#34;` |
| `profile` | `String` |Tealiumのプロファイル名 | `&#34;main&#34;`  |
| `datasource` | `String` | データソースのキー  | `&#34;abc123&#34;` |


## イベントの追跡

`triggers` 構成オブジェクトは、追跡するイベントを定義します。トリガーは、トリガー名と構成のキーと値のペアとして定義されます。トリガー名は英数字の文字列で、構成はイベントのターゲットを決定します。

以下はトリガーの例です：

```json
&#34;triggers&#34;: {
  &#34;trigger_name&#34;: {
    &#34;on&#34;: &#34;VALUE&#34;,
    &#34;selector&#34;: &#34;VALUE&#34;,
    &#34;request&#34;: &#34;VALUE&#34;,
    &#34;vars&#34;: {
      &#34;tealium_event&#34;: &#34;VALUE&#34;
    }
    &#34;extraUrlParams&#34;: {
      &#34;extra_var&#34;: &#34;${extraVar}&#34;
    }
  }
}
```

AMPは以下の[`amp-analytics` triggers](https://www.ampproject.org/docs/reference/components/amp-analytics#triggers)をサポートしています。


## 動的追跡変数

イベントタイプ `visible` と `click`（`on` プロパティで使用）では、HTML5の要素属性を使用して `data-vars-*` の形式で動的追跡変数が渡されます。この方法で渡された変数はキャメルケースの命名に変換されます。

例えば、プロパティ `data-vars-link-name=&#34;register&#34;` は、トリガーの `extraUrlParams` ブロックで参照される変数 `${linkName}` になります。

```json
&#34;triggers&#34;: {
  &#34;custom_click&#34;: {
    &#34;on&#34;: &#34;click&#34;,
    &#34;selector&#34;: &#34;#the-button&#34;,
    &#34;request&#34;: &#34;event&#34;,
    &#34;vars&#34;: {
      &#34;tealium_event&#34;: &#34;custom_click&#34;
    }
    &#34;extraUrlParams&#34;: {
      &#34;link_name&#34;: &#34;${linkName}&#34;
    }
  }
}
```

AMPは以下の[`amp-analytics` extra URL params](https://amp.dev/documentation/components/amp-analytics/?referrer=ampproject.org#extra-url-params)をサポートしています。

ボタンのHTML例：

```html
&lt;span id=&#34;the-button&#34; data-vars-link-name=&#34;register&#34;&gt;
ボタンテキスト
&lt;/span&gt;
```
