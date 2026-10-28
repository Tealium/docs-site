---
title: Google Display and Video 360コネクタ構成ガイド
description: この記事では、Customer Data HubアカウントでGoogle Display & Video 360コネクタを構成する方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/google-display-video-360-connector/
---
## 要件

TealiumにGoogleオーディエンスの作成、一覧表示、更新を行うためのアクセス権を付与するには、Google DV360インターフェイスでアカウントをTealiumにリンクします（**Linked Accounts > Link New Account > External Data Partner > Tealium**）。詳細については、[Google：外部データ管理プラットフォームまたはカスタマーマッチアップローダーパートナーからオーディエンスリストを共有する](https://support.google.com/displayvideo/answer/9649053?hl=en)を参照してください。


<blockquote>
以前、このコネクタを使用するには、Googleにアカウントを許可リストへ追加するよう申請する必要がありました。最新バージョンのコネクタでは、この要件はなくなりました。
</blockquote>


## API情報

このコネクタは、以下のベンダーAPIを使用します。

* ユーザーリスト操作（作成／一覧表示）
  * API名：Google Data Manager API
  * APIバージョン：v1
  * APIエンドポイント：`https://datamanager.googleapis.com`
  * ドキュメント：[Google Data Manager API](https://developers.google.com/data-manager/api)
* ユーザーリストのアップロード
  * API名：Google Authorized Buyers
  * APIバージョン：v2
  * APIエンドポイント：`https://cm.g.doubleclick.net/upload`
  * ドキュメント：[Google Authorized Buyers API](https://developers.google.com/authorized-buyers/rtb/bulk-uploader)


<blockquote>
コネクタが実行されてから訪問が利用可能になるまで、最大72時間かかる場合があります。<br>
詳細については、[サードパーティのオーディエンスリストを使用する際のヒント](https://support.google.com/displayvideo/answer/6212219?hl=en&amp;ref_topic=2726036)を参照してください。
</blockquote>


## 構成

Connector Marketplaceに移動し、新しいコネクタを追加します。コネクタを追加する一般的な手順については、[コネクタの概要](https://docs.tealium.com/about-connectors/)の記事を参照してください。


<blockquote>
このコネクタを追加するときは、表示されるベンダーのデータプラットフォームポリシーに同意する必要があります。
</blockquote>


コネクタを追加した後、以下の構成を構成します。

* **クライアント顧客ID**
  * （必須）選択した製品で使用する顧客識別子
* **対象製品を選択**
  * （必須）接続を確立するアカウントには、選択した対象製品へのアクセス権が必要です。
* **GoogleネットワークID**
  * （任意）
  * Google Cookie MatchingタグのGoogleホスト版を使用する場合は、GoogleネットワークIDを入力します。
  * Google Cookie MatchingタグのTealiumホスト版を使用する場合は、空欄のままにします。

### 新しいセグメントの作成

AudienceStreamで新しいセグメントを作成するには、以下の手順を使用します。

1. **Actions**選択ドロップダウンリストの上部にある**Create a New Segment**をクリックします。
2. 以下のフィールドに入力します。
   * **セグメント名**（必須）
   * **セグメントメンバーの有効期間**（任意）：日数を整数で入力します。Tealiumは、Googleにリクエストを送信する前に、この値を秒に変換します。空欄のままにすると、有効期間はリクエストから省略されます。
   * **インテグレーションコード**（任意）：ユーザーリストの販売者が、自社システム上のIDを関連付けるために使用するIDです。使用できるIDがない場合は、`1`から`1000`までのランダムな数値を入力します。
   * **セグメントの説明**（任意）  
![](https://docs.tealium.com/images/server-side-connectors/audiencestream-create-segment.jpg)

<blockquote>
[DataAccess](https://docs.tealium.com/about-dataaccess/)製品（EventStore、AudienceStore、EventDB、またはAudienceDB）を使用する場合、セグメント名は128文字未満にする必要があります。そうしないと、DataAccessによってセグメント名が切り詰められ、エラーが発生する可能性があります。
</blockquote>

3. **Create Segment**をクリックします。  
**Create Segment**ボタンの横にチェックマークが表示され、作成が完了したことを確認できます。


<blockquote>
新しいGoogle Display &amp; Video 360オーディエンスを作成した場合、アクション内で新しいオーディエンスを使用するまで3～4時間待ってください。オーディエンスリストがGoogle Display &amp; Video 360内に表示された後は、エラーなくオーディエンスを使用できます。詳細については、[Google Display &amp; Videoヘルプ：オーディエンスリストによるターゲティング](https://support.google.com/displayvideo/answer/2949947?hl=en)を参照してください。
</blockquote>


## アクション

| アクション名 | AudienceStream | EventStream |
| ----------- | :------------: | :---------: |
| 訪問をユーザーリストまたはセグメントに追加 | ✓ | ✓ |
| ユーザーリストまたはセグメントから訪問を削除 | ✓ | ✓ |

### 訪問をユーザーリストまたはセグメントに追加

#### パラメータ


<blockquote>
次のIDパラメータのいずれかを使用する必要があります：**パートナー提供ID（MD5ハッシュ化済み）**、**パートナー提供ID（MD5ハッシュを適用）**、**GoogleユーザーID**、**iOS広告ID**、**Android広告ID**、**RIDA**、**AFAI**、または**MSAI**。
</blockquote>


| パラメータ | 説明 |
|---| ---|
| 対象のユーザーリスト／セグメントを選択 | （必須）ユーザーマップ識別子。この操作の適用対象となるユーザーを指定します。ユーザーが追加される対象のユーザーリスト／セグメントです。 |
| パートナー提供ID（MD5ハッシュ化済み） | このパラメータは、Tealium iQ Cookie MatchingサービスタグによってGoogleへ送信されます。Cookie Matchタグのデフォルト実装では、Tealium Visitor IDがMD5ハッシュとして送信されます。このIDをデフォルトとして使用する場合は、この属性をMD5ハッシュオプションにマッピングします。 |
| パートナー提供ID（MD5ハッシュを適用） | このパラメータは**パートナー提供ID（MD5ハッシュ化済み）**と似ていますが、値が自動的にMD5でハッシュ化されます。 |
| GoogleユーザーID | GoogleユーザーID。ADX Cookie Matchingサービスによって提供されます。 |
| iOS広告ID | iOS広告ID。 |
| Android広告ID | Android広告ID。 |
| RIDA | Roku ID。 |
| AFAI | Amazon Fire TV ID。 |
| MSAI | Xbox／Microsoft ID。 |
| データソースID | （任意）このメンバーシップに寄与したデータソースを示すID。`1`から`1,000`までの範囲で指定する必要があります。`1,000`を超えるIDを指定すると、`BAD_DATA_SOURCE_ID`エラーが発生します。これらのIDにはGoogleにとっての参照先や意味はなく、レポート用のラベルとしてのみ使用されます。 |

##### 同意

**訪問をユーザーリストに追加**アクションを使用すると、コネクタは同意情報を`true`として送信します。同意していない訪問がリストに追加されないようにするには、オーディエンスロジックを使用します。同意していない訪問をリストから削除するには、**ユーザーリストから訪問を削除**アクションを使用します。

### ユーザーリストまたはセグメントから訪問を削除

#### パラメータ

| パラメータ | 説明 |
|---| ---|
| 対象のユーザーリスト／セグメントを選択 | （必須）ユーザーが削除される対象のユーザーリスト／セグメントです。 |
| GoogleユーザーID | GoogleユーザーID。ADX Cookie Matchingサービスによって提供されます。 |
| データソースID | （任意）このメンバーシップに寄与したデータソースを示すID。`1`から`1,000`までの範囲で指定する必要があります。`1,000`を超えるIDを指定すると、`BAD_DATA_SOURCE_ID`エラーが発生します。これらのIDにはGoogleにとっての参照先や意味はなく、レポート用のラベルとしてのみ使用されます。 |