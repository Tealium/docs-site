---
title: Google Ad Manager 360 コネクタ構成ガイド
description: この記事では、Customer Data Hub アカウントで Google Ad Manager 360 コネクタを構成する方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/google-ad-manager-360-connector/
---
## 要件

Google オーディエンスの作成、リスト、更新へのアクセスを Tealium に許可するには、Google Ad Manager インターフェースでアカウントを Tealium にリンクしてください（**Linked Accounts > Link New Account > External Data Partner > Tealium**）。詳細については、[Google: Use Customer Match partners to upload data](https://support.google.com/google-ads/answer/7361372?hl=en) を参照してください。


<blockquote>
以前は、このコネクタを使用するには Google にアカウントを許可リストに追加するよう依頼する必要がありましたが、最新バージョンではその要件はありません。
</blockquote>


## コネクタのアクション

| アクション名 | AudienceStream | EventStream |
| --- | :---: | :---: |
|ユーザーリストまたはセグメントに訪問を追加| ✓| ✓|
|ユーザーリストまたはセグメントから訪問を削除| ✓| ✓|

## API 情報

このコネクタは以下のベンダー API を使用します：

* ユーザーリスト操作（作成/リスト）
  * API 名: Google Data Manager API
  * API バージョン: v1
  * API エンドポイント: `https://datamanager.googleapis.com`
  * ドキュメント: [Google Data Manager API](https://developers.google.com/data-manager/api)
* ユーザーリストアップロード
  * API 名: Google Authorized Buyers
  * API バージョン: v2
  * API エンドポイント: https://cm.g.doubleclick.net/upload
  * ドキュメント: [Google Authorized Buyers API](https://developers.google.com/authorized-buyers/rtb/bulk-uploader)

## 構成の構成

コネクタマーケットプレイスに移動して新しいコネクタを追加します。コネクタを追加する一般的な手順については、[About Connectors](https://docs.tealium.com/about-connectors/) の記事を参照してください。


<blockquote>
このコネクタを追加すると、ベンダーのデータプラットフォームポリシーを受け入れるように求められます。
</blockquote>


コネクタを追加した後、以下の構成を構成します：

* **クライアントカスタマーID**
  * 必須
  * 選択した製品の顧客識別子です。

* **Google ネットワークID**
  * 任意
  * Google ホスト版の Google Cookie Matching タグを使用する場合は、Google ネットワークIDを入力します。
  * Tealium ホスト版の Google Cookie Matching タグを使用する場合は、これを空白のままにします。

### 新しいセグメントの作成

AudienceStream で新しいセグメントを作成するには、次の手順に従います：

1. アクション選択ドロップダウン画面の上部から **Create a New Segment** をクリックします。
2. 次のフィールドを完了します：
  * **セグメント名**
  * **セグメントメンバー寿命**
  * **統合コード** - 統合コードは、ユーザーリスト販売者が自分のシステム上のIDを相関させるために使用するIDです。IDが利用できない場合は、1から1000の間のランダムな数字を入力します。
  * **セグメント説明**。
  
<blockquote>
[DataAccess](https://docs.tealium.com/about-dataaccess/) 製品（EventStore、AudienceStore、EventDB、または AudienceDB）を使用する場合、セグメント名は128文字未満でなければなりません。それ以外の場合、DataAccess はセグメント名を切り詰め、エラーが発生する可能性があります。
</blockquote>

![](https://docs.tealium.com/images/server-side-connectors/audiencestream-create-segment.jpg)

3. **Create Segment** をクリックします。
成功すると、**Create Segment** ボタンの隣にチェックマークが表示されます。

## アクション構成 - パラメータとオプション

コネクタアクションを構成するには、**Continue** をクリックします。アクションの名前を入力し、ドロップダウンメニューからアクションタイプを選択します。

次のセクションでは、各アクションのパラメータとオプションの構成方法について説明します。

### アクション - ユーザーリストまたはセグメントに訪問を追加

#### パラメータ

|**パラメータ**|  **説明** |
|---| ---|
|対象ユーザーリスト/セグメントの選択|  (必須) ユーザーマップ識別子。この操作が適用されるユーザーを指定します。このパラメータは、ユーザーが追加される対象のユーザーリスト/セグメントを指定します。 |
|ユーザーID| <ul><li>Google ユーザーID - Google によって TiQ クッキーマッチングサービスタグから返されます</li> <li>パートナー提供ID - [Google Cookie Matching Service for Google Ad Manager and DV360](https://docs.tealium.com/google-cookie-matching-service/) タグによって Google に送信されます。デフォルトのクッキーマッチタグ実装は Tealium 訪問IDに MD5 ハッシュを適用します。デフォルトオプションを使用する場合は、この属性を MD5 ハッシュオプションにマッピングします。</li><li>iOS 広告ID</li> <li>Android 広告ID</li> <li>Roku ID (RIDA)</li> <li>Amazon Fire TV ID (AFAI)</li> <li>XBOX/Microsoft ID (MSAI)</li></ul>|
|データソースID|  (任意) このメンバーシップに貢献したデータソースを示すIDです。IDは1から1,000の範囲内でなければならず、この範囲外のIDは次のエラーを引き起こします：`BAD_DATA_SOURCE_ID`。これらのIDは Google にとって意味をなさず、報告目的でのみラベルとして使用されます。 |

##### 同意

**ユーザーリストに訪問を追加** アクションを使用する場合、コネクタは同意を `true` として送信します。同意していない訪問がリストに追加されないように、オーディエンスロジックを使用します。**ユーザーリストから訪問を削除** アクションを使用して、同意していない訪問をリストから削除します。

### アクション - ユーザーリストまたはセグメントから訪問を削除

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|対象ユーザーリスト/セグメントの選択|  (必須) ユーザーマップ識別子。この操作が適用されるユーザーを指定します。このパラメータは、ユーザーが削除される対象のユーザーリスト/セグメントを指定します。 |
|ユーザーID|  <ul><li>Google ユーザーID - Google によって TiQ クッキーマッチングサービスタグから返されます</li> <li>パートナー提供ID - [Google Cookie Matching Service for Google Ad Manager and DV360](https://docs.tealium.com/google-cookie-matching-service/) タグによって Google に送信されます。デフォルトのクッキーマッチタグ実装は Tealium 訪問IDに MD5 ハッシュを適用します。デフォルトオプションを使用する場合は、この属性を MD5 ハッシュオプションにマッピングします。</li><li>iOS 広告ID</li> <li>Android 広告ID</li> <li>Roku ID (RIDA)</li> <li>Amazon Fire TV ID (AFAI)</li> <li>XBOX/Microsoft ID (MSAI)</li></ul>|
|データソースID|  (任意) このメンバーシップに貢献したデータソースを示すIDです。IDは1から1,000の範囲内でなければならず、この範囲外のIDは次のエラーを引き起こします：`BAD_DATA_SOURCE_ID`。これらのIDは Google にとって意味をなさず、報告目的でのみラベルとして使用されます。 |
