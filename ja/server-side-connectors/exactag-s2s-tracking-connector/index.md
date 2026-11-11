---
title: Exactag S2S Trackingコネクタ構成ガイド
description: この記事では、Customer Data HubアカウントでExactag S2S Trackingコネクタを構成する方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/exactag-s2s-tracking-connector/
---
この記事では、Exactag S2S Trackingコネクタを構成する方法について説明します。

## API情報

このコネクタでは、次のベンダーAPIを使用します。

* API名：Exactag S2S Tracking API
* APIバージョン：v1.0
* APIエンドポイント：`https://m.exactag.com/s2s/pi.ashx`

## アクション

| アクション名 | 訪問プロファイル | イベントデータ |
| --- | :---: | :---: |
| ページインプレッションイベントを送信 | ✗ | ✓ |
| オンサイトコンバージョンリクエストを送信 | ✗ | ✓ |

## 構成

コネクタマーケットプレイスに移動し、新しいコネクタを追加します。詳細については、[about-connectors](https://docs.tealium.com/about-connectors/)を参照してください。

コネクタを追加した後、次の構成を構成します。

* **キャンペーン**  

コネクタを構成したら、**完了**をクリックします。
32バイトで暗号化されたブランド固有のキャンペーンコードです。

## アクション

次のセクションでは、各アクションでサポートされるパラメータを示します。

### ページインプレッションイベントを送信

#### 一意の識別子属性

| **パラメータ** | **説明** |
| --- | --- |
| euk | ユーザーまたはデバイスを識別するための一意の識別子。Tealium Visitor IDを使用する場合は、このパラメータを使用します。 |
| mid | IDFAやGoogle PlayストアIDなどのモバイルデバイスIDを使用する場合は、このパラメータを使用します。MD5でハッシュ化し、ユーザーキーとして使用する必要があります。 |
| uk | ユーザーまたはデバイスを識別するための一意の識別子。この値はMD5でハッシュ化する必要があります。Exactag User IDを使用する場合は、このパラメータを使用します。 |
| gk | 複数ユーザーの匿名グループを識別するための一意の識別子。この値はMD5でハッシュ化し、グループの有効期限タイムスタンプ（urlEncodedまたはbase64url）と組み合わせる必要があります。 |

#### イベント属性

| **パラメータ** | **説明** |
| --- | --- |
| sitegroup | （必須）構成済みのイベント／サイトグループ。ページインプレッションの分類とコンバージョンイベントの識別に使用します。 |
| useragent | （必須）クライアントのユーザーエージェント（エンコード済み）。 |
| ipaddress | （必須）位置情報の特定に使用するクライアントのIPアドレス（保存されません）。 |
| referrer | （必須）プロトコルを含むリファラーURL。例：`https://www.tealium.com` |
| sessionid | （必須）単一のユーザーセッションを識別するための値。 |
| host | （必須）ホスト（サイトとプロトコルを含まないドメインのみ）。例：`example.com` |
| site | （必須）リクエストされたURIのパス部分。たとえば、`https://tealium.com/resources/`のパス部分は`resources`です。|
| search | （必須）リクエストされたURIのクエリ部分。例：`?utm_campaign=abc` |
| sescount | （必須）セッション番号。1は新規訪問、1より大きい値は再訪問を示します。 |
| sesevent | （必須）セッション番号。1はこのセッションにおける最初のページインプレッションを示します。 |
| optout | バイナリ値。1に構成すると、顧客がオプトアウトしたものとしてリクエストが処理されます。この場合、ユーザー識別子は無視され、保存されません。 |
| consent | タイプまたはパートナーに基づく同意を表すJSONオブジェクト（URLエンコード済み）。例：`{“comfort”:1,”analytics”:0,”marketing”:0}`。より複雑なデータ構造を作成するには、**イベント属性テンプレート**セクションでテンプレート名を指定します。 |
| consent_string | IAB GDPR同意文字列。 |
| protocol | プロトコル。`http`または`https`のいずれか。 |
| params | Exactagに送信する追加パラメータを含むJSONオブジェクト。より複雑なデータ構造を作成するには、**イベント属性テンプレート**セクションでテンプレート名を指定します。 |
| Event Attributes Template Variables | データ入力としてテンプレート変数を指定します。詳細については、[connector-template-variables](https://docs.tealium.com/connector-template-variables/)を参照してください。ネストされたテンプレート変数にはドット記法で名前を付けます（例：`items.name`）。ネストされたテンプレート変数は通常、データレイヤーのリスト属性から作成されます。 |
| Event Attributes Templates | **イベント属性**で参照するテンプレートを指定します。詳細については、[about-connector-templates](https://docs.tealium.com/about-connector-templates/)を参照してください。テンプレートは、二重波括弧で囲んだ名前を使用して、サポートされているフィールドに挿入されます。例：`{{SomeTemplateName}}`。 |

### オンサイトコンバージョンリクエストを送信

#### 一意の識別子属性

| **パラメータ** | **説明** |
| --- | --- |
| euk | ユーザーまたはデバイスを識別するための一意の識別子。Tealium Visitor IDを使用する場合は、このパラメータを使用します。 |
| mid | IDFAやGoogle PlayストアIDなどのモバイルデバイスIDを使用する場合に使用します。MD5でハッシュ化し、ユーザーキーとして使用する必要があります。 |
| uk | ユーザーまたはデバイスを識別するための一意の識別子。この値はMD5でハッシュ化する必要があります。Exactag User IDを使用する場合は、このパラメータを使用します。 |
| gk | 複数ユーザーの匿名グループを識別するための一意の識別子。この値はMD5でハッシュ化し、グループの有効期限タイムスタンプ（urlEncodedまたはbase64url）と組み合わせる必要があります。 |

#### リクエスト属性

| **パラメータ** | **説明** |
| --- | --- |
| sitegroup | （必須）構成済みのイベント／サイトグループ。ページインプレッションの分類とコンバージョンイベントの識別に使用します。 |
| useragent | （必須）クライアントのユーザーエージェント（エンコード済み）。 |
| ipaddress | （必須）位置情報の特定に使用するクライアントのIPアドレス（保存されません）。 |
| referrer | （必須）プロトコルを含むリファラーURL。例：`https://www.tealium.com`|
| sessionid | （必須）単一のユーザーセッションを識別するための値。 |
| host | （必須）ホスト（サイトとプロトコルを含まないドメインのみ）。例：`example.com` |
| site | （必須）リクエストされたURIのパス部分。たとえば、`https://tealium.com/resources/`のパス部分は`resources`です。|
| search | （必須）リクエストされたURIのクエリ部分。例：`?utm_campaign=abc` |
| sescount | （必須）セッション番号。1は新規訪問、1より大きい値は再訪問を示します。 |
| sesevent | （必須）セッション番号。1はこのセッションにおける最初のページインプレッションを示します。 |
| optout | （必須）バイナリ値。1に構成すると、顧客がオプトアウトしたものとしてリクエストが処理されます。この場合、ユーザー識別子は無視され、保存されません。 |
| level | 推奨。構成済みのコミッションレベル。 |
| orderid | 推奨。注文ID（注文の重複排除に使用できます）。 |
| customerid | 推奨。顧客ID（クロスデバイスで使用できます）。 |
| totalprice | 推奨。買い物かごの合計金額。 |
| consent | タイプまたはパートナーに基づく同意を表す、URLエンコードされたJSONオブジェクト（例：`{“comfort”:1,”analytics”:0,”marketing”:0}`）。より複雑なデータ構造を作成するには、**リクエスト属性テンプレート**セクションでテンプレート名を指定します。 |
| protocol | プロトコル（`http`または`https`）。 |
| params | Exactagに送信する追加パラメータを含むJSONオブジェクト。複雑なデータ構造には、**リクエスト属性テンプレート**セクションで定義されたテンプレートを使用します。 |
| Request Attributes Template Variables | データ入力としてテンプレート変数を指定します。詳細については、[connector-template-variables](https://docs.tealium.com/connector-template-variables/)を参照してください。ネストされたテンプレート変数にはドット記法で名前を付けます（例：`items.name`）。ネストされたテンプレート変数は通常、データレイヤーのリスト属性から作成されます。 |
| Request Attributes Templates | **リクエスト属性**で参照するテンプレートを指定します。詳細については、[about-connector-templates](https://docs.tealium.com/about-connector-templates/)を参照してください。テンプレートは、二重波括弧で囲んだ名前を使用して、サポートされているフィールドに挿入されます。例：`{{SomeTemplateName}}`。 |