---
title: Adjust Events API コネクタ構成ガイド
description: この記事では、Adjust Events API コネクタの構成方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/adjust-events-api-connector/
---
## コネクタアクション

| アクション名 | AudienceStream | EventStream |
| --- | :---: | :---: |
|イベント送信| ✗| ✓|

## 構成の構成

**コネクタマーケットプレイス**にアクセスし、新しいコネクタを追加します。コネクタを追加する一般的な手順については、[コネクタ概要]()の記事を参照してください。

コネクタを追加した後、以下の構成を構成します：

* **認証トークン**
  * AdjustのS2Sセキュリティ機能を使用すると、S2Sイベントのセキュリティを保証し、偽装リクエストから保護することができます。
  * S2S認証を構成した後、各受信リクエストにはAdjustダッシュボードで生成されたトークンが必要です。
  * 詳細については、[サーバー間（S2S）セキュリティ](https://help.adjust.com/en/article/server-to-server-s2s-security)を参照してください。
  * S2S認証を構成していない場合は、このフィールドを空白のままにしてください。

## アクション構成 - パラメータとオプション

**次へ**をクリックするか、**アクション**タブに進みます。ここでコネクタアクションを構成します。

このセクションでは、各アクションのパラメータとオプションの構成方法について説明します。

### アクション - イベント送信

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|イベントトークン|  &lt;ul&gt;&lt;li&gt;ダッシュボードからのAdjustイベントトークン。&lt;/li&gt;&lt;/ul&gt; |
|アプリトークン|  &lt;ul&gt;&lt;li&gt;ダッシュボードからのAdjustアプリトークン。&lt;/li&gt;&lt;/ul&gt; |
|Android ID|  &lt;ul&gt;&lt;li&gt;Android ID&lt;/li&gt;&lt;li&gt;[受け入れられるデバイス識別子](https://help.adjust.com/en/article/s2s-api-reference#accepted-identifiers)を参照。&lt;/li&gt;&lt;/ul&gt; |
|Open Advertising ID|  &lt;ul&gt;&lt;li&gt;プラットフォーム依存のOpen Advertising ID。&lt;/li&gt;&lt;li&gt;[受け入れられるデバイス識別子](https://help.adjust.com/en/article/s2s-api-reference#accepted-identifiers)を参照。&lt;/li&gt;&lt;/ul&gt; |
|Raw Amazon Fire Advertising ID|  &lt;ul&gt;&lt;li&gt;プラットフォーム依存のRaw Amazon Fire Advertising ID。&lt;/li&gt;&lt;li&gt;[受け入れられるデバイス識別子](https://help.adjust.com/en/article/s2s-api-reference#accepted-identifiers)を参照。&lt;/li&gt;&lt;/ul&gt; |
|Raw IDFA|  &lt;ul&gt;&lt;li&gt;iOS専用。&lt;/li&gt;&lt;li&gt;Raw IDFA識別子。&lt;/li&gt;&lt;li&gt;[受け入れられるデバイス識別子](https://help.adjust.com/en/article/s2s-api-reference#accepted-identifiers)を参照。&lt;/li&gt;&lt;/ul&gt; |
|Raw IDFV|  &lt;ul&gt;&lt;li&gt;Raw IDFV識別子。&lt;/li&gt;&lt;li&gt;[受け入れられるデバイス識別子](https://help.adjust.com/en/article/s2s-api-reference#accepted-identifiers)を参照。&lt;/li&gt;&lt;/ul&gt; |
|Raw Google Advertising ID|  &lt;ul&gt;&lt;li&gt;Raw Google Advertising ID識別子。&lt;/li&gt;&lt;li&gt;[受け入れられるデバイス識別子](https://help.adjust.com/en/article/s2s-api-reference#accepted-identifiers)を参照。&lt;/li&gt;&lt;/ul&gt; |
|Adjust Device ID|  &lt;ul&gt;&lt;li&gt;iOSでidfa情報なしでLATユーザーを識別する。&lt;/li&gt;&lt;/ul&gt; |
|作成時刻タイムスタンプ（フォーマット済み）|  &lt;ul&gt;&lt;li&gt;イベントが発生した正確な瞬間を伝える。&lt;/li&gt;&lt;li&gt;コネクタが値をエンコードします。&lt;/li&gt;&lt;li&gt;例：`2017-01-02T15:04:05.000&#43;0000` は `2017-01-02T15%3A04%3A05.000%2B0000` になります。&lt;/li&gt;&lt;/ul&gt; |
|作成時刻タイムスタンプ（Unix）|  &lt;ul&gt;&lt;li&gt;イベントが発生した正確な瞬間を伝える。&lt;/li&gt;&lt;li&gt;秒またはミリ秒を使用して指定可能です。&lt;/li&gt;&lt;/ul&gt; |
|IPアドレス|  &lt;ul&gt;&lt;li&gt;Googleなどの第三者へのイベントリンク（`city` や `postal_code` などの位置関連情報をコールバックに含める場合）。&lt;/li&gt;&lt;li&gt;`ip_address` パラメータはIPv4のみを受け入れます。&lt;/li&gt;&lt;li&gt;IPv6はまだサポートされていません。&lt;/li&gt;&lt;/ul&gt; |
|通貨|  &lt;ul&gt;&lt;li&gt;収益イベント&lt;/li&gt;&lt;li&gt;[通貨コード](https://help.adjust.com/en/article/supported-currencies)を参照。&lt;/li&gt;&lt;/ul&gt; |
|環境|  &lt;ul&gt;&lt;li&gt;データを投稿する環境。&lt;/li&gt;&lt;li&gt;例：`environment=sandbox` または `environment=production`&lt;/li&gt;&lt;li&gt;このパラメータが含まれていない場合、イベントは本番環境にプッシュされます。&lt;/li&gt;&lt;/ul&gt; |
|収益|  &lt;ul&gt;&lt;li&gt;完全な通貨単位での収益イベント値（149.99 = $149.99）。&lt;/li&gt;&lt;li&gt;Adjustはこのパラメータの最小値として0.001を受け入れます。&lt;/li&gt;&lt;/ul&gt; |
|テンプレート変数|  &lt;ul&gt;&lt;li&gt;データ入力としてテンプレート変数を提供します。&lt;/li&gt;&lt;li&gt;詳細については、を参照してください。&lt;/li&gt;&lt;li&gt;ドット表記でネストされたテンプレート変数を参照します。&lt;/li&gt;&lt;li&gt;例：`items.name`&lt;/li&gt;&lt;li&gt;ネストされたテンプレート変数は通常、データレイヤーリスト属性から構築されます。&lt;/li&gt;&lt;/ul&gt; |
|テンプレート|  &lt;ul&gt;&lt;li&gt;本文データで参照されるテンプレートを提供します。&lt;/li&gt;&lt;li&gt;詳細については、を参照してください。&lt;/li&gt;&lt;li&gt;テンプレートは名前で二重中括弧によってサポートされるフィールドに注入されます。&lt;/li&gt;&lt;li&gt;例：`{{SomeTemplateName}}`。&lt;/li&gt;&lt;/ul&gt; |
