---
title: データソース: インストールとテスト
description: HTTP APIのインストールとテストは、ブラウザにURLを入力するだけの簡単な操作です。データソースに別のプラットフォームを選択した場合は、インストール手順に従って必要なコードを追加してください。
url: https://docs.tealium.com/ja/server-side/getting-started/eventstream-api-hub/install-test/
---
## テストイベントの送信

イベントはEventStreamで`tealium_event`属性によって識別されます。テストイベントとして、`search`というイベントを送信します。

`GET`メソッドを使用すると、テストイベントのURLは次のようになります（可読性のために改行を追加）：

```none
https://collect.tealiumiq.com/event?
tealium_account=your_account
&amp;tealium_profile=your_profile
&amp;tealium_datasource=abc123
&amp;tealium_event=search
```

対応するSwift（iOS）のコードは次のようになるかもしれません：

```swift
var tealConfig = TealiumConfig(
    account: &#34;your_account&#34;,
    profile: &#34;your_profile&#34;,
    environment: &#34;prod&#34;,
    datasource: &#34;abc123&#34;)

let tealium = Tealium(config: tealConfig)

// トラッキングされたイベント &#34;search&#34; は自動的に以下の結果を生み出します：
// tealium_event : &#34;search&#34; in the event data
tealium?.trackEventWithTitle(&#34;search&#34;, dataSources: [:])
```

次のステップに進んで、**Live Events**画面でこれらのテストイベントをどのように観察するかを見てみましょう。