---
title: トラッキング
description: ユーザー活動の追跡方法について学びます。
url: https://docs.tealium.com/ja/platforms/amp/track/
---
## ビューの追跡

基本的なインストールでは、ユーザーがAMPサイトの画面を開いたり、変更したりするたびに追跡コールが行われます。

この追跡に使用されるデータレイヤーをカスタマイズするには、変数のキーと値のペアで[extra URL Params](https://amp.dev/documentation/components/amp-analytics/?format=websites#extra-url-params) ブロック `extraUrlParams` を追加します：

```html
<amp-analytics type="tealiumcollect">
<script type="application/json">
{
  "vars": {
    "account": "ACCOUNT",
    "profile": "PROFILE",
    "datasource": "DATASOURCE"
  },
  "extraUrlParams": {
    "example_param1": "abc",
    "example_param2": 123
  }
}     
</script>
</amp-analytics>
```

| パラメータ | タイプ | 説明 |例 |
| --- | --- | --- | --- |
| `account` | `String` |Tealiumのアカウント名 | `"companyXYZ"` |
| `profile` | `String` |Tealiumのプロファイル名 | `"main"`  |
| `datasource` | `String` | データソースのキー  | `"abc123"` |


## イベントの追跡

`triggers` 構成オブジェクトは、追跡するイベントを定義します。トリガーは、トリガー名と構成のキーと値のペアとして定義されます。トリガー名は英数字の文字列で、構成はイベントのターゲットを決定します。

以下はトリガーの例です：

```json
"triggers": {
  "trigger_name": {
    "on": "VALUE",
    "selector": "VALUE",
    "request": "VALUE",
    "vars": {
      "tealium_event": "VALUE"
    }
    "extraUrlParams": {
      "extra_var": "${extraVar}"
    }
  }
}
```

AMPは以下の[`amp-analytics` triggers](https://www.ampproject.org/docs/reference/components/amp-analytics#triggers)をサポートしています。


## 動的追跡変数

イベントタイプ `visible` と `click`（`on` プロパティで使用）では、HTML5の要素属性を使用して `data-vars-*` の形式で動的追跡変数が渡されます。この方法で渡された変数はキャメルケースの命名に変換されます。

例えば、プロパティ `data-vars-link-name="register"` は、トリガーの `extraUrlParams` ブロックで参照される変数 `${linkName}` になります。

```json
"triggers": {
  "custom_click": {
    "on": "click",
    "selector": "#the-button",
    "request": "event",
    "vars": {
      "tealium_event": "custom_click"
    }
    "extraUrlParams": {
      "link_name": "${linkName}"
    }
  }
}
```

AMPは以下の[`amp-analytics` extra URL params](https://amp.dev/documentation/components/amp-analytics/?referrer=ampproject.org#extra-url-params)をサポートしています。

ボタンのHTML例：

```html
<span id="the-button" data-vars-link-name="register">
ボタンテキスト
</span>
```
