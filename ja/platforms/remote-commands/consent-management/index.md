---
title: 同意管理
description: リモートコマンドで同意管理を実装する方法について説明します。
url: https://docs.tealium.com/ja/platforms/remote-commands/consent-management/
---
Tealiumモバイルライブラリで[同意管理](https://docs.tealium.com/ja/platforms/getting-started-mobile/consent-management/)を有効にすると、デバイスからトラッキングデータが送信される前に、ユーザーがトラッキングに同意する必要があります。ユーザーの同意は、リモートコマンドおよびアプリに統合されているサードパーティベンダーのSDKにも適用する必要があります。以下のシナリオでは、リモートコマンドで同意を処理する方法について説明します。

## 同意のシナリオ

アプリでユーザーに同意を求める場合、デバイスから送信されるトラッキングデータを決定するシナリオは3つあります。

* ユーザーがすべてのトラッキングを拒否する
* ユーザーがすべてのトラッキングに同意する
* ユーザーが一部のトラッキングに同意する

### ユーザーがすべてのトラッキングを拒否する場合

ユーザーがすべてのトラッキングへの同意を拒否すると、Tealiumモバイルライブラリは、すべての標準トラッキングリクエストがデバイス外部やリモートコマンドに送信されるのを防止します。ただし、**Remote API**オプションが有効な場合は、特殊なイベントタイプ`remote_api`を含む追加の呼び出しが生成されます。この呼び出しでは、オフラインキューと同意に関するすべての制限が無視されます。

`remote_api`呼び出しでは、タグ管理によって読み込まれたJavaScriptタグや、Customer Data Platform（CDP）またはEvent StreamingなどのTealiumサーバーサイド製品にデータは送信されません。代わりに、次のリモートコマンドをトリガーするために使用されます。

* 機能用リモートコマンド（アプリで必要な機能をサポートするものなど）。
* 同意やオフラインキューを組み込みでサポートし、フィルタリングされていないアプリイベントのストリームを必要とするサードパーティSDKのリモートコマンド。

### ユーザーがすべてのトラッキングに同意する場合

ユーザーがすべてのトラッキングに同意すると、すべてのリモートコマンドをトリガーできます。同意が得られると、Tealiumライブラリはリモートコマンドを初期化し、マッピングされたイベントとデータがベンダーSDKに送信されます。

一部のベンダーSDKでは、リモートコマンドがトリガーされる前にオプトインコマンドを呼び出す必要があります。具体的なコマンドについては、各[ベンダー統合](https://docs.tealium.com/ja/platforms/remote-commands/integrations/)を参照してください。

### ユーザーが一部のトラッキングに同意する場合

ユーザーが特定のカテゴリに対して部分的な同意を付与した場合、次の処理が適用されます。

* `grant_partial_consent`イベントが`consent_categories`属性とともに送信されます。
* すべてのJSONリモートコマンドがトリガーされます。
* リモートコマンドタグは、ユーザーが同意したカテゴリのいずれかに割り当てられている場合、またはそのタグが同意の対象外に構成されている場合にのみトリガーされます。

[同意カテゴリ](https://docs.tealium.com/ja/iq-tag-management/consent-management/consent-preferences-dialog/manage/)および[同意イベントの仕様](https://docs.tealium.com/consent-change-event-specifications/)の詳細を確認してください。

## Remote API呼び出し

**Remote API**オプションがリモートコマンドに与える影響は、そのリモートコマンドがJSON構成ファイルとタグ管理のどちらを使用して実装されているかによって異なります。

### JSONリモートコマンド

`remote_api`呼び出しは、JSONファイルを使用して構成されたすべてのリモートコマンドをトリガーします。すべてのマッピングロジックが適用され、コマンドが実行されます。JSON構成ファイルを使用してベンダーSDKに同意を適用するには、Tealiumの同意イベントを、ベンダーがサポートするメソッドにマッピングします。

次のBrazeの例では、Tealiumの同意イベントをAndroid向けのベンダー同意メソッドにマッピングしています。

```json
{
  "commands": {
    "grant_full_consent": "enableSDK",
    "decline_consent": "disableSDK,wipeData"
  }
}
```

[JSON構成のマッピング](https://docs.tealium.com/ja/platforms/remote-commands/vendor-integrations/#mappings)の詳細を確認してください。

### リモートコマンドタグ

同意イベントをリモートコマンドタグに送信するには、`remote_api`イベントを受け取るようにタグを構成する必要があります。デフォルトでは、タグは`view`および`link`呼び出しのみを受け取るように構成されています。

`remote_api`呼び出しを受け取るようにタグを更新するには、イベントのリストを次のように変更します。

```javascript
u.ev = { remote_api: 1 }; // remove "view" and "link" to avoid double-counting when remote_api is enabled
```

次の例は、Braze Mobile Remote Commandタグでトラッキングを無効にする方法を示しています。`tealium_event`変数をBrazeコマンド`Disable Data Collection (disableSDK)`にマッピングします。  
[同意イベントの仕様](https://docs.tealium.com/consent-change-event-specifications/)の詳細を確認してください。

![](https://docs.tealium.com/images/platforms/remote-commands/remote-command-tag-mapping-consent.png)

タグがどのイベントをリッスンするように構成されているかを確認する方法については、[タグが「View」または「Link」呼び出しで実行されるかを確認する方法](https://support.tealiumiq.com/en/support/solutions/articles/36000363410-how-to-check-if-a-tag-will-fire-on-view-or-link-calls)を参照してください。

## ベンダー固有の同意構成

同意の管理方法はベンダーSDKごとに異なります。各ベンダーSDKの同意オプションを構成する方法については、[リモートコマンド統合](https://docs.tealium.com/ja/platforms/remote-commands/integrations/)にあるベンダー固有のリモートコマンドドキュメントを参照してください。