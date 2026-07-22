---
title: 同意管理
description: リモートコマンドでの同意管理の実装を学びます。
url: https://docs.tealium.com/ja/platforms/remote-commands/consent-management/
---
Tealiumのモバイルライブラリで[同意管理](https://docs.tealium.com/ja/platforms/getting-started-mobile/consent-management/)を有効にすると、ユーザーがトラッキングに同意するまで、デバイスからのトラッキングデータは送信されません。ユーザーの同意は、リモートコマンドと、アプリに統合されたサードパーティのベンダーSDKでも強制される必要があります。以下のシナリオでは、リモートコマンドでの同意の取り扱い方法を説明します。

## 同意シナリオ

アプリでユーザーに同意を求めるとき、デバイスから送信されるトラッキングデータを決定する3つの可能なシナリオがあります：

* ユーザーがすべてのトラッキングを拒否する
* ユーザーがすべてのトラッキングに同意する
* ユーザーが部分的なトラッキングに同意する

### ユーザーがすべてのトラッキングを拒否する

ユーザーがすべてのトラッキングに同意を拒否すると、Tealiumのモバイルライブラリは、デバイスからのすべての標準的なトラッキングリクエストを防ぎます。ただし、**リモートAPI**オプションが有効になっている場合、特別なイベントタイプ`remote_api`を持つ追加の呼び出しを生成します。この呼び出しは、すべてのオフラインキューイングと同意制限を無視します。

`remote_api`呼び出しは、Tealium iQ経由でロードされたJavaScriptタグや、AudienceStreamやEventStreamなどのTealiumのサーバーサイド製品にはデータを送信しません。代わりに、以下のリモートコマンドをトリガーするために使用されます：

* アプリの必要な機能をサポートする機能的なリモートコマンド。
* 組み込みの同意および/またはオフラインキューイングサポートを持つサードパーティのSDKからのリモートコマンド、これらはアプリイベントのフィルタリングされていないストリームを期待しています。

### ユーザーがすべてのトラッキングに同意する

ユーザーがすべてのトラッキングに同意すると、任意のリモートコマンドがトリガーできます。同意が得られると、Tealiumライブラリはリモートコマンドを初期化し、マッピングされたイベントとデータがベンダーSDKに送信されます。

一部のベンダーSDKでは、リモートコマンドがトリガーされる前にオプトインコマンドを呼び出す必要があります。具体的なコマンドについては、各[ベンダー統合](https://docs.tealium.com/ja/platforms/remote-commands/integrations/)を参照してください。

### ユーザーが部分的なトラッキングに同意する

ユーザーが特定のカテゴリーに部分的な同意を与える場合、以下が適用されます：

* `grant_partial_consent`イベントが`consent_categories`属性とともに送信されます。
* すべてのJSONリモートコマンドがトリガーされます。
* リモートコマンドタグは、ユーザーが同意したカテゴリーのいずれかに割り当てられている場合、またはタグが同意から省略されている場合にのみトリガーされます。

[同意カテゴリー](https://docs.tealium.com/ja/iq-tag-management/consent-management/consent-preferences-dialog/manage/)と[同意イベント仕様](https://docs.tealium.com/consent-change-event-specifications/)について詳しく学びましょう。

## リモートAPI呼び出し

**リモートAPI**オプションがリモートコマンドにどのように影響するかは、リモートコマンドがJSON構成ファイルを使用して実装されているか、Tealium iQを経由して実装されているかによります。

### JSONリモートコマンド

`remote_api`呼び出しは、JSONファイルを使用して構成されたすべてのリモートコマンドをトリガーします。すべてのマッピングロジックが適用され、コマンドが実行されます。JSON構成ファイルを使用してベンダーSDKで同意を強制するには、Tealiumの同意イベントをサポートされているベンダーメソッドにマップします。

この例では、Brazeで、Tealiumの同意イベントがAndroidのベンダー同意メソッドにマップされています：

```json
{
  "commands": {
    "grant_full_consent": "enableSDK",
    "decline_consent": "disableSDK,wipeData"
  }
}
```

[JSON構成マッピング](https://docs.tealium.com/ja/platforms/remote-commands/vendor-integrations/#mappings)について詳しく学びましょう。

### リモートコマンドタグ

同意イベントをリモートコマンドタグに送信するには、タグを`remote_api`イベントを期待するように構成する必要があります。デフォルトでは、タグは`view`と`link`呼び出しを期待するように構成されています。

タグを`remote_api`呼び出しを期待するように更新するには、次のようにイベントのリストを変更します：
```javascript
u.ev = { remote_api: 1 }; // remove "view" and "link" to avoid double-counting when remote_api is enabled
```

次の例は、Braze Mobile Remote Commandタグでトラッキングを無効にする方法を示しています。`tealium_event`変数をBrazeコマンド`Disable Data Collection (disableSDK)`にマップします。
[同意イベント仕様](https://docs.tealium.com/consent-change-event-specifications/)について詳しく学びましょう。

![](https://docs.tealium.com/images/platforms/remote-commands/remote-command-tag-mapping-consent.png)

タグがどのイベントをリッスンするように構成されているかを確認する方法についての詳細は、[タグが'View'または'Link' Callsで発火するかどうかを確認する方法](https://support.tealiumiq.com/en/support/solutions/articles/36000363410-how-to-check-if-a-tag-will-fire-on-view-or-link-calls)を参照してください。

## ベンダー固有の同意構成

各ベンダーSDKは同意を異なる方法で管理します。各ベンダーSDKの同意オプションの構成方法についての詳細は、[リモートコマンド統合](https://docs.tealium.com/ja/platforms/remote-commands/integrations/)のベンダー固有のリモートコマンドドキュメンテーションを参照してください。


