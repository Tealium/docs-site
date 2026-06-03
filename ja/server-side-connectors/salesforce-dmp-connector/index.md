---
title: Salesforce DMPコネクタ構成ガイド
description: この記事では、Salesforce DMPコネクタの構成方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/salesforce-dmp-connector/
---
## コネクタアクション

| アクション名 | AudienceStream | EventStream |
| --- | :---: | :---: |
|ユーザー属性の追跡| ✓| ✓|
|ユーザーをストリーミングセグメントに追加| ✓| ✓|
|ユーザーをストリーミングセグメントから削除| ✓| ✓|

## 構成の構成

コネクタマーケットプレイスにアクセスし、新しいコネクタを追加します。コネクタの追加方法については、[コネクタ概要]()の記事を参照してください。

コネクタを追加した後、以下の構成を構成します：

## アクション構成 - パラメータとオプション

**Next**をクリックするか、**Actions**タブに進みます。ここでコネクタアクションを構成します。

このセクションでは、各アクションのパラメータとオプションの構成方法について説明します。

### アクション - ユーザー属性の追跡

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|エンドポイントURL|  &lt;ul&gt;&lt;li&gt;(必須) Salesforce DMP担当者から提供されるイベントデータを送信するイベントURL。&lt;/li&gt;&lt;li&gt;あなたのエンドポイントは次のようになるかもしれません：`https://beacon.krxd.net/pixel.gif?tech_browser_lang=en`&lt;/li&gt;&lt;li&gt;Salesforce DMP担当者にイベントURLを問い合わせてください。&lt;/li&gt;&lt;li&gt;詳細については、次の[APIドキュメント](https://konsole.zendesk.com/hc/en-us/articles/219493027-Mobile-HTTP-API)を参照してください。&lt;/li&gt;&lt;/ul&gt; |
|Krux Publisher uuid|  &lt;ul&gt;&lt;li&gt;Salesforce DMP担当者に連絡して、公開社の`uuid`を取得してください。&lt;/li&gt;&lt;li&gt;詳細については、次の[APIドキュメント](https://konsole.zendesk.com/hc/en-us/articles/219493027-Mobile-HTTP-API)を参照してください。&lt;/li&gt;&lt;/ul&gt; |
|Krux Domain ID|  &lt;ul&gt;&lt;li&gt;Salesforce DMP担当者に連絡して、この値を取得してください。&lt;/li&gt;&lt;li&gt;詳細については、次の[APIドキュメント](https://konsole.zendesk.com/hc/en-us/articles/219493027-Mobile-HTTP-API)を参照してください。&lt;/li&gt;&lt;/ul&gt; |
|Krux Site ID|  &lt;ul&gt;&lt;li&gt;Salesforce DMP担当者に連絡して、この値を取得してください。&lt;/li&gt;&lt;li&gt;詳細については、次の[APIドキュメント](https://konsole.zendesk.com/hc/en-us/articles/219493027-Mobile-HTTP-API)を参照してください。&lt;/li&gt;&lt;/ul&gt; |
|Krux User ID|  &lt;ul&gt;&lt;li&gt;ユーザーを追跡するためのユニークなユーザーID。iOSの場合、これはユニークな広告主IDである必要があります（デバイスIDではありません）。&lt;/li&gt;&lt;li&gt;ユーザーIDの取得方法については、次の[記事]()を参照してください。&lt;/li&gt;&lt;/ul&gt; |
|ユーザー属性|  &lt;ul&gt;&lt;li&gt;送信する必要があるすべてのユーザー属性データには、`_kua_`のプレフィックスを付ける必要があります。例：`_kua_{user_attribute_name}`&lt;/li&gt;&lt;li&gt;注：ピクセル呼び出しで単一の属性に複数の属性値を渡す場合は、値をカンマで区切って渡すことを確認してください。&lt;/li&gt;&lt;/ul&gt; |

### アクション - ユーザーをストリーミングセグメントに追加

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|エンドポイントURL|  &lt;ul&gt;&lt;li&gt;(必須) セグメントデータを配信するためにSalesforce DMP担当者から提供されるセグメントURL。&lt;/li&gt;&lt;li&gt;あなたのエンドポイントは次のようになるかもしれません：`https://beacon.krxd.net/segment.gif`&lt;/li&gt;&lt;li&gt;詳細については、次の[APIドキュメント](https://konsole.zendesk.com/hc/en-us/articles/115012370488-Segments-Streaming-Segments-Implementation)を参照してください。&lt;/li&gt;&lt;/ul&gt; |
|セグメント|  &lt;ul&gt;&lt;li&gt;カンマ区切りのユーザーセグメント長uidリスト（セグメント長uidはストリーミングセグメント作成APIへの応答で返されます）（segs）。&lt;/li&gt;&lt;li&gt;ストリーミングセグメントはオフサイトアクティベーションのみです。&lt;/li&gt;&lt;li&gt;ストリーミングセグメントをcurlを使用して作成する方法については、次の[記事]を参照してください。(https://konsole.zendesk.com/hc/en-us/articles/115012370488-Segments-Streaming-Segments-Implementation)&lt;/li&gt;&lt;/ul&gt; |
|Krux Publisher uuid|  &lt;ul&gt;&lt;li&gt;Salesforce DMP担当者に連絡して、公開社の`uuid`を取得してください。&lt;/li&gt;&lt;li&gt;詳細については、次の[APIドキュメント](https://konsole.zendesk.com/hc/en-us/articles/219493027-Mobile-HTTP-API)を参照してください。&lt;/li&gt;&lt;/ul&gt; |
|Krux User ID|  &lt;ul&gt;&lt;li&gt;ユーザーを追跡するためのユニークなユーザーID（`_kuid`）。iOSの場合、これはユニークな広告主IDである必要があります（デバイスIDではありません）。&lt;/li&gt;&lt;li&gt;`fpuid`または`_kuid`のいずれかを提供することができます。`_fpuid`が提供された場合、ユーザーマッチルックアップに基づいてユーザーが一致します。それ以外の場合は、kuidが使用され、ルックアップは必要ありません。&lt;/li&gt;&lt;li&gt;ユーザーIDの取得方法については、次の[記事]()を参照してください。&lt;/li&gt;&lt;/ul&gt; |
|Krux Single First Party uid|  &lt;ul&gt;&lt;li&gt;シングルファーストパーティuid（`fpuid`）。&lt;/li&gt;&lt;li&gt;`fpuid`または`_kuid`のいずれかを提供することができます。`_fpuid`が提供された場合、ユーザーマッチルックアップに基づいてユーザーが一致します。それ以外の場合は、kuidが使用され、ルックアップは必要ありません。&lt;/li&gt;&lt;li&gt;ユーザーIDの取得方法については、次の[記事]()を参照してください。&lt;/li&gt;&lt;li&gt;詳細については、次の[情報]を参照してください。(https://konsole.zendesk.com/hc/en-us/articles/115012370488-Segments-Streaming-Segments-Implementation)&lt;/li&gt;&lt;/ul&gt; |

### アクション - ユーザーをストリーミングセグメントから削除

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|エンドポイントURL|  &lt;ul&gt;&lt;li&gt;(必須) セグメントデータを配信するためにSalesforce DMP担当者から提供されるセグメントURL。&lt;/li&gt;&lt;li&gt;あなたのエンドポイントは次のようになるかもしれません：`https://beacon.krxd.net/segment.gif`&lt;/li&gt;&lt;li&gt;詳細については、次の[APIドキュメント](https://konsole.zendesk.com/hc/en-us/articles/115012370488-Segments-Streaming-Segments-Implementation)を参照してください。&lt;/li&gt;&lt;/ul&gt; |
|セグメント|  &lt;ul&gt;&lt;li&gt;カンマ区切りのユーザーセグメント長uidリスト（セグメント長uidはストリーミングセグメント作成APIへの応答で返されます）（segs）。&lt;/li&gt;&lt;li&gt;ストリーミングセグメントはオフサイトアクティベーションのみです。&lt;/li&gt;&lt;li&gt;ストリーミングセグメントをcurlを使用して作成する方法については、次の[記事]を参照してください。(https://konsole.zendesk.com/hc/en-us/articles/115012370488-Segments-Streaming-Segments-Implementation)&lt;/li&gt;&lt;/ul&gt; |
|Krux Publisher uuid|  &lt;ul&gt;&lt;li&gt;Salesforce DMP担当者に連絡して、公開社のuuidを取得してください。&lt;/li&gt;&lt;li&gt;詳細については、次の[APIドキュメント](https://konsole.zendesk.com/hc/en-us/articles/219493027-Mobile-HTTP-API)を参照してください。&lt;/li&gt;&lt;/ul&gt; |
|Krux User ID|  &lt;ul&gt;&lt;li&gt;ユーザーを追跡するためのユニークなユーザーID（`_kuid`）。iOSの場合、これはユニークな広告主IDである必要があります（デバイスIDではありません）。&lt;/li&gt;&lt;li&gt;`fpuid`または`_kuid`のいずれかを提供することができます。`_fpuid`が提供された場合、ユーザーマッチルックアップに基づいてユーザーが一致します。それ以外の場合は、`kuid`が使用され、ルックアップは必要ありません。&lt;/li&gt;&lt;li&gt;ユーザーIDの取得方法については、次の[記事]()を参照してください。&lt;/li&gt;&lt;/ul&gt; |
|Krux Single First Party uid|  &lt;ul&gt;&lt;li&gt;シングルファーストパーティ`uid`（`fpuid`）。&lt;/li&gt;&lt;li&gt;`fpuid`または`_kuid`のいずれかを提供することができます。`_fpuid`が提供された場合、ユーザーマッチルックアップに基づいてユーザーが一致します。それ以外の場合は、`kuid`が使用され、ルックアップは必要ありません。&lt;/li&gt;&lt;li&gt;ユーザーIDの取得方法については、次の[記事]()を参照してください。&lt;/li&gt;&lt;li&gt;詳細については、次の[情報]を参照してください。(https://konsole.zendesk.com/hc/en-us/articles/115012370488-Segments-Streaming-Segments-Implementation)&lt;/li&gt;&lt;/ul&gt; |
