---
title: Google Ad Manager 360コネクタ構成ガイド
description: この記事では、Customer Data HubアカウントでGoogle Ad Manager 360コネクタを構成する方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/google-ad-manager-360-connector/
---
## 要件

TealiumにGoogleオーディエンスを作成、一覧表示、更新するためのアクセス権を付与するには、Google Ad ManagerのインターフェイスでアカウントをTealiumにリンクします（**Linked Accounts > Link New Account > External Data Partner > Tealium**）。詳細については、[Google：カスタマーマッチパートナーを使用してデータをアップロードする](https://support.google.com/google-ads/answer/7361372?hl=en)を参照してください。


<blockquote>
以前、このコネクタを使用するには、アカウントを許可リストに追加するようGoogleにリクエストする必要がありました。最新バージョンのコネクタでは、この要件はなくなりました。
</blockquote>


## コネクタアクション

| アクション名 | AudienceStream | EventStream |
| --- | :---: | :---: |
|訪問をユーザーリストまたはセグメントに追加| ✓| ✓|
|訪問をユーザーリストまたはセグメントから削除| ✓| ✓|

## API情報

このコネクタでは、以下のベンダーAPIを使用します。

* ユーザーリスト操作（作成／一覧表示）
  * API名：Google Data Manager API
  * APIバージョン：v1
  * APIエンドポイント：`https://datamanager.googleapis.com`
  * ドキュメント：[Google Data Manager API](https://developers.google.com/data-manager/api)
* ユーザーリストのアップロード
  * API名：Google Authorized Buyers
  * APIバージョン：v2
  * APIエンドポイント：https://cm.g.doubleclick.net/upload
  * ドキュメント：[Google Authorized Buyers API](https://developers.google.com/authorized-buyers/rtb/bulk-uploader)

## 構成の構成

コネクタマーケットプレイスに移動し、新しいコネクタを追加します。コネクタを追加する一般的な手順については、[コネクタについて](https://docs.tealium.com/about-connectors/)の記事を参照してください。


<blockquote>
このコネクタを追加すると、ベンダーのデータプラットフォームポリシーへの同意を求められます。
</blockquote>


コネクタを追加した後、以下の構成を構成します。

* **クライアント顧客ID**
  * 必須
  * 選択したプロダクトで使用する顧客識別子です。

* **GoogleネットワークID**
  * 任意
  * GoogleでホストされているバージョンのGoogle Cookie Matchingタグを使用する場合は、GoogleネットワークIDを入力します。
  * TealiumでホストされているバージョンのGoogle Cookie Matchingタグを使用する場合は、空白のままにします。

### 新しいセグメントの作成

AudienceStreamで新しいセグメントを作成するには、以下の手順を実行します。

1. アクション選択ドロップダウン画面の上部にある**新しいセグメントを作成**をクリックします。
2. 以下のフィールドに入力します。
  * **セグメント名**（必須）
  * **セグメントメンバーの有効期間**（任意）：日数を整数で入力します。TealiumはGoogleにリクエストを送信する前に、この値を秒に変換します。空白のままにした場合、有効期間はリクエストから省略されます。
  * **インテグレーションコード**（任意）：ユーザーリストの販売者が、自社システム上のIDを関連付けるために使用するIDです。使用可能なIDがない場合は、`1`から`1000`までの任意の数値を入力します。
  * **セグメントの説明**（任意）
  
<blockquote>
[DataAccess](https://docs.tealium.com/about-dataaccess/)プロダクト（EventStore、AudienceStore、EventDB、またはAudienceDB）を使用する場合、セグメント名は128文字未満にする必要があります。そうしない場合、DataAccessによってセグメント名が切り詰められ、エラーが発生する可能性があります。
</blockquote>

![](https://docs.tealium.com/images/server-side-connectors/audiencestream-create-segment.jpg)

3. **セグメントを作成**をクリックします。  
正常に完了すると、**セグメントを作成**ボタンの横にチェックマークが表示されます。

## アクション構成 - パラメータとオプション

**続行**をクリックして、コネクタアクションを構成します。アクションの名前を入力し、ドロップダウンメニューからアクションタイプを選択します。

以下のセクションでは、各アクションのパラメータとオプションを構成する方法について説明します。

### アクション - 訪問をユーザーリストまたはセグメントに追加

#### パラメータ

|**パラメータ**| **説明** |
|---| ---|
|対象のユーザーリスト／セグメントを選択|（必須）ユーザーマップ識別子です。この操作の対象となるユーザーを指定します。このパラメータでは、ユーザーの追加先となるユーザーリスト／セグメントを指定します。|
|ユーザーID| <ul><li>GoogleユーザーID - TiQ Cookie MatchingサービスタグによってGoogleから返されます</li> <li>パートナー提供ID - [Google Ad ManagerおよびDV360向けGoogle Cookie Matchingサービス](https://docs.tealium.com/google-cookie-matching-service/)タグによってGoogleに送信されます。デフォルトのCookie Matchタグ実装では、Tealium訪問IDにMD5ハッシュが適用されます。デフォルトオプションを使用する場合、この属性をMD5ハッシュオプションにマッピングします。</li><li>iOS広告ID</li> <li>Android広告ID</li> <li>Roku ID（RIDA）</li> <li>Amazon Fire TV ID（AFAI）</li> <li>XBOX／Microsoft ID（MSAI）</li></ul>|
|データソースID|（任意）このメンバーシップに寄与したデータソースを示すIDです。IDは1～1,000の範囲内である必要があり、この範囲外のIDを指定すると、`BAD_DATA_SOURCE_ID`エラーが発生します。これらのIDはGoogleにとって意味を持たず、レポート用のラベルとしてのみ使用されます。|

##### 同意

**訪問をユーザーリストに追加**アクションを使用すると、コネクタは同意情報を`true`として送信します。同意していない訪問がリストに追加されないように、オーディエンスロジックを使用してください。**訪問をユーザーリストから削除**アクションを使用して、同意していない訪問をリストから削除してください。

### アクション - 訪問をユーザーリストまたはセグメントから削除

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|対象のユーザーリスト／セグメントを選択|（必須）ユーザーマップ識別子です。この操作の対象となるユーザーを指定します。このパラメータでは、ユーザーの削除元となるユーザーリスト／セグメントを指定します。|
|ユーザーID| <ul><li>GoogleユーザーID - TiQ Cookie MatchingサービスタグによってGoogleから返されます</li> <li>パートナー提供ID - [Google Ad ManagerおよびDV360向けGoogle Cookie Matchingサービス](https://docs.tealium.com/google-cookie-matching-service/)タグによってGoogleに送信されます。デフォルトのCookie Matchタグ実装では、Tealium訪問IDにMD5ハッシュが適用されます。デフォルトオプションを使用する場合、この属性をMD5ハッシュオプションにマッピングします。</li><li>iOS広告ID</li> <li>Android広告ID</li> <li>Roku ID（RIDA）</li> <li>Amazon Fire TV ID（AFAI）</li> <li>XBOX／Microsoft ID（MSAI）</li></ul>|
|データソースID|（任意）このメンバーシップに寄与したデータソースを示すIDです。IDは1～1,000の範囲内である必要があり、この範囲外のIDを指定すると、`BAD_DATA_SOURCE_ID`エラーが発生します。これらのIDはGoogleにとって意味を持たず、レポート用のラベルとしてのみ使用されます。|