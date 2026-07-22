---
title: イベントログ
description: クライアントサイドの同意管理におけるイベントログの仕組みを学びます。
url: https://docs.tealium.com/ja/consent/client-side/consent-management/event-logging/
---
## 要件

* Tealium EventStream または [Tealium DataAccess](https://docs.tealium.com/about-dataaccess/) (EventStore または EventDB)

## 動作原理

イベントログ機能は、訪問によるすべての同意アクションを記録し、すべての[クライアントサイド同意管理](https://docs.tealium.com/about-consent-management/)オファリングで動作します。クライアントサイド同意管理があなたのサイトにデプロイされ、イベントログが有効になっている場合、同意アクションはHTTPリクエストとしてTealiumのサーバーサイドCDHに送信され、監査および記録保持の目的でEventStoreやEventDBでログ記録されたり、EventStreamでストリーミングされたりします。

以下の同意アクションが記録されます：

* 同意の付与または撤回
* 同意構成の変更
* **Do Not Sell** オプションの変更

関連製品にアクセスできる顧客の場合、これらのイベントはEventDBおよびEventStoreに保存されたり、EventStreamでストリーミングされたりすることができます（これらの特定のイベントには同意に基づくブロッキングが適用されません）。

独自のデータ収集エンドポイントを使用することを好む顧客の場合、カスタムURLを指定することができます。

## イベントログ構成

以下の構成が利用可能です：

* **Log Consent Changes** - すべての同意管理オファリングに対してイベントログを有効にするには**Yes**に構成します。
* **Event Log URL** - 同意変更をログするために使用されるイベント収集エンドポイント。独自のデータ収集エンドポイントを持っている場合のみこの構成を編集してください。
    デフォルト：
    ```bash
    https://collect.tealiumiq.com/event
    ```

* **Event Log Profile** - ログされたイベントが送信されるプロファイル。ここで構成された値はパラメータ `tealium_profile="PROFILE"` としてイベントログURLに渡されます。

[同意イベント](https://docs.tealium.com/consent-change-event-specifications/)のペイロードをカスタマイズするには、これらの2つのテンプレート `fullConsentEventHandler` と `partialConsentEventHandler` を編集します。テンプレートの更新についての詳細は、[テンプレートの管理](https://docs.tealium.com/about-templates/)を参照してください。