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

**コネクタマーケットプレイス**にアクセスし、新しいコネクタを追加します。コネクタを追加する一般的な手順については、[コネクタ概要](https://docs.tealium.com/about-connectors/)の記事を参照してください。

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
|イベントトークン|  <ul><li>ダッシュボードからのAdjustイベントトークン。</li></ul> |
|アプリトークン|  <ul><li>ダッシュボードからのAdjustアプリトークン。</li></ul> |
|Android ID|  <ul><li>Android ID</li><li>[受け入れられるデバイス識別子](https://help.adjust.com/en/article/s2s-api-reference#accepted-identifiers)を参照。</li></ul> |
|Open Advertising ID|  <ul><li>プラットフォーム依存のOpen Advertising ID。</li><li>[受け入れられるデバイス識別子](https://help.adjust.com/en/article/s2s-api-reference#accepted-identifiers)を参照。</li></ul> |
|Raw Amazon Fire Advertising ID|  <ul><li>プラットフォーム依存のRaw Amazon Fire Advertising ID。</li><li>[受け入れられるデバイス識別子](https://help.adjust.com/en/article/s2s-api-reference#accepted-identifiers)を参照。</li></ul> |
|Raw IDFA|  <ul><li>iOS専用。</li><li>Raw IDFA識別子。</li><li>[受け入れられるデバイス識別子](https://help.adjust.com/en/article/s2s-api-reference#accepted-identifiers)を参照。</li></ul> |
|Raw IDFV|  <ul><li>Raw IDFV識別子。</li><li>[受け入れられるデバイス識別子](https://help.adjust.com/en/article/s2s-api-reference#accepted-identifiers)を参照。</li></ul> |
|Raw Google Advertising ID|  <ul><li>Raw Google Advertising ID識別子。</li><li>[受け入れられるデバイス識別子](https://help.adjust.com/en/article/s2s-api-reference#accepted-identifiers)を参照。</li></ul> |
|Adjust Device ID|  <ul><li>iOSでidfa情報なしでLATユーザーを識別する。</li></ul> |
|作成時刻タイムスタンプ（フォーマット済み）|  <ul><li>イベントが発生した正確な瞬間を伝える。</li><li>コネクタが値をエンコードします。</li><li>例：`2017-01-02T15:04:05.000+0000` は `2017-01-02T15%3A04%3A05.000%2B0000` になります。</li></ul> |
|作成時刻タイムスタンプ（Unix）|  <ul><li>イベントが発生した正確な瞬間を伝える。</li><li>秒またはミリ秒を使用して指定可能です。</li></ul> |
|IPアドレス|  <ul><li>Googleなどの第三者へのイベントリンク（`city` や `postal_code` などの位置関連情報をコールバックに含める場合）。</li><li>`ip_address` パラメータはIPv4のみを受け入れます。</li><li>IPv6はまだサポートされていません。</li></ul> |
|通貨|  <ul><li>収益イベント</li><li>[通貨コード](https://help.adjust.com/en/article/supported-currencies)を参照。</li></ul> |
|環境|  <ul><li>データを投稿する環境。</li><li>例：`environment=sandbox` または `environment=production`</li><li>このパラメータが含まれていない場合、イベントは本番環境にプッシュされます。</li></ul> |
|収益|  <ul><li>完全な通貨単位での収益イベント値（149.99 = $149.99）。</li><li>Adjustはこのパラメータの最小値として0.001を受け入れます。</li></ul> |
|テンプレート変数|  <ul><li>データ入力としてテンプレート変数を提供します。</li><li>詳細については、[connector-template-variables](https://docs.tealium.com/connector-template-variables/)を参照してください。</li><li>ドット表記でネストされたテンプレート変数を参照します。</li><li>例：`items.name`</li><li>ネストされたテンプレート変数は通常、データレイヤーリスト属性から構築されます。</li></ul> |
|テンプレート|  <ul><li>本文データで参照されるテンプレートを提供します。</li><li>詳細については、[about-connector-templates](https://docs.tealium.com/about-connector-templates/)を参照してください。</li><li>テンプレートは名前で二重中括弧によってサポートされるフィールドに注入されます。</li><li>例：`{{SomeTemplateName}}`。</li></ul> |
