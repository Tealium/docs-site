---
title: Google Display & Video 360 コネクタ構成ガイド
description: この記事では、お客様のCustomer Data HubアカウントでGoogle Display & Video 360コネクタを構成する方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/google-display-video-360-connector/
---
## 要件

Googleのオーディエンスを作成、リスト、更新するためのTealiumへのアクセスを許可するには、Google DV360インターフェースでアカウントをTealiumにリンクしてください（**Linked Accounts &gt; Link New Account &gt; External Data Partner &gt; Tealium**）。詳細については、[Google: 外部データ管理プラットフォームまたは顧客マッチアップローダーパートナーからのオーディエンスリストの共有](https://support.google.com/displayvideo/answer/9649053?hl=ja)を参照してください。

 以前は、このコネクタを使用するにはGoogleにアカウントを許可リストに追加するよう依頼する必要がありましたが、コネクタの最新バージョンではこの要件はありません。 

## API情報

このコネクタは以下のベンダーAPIを使用します：

* ユーザーリスト操作（作成/リスト）
  * API名：Google Data Manager API
  * APIバージョン：v1
  * APIエンドポイント：`https://datamanager.googleapis.com`
  * ドキュメント：[Google Data Manager API](https://developers.google.com/data-manager/api)
* ユーザーリストアップロード
  * API名：Google Authorized Buyers
  * APIバージョン：v2
  * APIエンドポイント：`https://cm.g.doubleclick.net/upload`
  * ドキュメント：[Google Authorized Buyers API](https://developers.google.com/authorized-buyers/rtb/bulk-uploader)

コネクタが発火してから訪問が使用可能になるまで最大72時間かかる場合があります。&lt;br&gt;
詳細については、[第三者のオーディエンスリストの使用に関するヒント](https://support.google.com/displayvideo/answer/6212219?hl=ja&amp;amp;ref_topic=2726036)を参照してください。

## 構成

コネクタマーケットプレイスにアクセスし、新しいコネクタを追加します。コネクタの追加方法については、[コネクタ概要]()の記事を読んでください。

このコネクタを追加する際には、表示されるベンダーのデータプラットフォームポリシーを受け入れる必要があります。

コネクタを追加した後、以下の構成を構成します：

* **クライアントカスタマーID**
  * （必須）選択した製品の顧客識別子
* **対象製品の選択**
  * （必須）接続を確立するアカウントは、選択した対象製品にアクセスできる必要があります。
* **GoogleネットワークID**
  * （オプション）
  * Googleホスト版のGoogle Cookie Matchingタグを使用する場合は、GoogleネットワークIDを入力します。
  * Tealiumホスト版のGoogle Cookie Matchingタグを使用する場合は、これを空白のままにします。

### 新しいセグメントの作成

AudienceStreamで新しいセグメントを作成するには、次の手順に従ってください：

1. **アクション**選択ドロップダウンリストの上部から**新しいセグメントを作成**をクリックします。
2. **セグメント名**、**セグメントメンバー寿命**、**統合コード**、および**セグメント説明**を入力します。  
![](/images/server-side-connectors/audiencestream-create-segment.jpg)
[DataAccess]()製品（EventStore、AudienceStore、EventDB、またはAudienceDB）を使用する場合、セグメント名は128文字未満である必要があります。それ以外の場合、DataAccessはセグメント名を切り詰め、エラーが発生する可能性があります。
3. **セグメント作成**をクリックします。  
統合コードは、ユーザーリスト販売者が自分のシステム上のIDを相関させるために使用するIDです。IDが利用できない場合は、`1`から`1000`の間のランダムな数字を手動で入力することができます。セグメントが作成されたことを確認するチェックマークがセグメント作成ボタンの隣に表示されます。

新しいGoogle Display &amp;amp; Video 360オーディエンスをアクション内で使用する前に、3〜4時間待ってください。オーディエンスリストがGoogle Display &amp;amp; Video 360内に表示されたら、エラーなくオーディエンスを使用できます。詳細については、[Google Display &amp;amp; Videoヘルプ：オーディエンスリストターゲティング](https://support.google.com/displayvideo/answer/2949947?hl=ja)を参照してください。

## アクション

| アクション名 | AudienceStream | EventStream |
| ----------- | :------------: | :---------: |
| ユーザーリストまたはセグメントに訪問を追加 | ✓ | ✓ |
| ユーザーリストまたはセグメントから訪問を削除 | ✓ | ✓ |

### ユーザーリストまたはセグメントに訪問を追加

#### パラメータ

 次のいずれかのIDパラメータを使用する必要があります：**パートナー提供ID（既にMD5ハッシュ化済み）**、**パートナー提供ID（MD5ハッシュを適用）**、**GoogleユーザーID**、**iOS広告ID**、**Android広告ID**、**RIDA**、**AFAI**、または**MSAI**。 

| パラメータ | 説明 |
|---| ---|
| 対象ユーザーリスト/セグメントの選択 | (必須) ユーザーマップ識別子。この操作が適用されるユーザーを指定します。これがユーザーが追加される対象のユーザーリスト/セグメントです。 |
| パートナー提供ID（既にMD5ハッシュ化済み） | このパラメータは、Tealium iQクッキーマッチングサービスタグによってGoogleに送信されます。デフォルトのクッキーマッチタグ実装では、Tealium訪問IDをMD5ハッシュとして送信します。このIDをデフォルトとして使用する場合は、この属性をMD5ハッシュオプションにマップします。 |
| パートナー提供ID（MD5ハッシュを適用） | このパラメータは**パートナー提供ID（既にMD5ハッシュ化済み）**と似ていますが、値にMD5ハッシュを適用します。 |
| GoogleユーザーID | GoogleユーザーID。ADXクッキーマッチングサービスによって提供されます。 |
| iOS広告ID | iOS広告ID。 |
| Android広告ID | Android広告ID。 |
| RIDA | Roku ID。 |
| AFAI | Amazon Fire TV ID。 |
| MSAI | Xbox/Microsoft ID。 |
| データソースID | (オプション) このメンバーシップに貢献したデータソースを示すID。`1`から`1,000`の範囲である必要があります。`1,000`を超えるIDは`BAD_DATA_SOURCE_ID`エラーを引き起こします。これらのIDはGoogleにとって参照や意味を持たず、報告目的でのみラベルとして使用されます。 |

##### 同意

**ユーザーリストに訪問を追加**アクションを使用する場合、コネクタは同意を`true`として送信します。同意していない訪問がリストに追加されないように、オーディエンスロジックを使用してください。**ユーザーリストから訪問を削除**アクションを使用して、リストから同意していない訪問を削除します。

### ユーザーリストまたはセグメントから訪問を削除

#### パラメータ

| パラメータ | 説明 |
|---| ---|
| 対象ユーザーリスト/セグメントの選択 | (必須) これがユーザーが削除される対象のユーザーリスト/セグメントです。 |
| GoogleユーザーID | GoogleユーザーID。ADXクッキーマッチングサービスによって提供されます。 |
| データソースID | (オプション) このメンバーシップに貢献したデータソースを示すID。`1`から`1,000`の範囲である必要があります。`1,000`を超えるIDは`BAD_DATA_SOURCE_ID`エラーを引き起こします。これらのIDはGoogleにとって参照や意味を持たず、報告目的でのみラベルとして使用されます。 |
