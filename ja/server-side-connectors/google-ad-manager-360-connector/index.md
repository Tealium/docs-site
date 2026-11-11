---
title: Google Ad Manager 360 コネクタ構成ガイド
description: この記事では、Customer Data Hub アカウントで Google Ad Manager 360 コネクタを構成する方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/google-ad-manager-360-connector/
---
## 要件

Tealium に Google オーディエンスの作成、一覧表示、更新を行うためのアクセス権を付与するには、Google Ad Manager のインターフェイスでアカウントを Tealium にリンクします（**Linked Accounts > Link New Account > External Data Partner > Tealium**）。詳細については、[Google：カスタマーマッチ パートナーを使用してデータをアップロードする](https://support.google.com/google-ads/answer/7361372?hl=en)を参照してください。


<blockquote>
以前、このコネクタを使用するには、Google にアカウントを許可リストへ追加するよう依頼する必要がありました。最新バージョンのコネクタでは、この要件はなくなりました。
</blockquote>


## コネクタのアクション

| アクション名 | 訪問プロファイル | イベントデータ |
| --- | :---: | :---: |
|訪問をユーザーリストまたはセグメントに追加| ✓| ✓|
|ユーザーリストまたはセグメントから訪問を削除| ✓| ✓|

## API 情報

このコネクタは、次のベンダー API を使用します。

* ユーザーリスト操作（作成／一覧表示）
  * API 名：Google Data Manager API
  * API バージョン：v1
  * API エンドポイント：`https://datamanager.googleapis.com`
  * ドキュメント：[Google Data Manager API](https://developers.google.com/data-manager/api)
* ユーザーリストのアップロード
  * API 名：Google Authorized Buyers
  * API バージョン：v2
  * API エンドポイント：https://cm.g.doubleclick.net/upload
  * ドキュメント：[Google Authorized Buyers API](https://developers.google.com/authorized-buyers/rtb/bulk-uploader)

## 構成の構成

コネクタマーケットプレイスに移動し、新しいコネクタを追加します。詳細については、[about-connectors](https://docs.tealium.com/about-connectors/)を参照してください。


<blockquote>
このコネクタを追加すると、ベンダーのデータプラットフォームポリシーへの同意を求められます。
</blockquote>


コネクタを追加した後、次の構成を構成します。

* **クライアント顧客 ID**
  * 必須
  * 選択した製品における顧客識別子。

* **Google ネットワーク ID**
  * オプション
  * Google がホストするバージョンの Google Cookie Matching タグを使用する場合は、Google ネットワーク ID を入力します。
  * Tealium がホストするバージョンの Google Cookie Matching タグを使用する場合は、空白のままにします。

### 新しいセグメントの作成

Customer Data Platform（CDP）で新しいセグメントを作成するには、次の手順を使用します。

1. アクション選択ドロップダウン画面の上部にある **Create a New Segment** をクリックします。
2. 次のフィールドに入力します。
  * **Segment Name**（必須）
  * **Segment Member Lifespan**（オプション）：日数を整数で入力します。Tealium は、リクエストを Google に送信する前にこの値を秒に変換します。空白のままにすると、リクエストから有効期間が省略されます。
  * **Integration Code**（オプション）：ユーザーリストの販売者が、自社システム上の ID を関連付けるために使用する ID です。使用できる ID がない場合は、`1`～`1000`のランダムな数値を入力します。
  * **Segment Description**（オプション）
  
<blockquote>
[DataAccess](https://docs.tealium.com/about-dataaccess/) 製品（EventStore、AudienceStore、EventDB、または AudienceDB）を使用する場合、セグメント名は 128 文字未満にする必要があります。そうしないと、DataAccess によってセグメント名が切り詰められ、エラーが発生する可能性があります。
</blockquote>

![](https://docs.tealium.com/images/server-side-connectors/audiencestream-create-segment.jpg)

3. **Create Segment** をクリックします。  
成功すると、**Create Segment** ボタンの横にチェックマークが表示されます。

## アクション構成 - パラメータとオプション

**Continue** をクリックして、コネクタのアクションを構成します。アクションの名前を入力し、ドロップダウンメニューからアクションタイプを選択します。

次のセクションでは、各アクションのパラメータとオプションを構成する方法について説明します。

### アクション - 訪問をユーザーリストまたはセグメントに追加

#### パラメータ

|**パラメータ**| **説明** |
|---| ---|
|対象のユーザーリスト／セグメントを選択|（必須）ユーザーマップ識別子。この操作の対象となるユーザーを指定します。このパラメータでは、ユーザーの追加先となる対象のユーザーリスト／セグメントを指定します。|
|ユーザー ID| <ul><li>Google ユーザー ID - TiQ Cookie Matching サービスタグによって Google から返されます</li><li>パートナー提供 ID - [Google Ad Manager および DV360 向け Google Cookie Matching Service](https://docs.tealium.com/google-cookie-matching-service/) タグによって Google に送信されます。デフォルトの Cookie Match タグ実装では、Tealium 訪問 ID に MD5 ハッシュが適用されます。デフォルトオプションを使用する場合は、この属性を MD5 ハッシュオプションにマッピングします。</li><li>iOS 広告 ID</li><li>Android 広告 ID</li><li>Roku ID（RIDA）</li><li>Amazon Fire TV ID（AFAI）</li><li>XBOX／Microsoft ID（MSAI）</li></ul>|
|データソース ID|（オプション）このメンバーシップに寄与したデータソースを示す ID。ID は 1～1,000 の範囲内である必要があります。この範囲外の ID を指定すると、次のエラーが発生します：`BAD_DATA_SOURCE_ID`。これらの ID は Google にとって意味を持たず、レポート目的のラベルとしてのみ使用されます。|

##### 同意

**ユーザーリストに訪問を追加**アクションを使用すると、コネクタは同意情報を `true` として送信します。同意していない訪問がリストに追加されないようにするには、オーディエンスロジックを使用します。同意していない訪問をリストから削除するには、**ユーザーリストから訪問を削除**アクションを使用します。

### アクション - ユーザーリストまたはセグメントから訪問を削除

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|対象のユーザーリスト／セグメントを選択|（必須）ユーザーマップ識別子。この操作の対象となるユーザーを指定します。このパラメータでは、ユーザーの削除元となる対象のユーザーリスト／セグメントを指定します。|
|ユーザー ID| <ul><li>Google ユーザー ID - TiQ Cookie Matching サービスタグによって Google から返されます</li><li>パートナー提供 ID - [Google Ad Manager および DV360 向け Google Cookie Matching Service](https://docs.tealium.com/google-cookie-matching-service/) タグによって Google に送信されます。デフォルトの Cookie Match タグ実装では、Tealium 訪問 ID に MD5 ハッシュが適用されます。デフォルトオプションを使用する場合は、この属性を MD5 ハッシュオプションにマッピングします。</li><li>iOS 広告 ID</li><li>Android 広告 ID</li><li>Roku ID（RIDA）</li><li>Amazon Fire TV ID（AFAI）</li><li>XBOX／Microsoft ID（MSAI）</li></ul>|
|データソース ID|（オプション）このメンバーシップに寄与したデータソースを示す ID。ID は 1～1,000 の範囲内である必要があります。この範囲外の ID を指定すると、次のエラーが発生します：`BAD_DATA_SOURCE_ID`。これらの ID は Google にとって意味を持たず、レポート目的のラベルとしてのみ使用されます。|