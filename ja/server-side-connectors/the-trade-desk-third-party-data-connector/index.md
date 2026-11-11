---
title: The Trade Deskサードパーティデータコネクタ構成ガイド
description: この記事では、The Trade Deskサードパーティデータコネクタの構成方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/the-trade-desk-third-party-data-connector/
---

<blockquote>
現在、このコネクタはコネクタマーケットプレイスでは利用できません。The Trade Deskサードパーティデータコネクタを使用するには、TealiumとThe Trade Deskの両方のアカウントマネージャーによるサポートが必要です。このコネクタを使用するには、Tealiumのアカウントマネージャーにお問い合わせください。
</blockquote>


## API情報

このコネクタでは、次のベンダーAPIを使用します。

* API名：The Trade Desk API
* APIバージョン：v3.0
* APIエンドポイント：`https://bulk-data.adsrvr.org`
  * データレートエンドポイント：`POST /datarate/batch`
  * サードパーティエンドポイント：`POST /data/thirdparty`
* ドキュメント：[The Trade Desk API](https://partner.thetradedesk.com/v3/portal/data/doc/post-data-thirdparty)

## バッチ処理の制限
  
このコネクタは、ベンダーへの大量のデータ転送をサポートするために、リクエストをバッチ処理します。並列処理により、イベントが順不同でベンダーに到達する場合があります。順序が重要な場合は、イベントにシーケンス値を追加してください。詳細については、[バッチアクション](https://docs.tealium.com/batched-actions/)を参照してください。リクエストは、次のいずれかのしきい値に達するか、プロファイルがパブリッシュされるまでキューに格納されます。

* リクエストの最大数：10000
* 最も古いリクエストからの最大経過時間：30分
* リクエストの最大サイズ：2 MB

## 構成

コネクタマーケットプレイスに移動し、新しいコネクタを追加します。詳細については、[about-connectors](https://docs.tealium.com/about-connectors/)を参照してください。

コネクタを追加した後、次の構成を構成します。

* **シークレットキー**：（必須）シークレットキー。
* **APIベースURL**：（必須）APIベースURLを選択します。

コネクタを構成した後、**完了**をクリックします。

## 管理者構成

### 認証トークンの生成

管理タスクを実行する前に、有効なユーザー名とパスワードを使用して認証トークンを生成する必要があります。認証は管理タスクにのみ適用され、コネクタの動作には必要ありません。

* **ログイン**：（必須）ログイン情報を入力します。
* **パスワード**：（必須）パスワードを入力します。

### タクソノミーセグメントの作成

詳細については、[The Trade Deskパートナーポータル：サードパーティデータのタクソノミー設計](https://partner.thetradedesk.com/v3/portal/data/doc/DataTaxonomyDesign#top)を参照してください。

| パラメータ | 説明 |
|--------------------------|----------------------------|
| プロバイダーID | （必須）アカウントマネージャーから提供された、プロバイダーアカウントの一意のID。|
| プロバイダー要素ID | （必須）タクソノミーの設計時にセグメントに割り当てられた一意のID。IDは512文字以内にする必要があります。この値は作成後に変更できません。|
| 親要素ID | （必須）タクソノミー内の親セグメントのプロバイダー要素ID値。このパラメータによって、タクソノミーの階層構造が確立されます。この値は作成後に変更できません。すべてのデータプロバイダーは、タクソノミーのベース要素である`ROOT`を使用します。|
| 表示名 | （必須）DMPのユーザーインターフェイスで購入者に表示されるセグメント名。表示名は256文字以内にする必要があります。ただし、特にフルパスが長くなる下位の子要素では、読みやすさを考慮して50文字以内を推奨します。タブや、`'`、`"`、`^`などの特殊文字を含めないでください。|
| 購入可能 | （必須）セグメントをDMPで購入者に表示し、利用可能にするには、`true`に構成します。コンテナ要素は子要素の整理とレートの割り当てにのみ使用されるため、このプロパティ値を`false`に構成します。購入可能なセグメントのプロパティ値を`false`に変更した場合、そのセグメントを現在オーディエンスに含めている顧客は、キャンペーンが終了するまで引き続き使用できます。|
| 説明 | （任意）DMPで顧客に表示されるデータセグメントの説明。説明は4,000文字以内にする必要がありますが、読みやすさを考慮して256文字以内を推奨します。|
| 直接IPターゲティング | （任意）`true`の場合、使用または作成される`TargetingData`のタイプは、デフォルトの`7`（`ThirdPartyData`）ではなく`16`（`DirectIpTargeting`）になります。|

### セグメントへのレートの割り当て

| パラメータ | 説明 |
|-------------------------------|-------------|
| プロバイダーID | （必須）アカウントマネージャーから提供された、プロバイダーアカウントの一意のID。 |
| プロバイダー要素ID | （必須）システム内でこのデータ要素を識別する一意のID。 |
| ブランドID | （必須）プロバイダーが管理するブランドを識別する一意のID。 |
| レートレベル | （必須）サードパーティデータのレートレベル。アクセスをリクエストするには、テクニカルアカウントマネージャーにお問い合わせください。<br>`Partner`：特定のパートナーとその広告主向け。<br>`Advertiser`：特定の広告主向け。このレートレベルには追加の権限が必要です。 |
| パートナーID | （必須）カスタムタクソノミーで、このレートのデータセグメントにアクセスできるパートナーのプラットフォームID。 |
| 広告主ID | （必須）カスタムタクソノミーで、このレートのデータセグメントにアクセスできる広告主のプラットフォームID。 |
| レートタイプ | （必須）セグメントのデータレートタイプ。シンジケートされたタクソノミーのシステムレベルのデータレートはすべて、メディアコストの割合と最大CPM（1,000インプレッションあたりのコスト）の上限を使用するハイブリッドレートとして割り当てる必要があります。つまり、このプロパティを`Hybrid`に構成し、`CPMRate`と`PercentOfMediaCostRate`の両方のプロパティに値を指定する必要があります。カスタムタクソノミーでは任意のデータレートタイプを使用できますが、ハイブリッドレートを強く推奨します。 |
| CPMレート金額 | （必須）CPMレートの金額。 |
| CPMレート通貨コード | （必須）CPMレートの通貨コード。 |
| メディアコスト比率レート | （任意）ハイブリッドデータレート（**レートタイプ**で選択）において、`CPMRate`の上限と組み合わせて使用するメディアコストの割合。割合を小数で入力します。 |

## アクション

| アクション名 | 訪問プロファイル | イベントデータ |
| --- | :---: | :---: |
| サードパーティデータのアップロード | ✓ | ✗ |
| サードパーティデータの削除 | ✓ | ✗ |

アクションの名前を入力し、ドロップダウンメニューからアクションタイプを選択します。

次のセクションでは、各アクションのパラメータとオプションの構成方法について説明します。

### サードパーティデータのアップロード

#### パラメータ

| パラメータ | 説明 |
| --- | --- |
| データプロバイダーID | （必須）テクニカルアカウントマネージャーから提供されたプロバイダーID。 |
#### ID

少なくとも1つのIDパラメータが必要です。同じリクエストに複数のIDを含めることができます。The Trade Deskでは、以下のIDがサポートされています。

| パラメータ | 説明 |
| --- | --- |
| TDID | このユーザーのThe Trade Deskの36文字のGUID（ハイフンを含む）。 |
| DAID | このユーザーの未加工のデバイスID。36文字のGUID形式（ハイフンを含む）で送信します。iOSのIDFAまたはAndroidのAAIDを使用してください。 |
| UID2Token（SHA256でハッシュ化済み） | SHA256ですでにハッシュ化されている、ユーザーのUnified ID 2.0。 |
| UID2Token（SHA256ハッシュを適用） | SHA256ハッシュが適用される、ユーザーのUnified ID 2.0。 |
| UID2 | 44文字のBase64エンコードされたSHA-256文字列として表された、ユーザーのUnified ID 2.0。詳細については、[The Trade Desk Partner Portal：PIIの正規化とハッシュエンコーディング](https://partner.thetradedesk.com/v3/portal/data/doc/DataPiiNormalization)および[Unified ID](https://partner.thetradedesk.com/v3/portal/data/doc/UnifiedIDs)を参照してください。 |
| EUIDToken（SHA256でハッシュ化済み） | SHA256ですでにハッシュ化されている、ユーザーのEuropean Unified ID。 |
| EUIDToken（SHA256ハッシュを適用） | SHA256ハッシュが適用される、ユーザーのEuropean Unified ID。 |
| EUID | 44文字のBase64エンコードされたSHA-256文字列として表された、ユーザーのEuropean Unified ID。詳細については、[The Trade Desk Partner Portal：PIIの正規化とハッシュエンコーディング](https://partner.thetradedesk.com/v3/portal/data/doc/DataPiiNormalization)を参照してください。EUIDは、欧州および英国の市場要件を満たすよう設計されたユーザー向けの透明性とプライバシー制御を提供し、UID2と同じメールアドレスの正規化およびエンコーディングを必要とします。詳細については、[The Trade Desk Partner Portal：Unified ID](https://partner.thetradedesk.com/v3/portal/data/doc/UnifiedIDs)を参照してください。 |
| IDL | 49文字または70文字のRampID（旧称IdentityLink）。この値は、The Trade Desk専用にマッピングされたLiveRampのRampIDである必要があります。RampIDのマッピングの詳細については、[LiveRamp：LiveRampのSidecar](https://sidecar.readme.io/docs/getting-started)を参照してください。 |

#### データ

| パラメータ | 説明 |
| --- | --- |
| 名前 | （必須）セグメント名。最大128文字です。 |
| TTL（分） | （必須）有効期間（TTL）は、`TimeStampUtc`の値を基準として、このユーザーがアクティブな状態を維持する時間（分）です。TTLが期限切れになると、そのユーザーはターゲティングに使用されなくなります。TTLの最大値は259200分（180日）です。 |
| タイムスタンプ | ユーザーがセグメントの対象となった時点のタイムスタンプ。指定しない場合、データが処理された時刻に基づいてタイムスタンプが割り当てられます。このタイムスタンプは、ターゲティングおよび入札調整に使用するユーザーのリーセンシーを判定するために使用されます。 |

### サードパーティデータの削除

#### パラメータ

| パラメータ | 説明 |
| --- | --- |
| データプロバイダーID | 必須。テクニカルアカウントマネージャーから提供されたプロバイダーID。 |
| リクエストタイプ | <ul><li>**オプトアウト**：The Trade DeskはTTL値を`0`に構成して、データセグメントから該当IDをオプトアウトし、キャンペーンでのターゲティングを制限します。</li><li>**削除**：The Trade Deskは、データセグメントおよび`REDS`フィードを含むデータセットから該当IDを削除します。 |

#### ID

少なくとも1つのIDパラメータが必要です。同じリクエストに複数のIDを含めることができます。The Trade Deskでは、以下のIDがサポートされています。

| パラメータ | 説明 |
| --- | --- |
| TDID | このユーザーのThe Trade Deskの36文字のGUID（ハイフンを含む）。 |
| DAID | このユーザーの未加工のデバイスID。36文字のGUID形式（ハイフンを含む）で送信します。iOSのIDFAまたはAndroidのAAIDを使用してください。 |
| UID2Token（SHA256でハッシュ化済み） | SHA256ですでにハッシュ化されている、ユーザーのUnified ID 2.0。 |
| UID2Token（SHA256ハッシュを適用） | SHA256ハッシュが適用される、ユーザーのUnified ID 2.0。 |
| UID2 | 44文字のBase64エンコードされたSHA-256文字列として表された、ユーザーのUnified ID 2.0。詳細については、[The Trade Desk Partner Portal：PIIの正規化とハッシュエンコーディング](https://partner.thetradedesk.com/v3/portal/data/doc/DataPiiNormalization)および[Unified ID](https://partner.thetradedesk.com/v3/portal/data/doc/UnifiedIDs)を参照してください。 |
| EUIDToken（SHA256でハッシュ化済み） | SHA256ですでにハッシュ化されている、ユーザーのEuropean Unified ID。 |
| EUIDToken（SHA256ハッシュを適用） | SHA256ハッシュが適用される、ユーザーのEuropean Unified ID。 |
| EUID | 44文字のBase64エンコードされたSHA-256文字列として表された、ユーザーのEuropean Unified ID。詳細については、[The Trade Desk Partner Portal：PIIの正規化とハッシュエンコーディング](https://partner.thetradedesk.com/v3/portal/data/doc/DataPiiNormalization)を参照してください。EUIDは、欧州および英国の市場要件を満たすよう設計されたユーザー向けの透明性とプライバシー制御を提供し、UID2と同じメールアドレスの正規化およびエンコーディングを必要とします。詳細については、[The Trade Desk Partner Portal：Unified ID](https://partner.thetradedesk.com/v3/portal/data/doc/UnifiedIDs)を参照してください。 |
| RampID | 49文字または70文字のRampID（旧称IdentityLink）。これは、The Trade Desk専用にマッピングされたLiveRampのRampIDである必要があります。詳細については、[LiveRamp：LiveRampのSidecar](https://sidecar.readme.io/docs/getting-started)を参照してください。 |