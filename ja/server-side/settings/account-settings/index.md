---
title: サーバーサイドのアカウント構成
description: この記事では、Customer Data Hubのすべてのプロファイル構成について説明します。
url: https://docs.tealium.com/ja/server-side/settings/account-settings/
---
プロファイル構成を表示するには、アカウントにログインし、画面右上にある自分のイニシャルをクリックします。次に、ドロップダウンリストから **Server-Side Settings** を選択します。

編集可能な構成を変更した後、**Save**、続いて **Save/Publish** をクリックして変更を適用します。


<blockquote>
読み取り専用（編集不可）の構成は、Tealiumサポートまたはアカウントマネージャーのみが変更できます。
</blockquote>


## 一般構成

* **Enable Concurrency**（読み取り専用）：アカウント管理者が、プロファイルレベルでServer-Side Concurrencyの有効／無効を切り替えられるようにします。
* **Enable Customer Data Platform**（読み取り専用）：現在のプロファイルで、顧客データおよびオーディエンスのアクティベーション機能を有効にします。
* **Customer Data Platform - Event Filter**（読み取り専用）：**Event Attribute** の名前と値を入力します（大文字と小文字は区別されません）。この条件に一致するイベントのみが顧客データプラットフォームに送信されます。これらのフィールドを空のままにすると、すべてのイベントが送信されます。
    
<blockquote>
フィルターで指定できる属性名と値は1組だけですが、イベントフィルターはサーバーサイドのエンリッチメントが適用された後に適用されます。そのため、エンリッチメントとルールを使用してカスタム属性に基づく、より複雑なフィルタリングを実行できます。
</blockquote>

* **Visitor Stitching**（読み取り専用）：同一の訪問から発生した場合に、プラットフォーム、デバイス、ブラウザーをまたいで訪問プロファイルを統合します。デフォルト値は **ON** です。
* **Profile Retention Time**（読み取り専用）：訪問プロファイルの保持期間を構成します。訪問の最後のイベントを基準として、保持期間が日数単位で開始されます。
* **Display/UI Time Zone**（読み取り専用）：Customer Data Hubダッシュボードで表示するタイムゾーンを選択します。
    * オプションは **Greenwich Mean Time (GMT)** または **Local Time** です。
    * **Local Time** を選択すると、現在ログインしているユーザーのブラウザー時刻が表示されます。
* **Enable Rule Dependency Checking**：ルールに対する属性の依存関係が取得され、正しい順序で実行されるようにします。デフォルト値は **ON** です。
    
<blockquote>
このオプションは **On** に構成することをお勧めします。この構成が **Off** の場合、実行順序の計算時にルールが考慮されません。そのため、ルールに依存関係がある場合、エンリッチメントが正しい順序で実行されることは保証されません。
</blockquote>

* **Enable Visitor IP Attribute**（読み取り専用）：訪問のIPアドレスを **Client IP** という名前の属性として使用できるようにします。この属性はコネクターにマッピングでき、エンリッチメントやルールでも使用できます。
    * データレイヤーのエンリッチメントキー：`client_ip`。
    * AudienceStoreでは `current_visit.last_event.client_ip` として使用できます。
    * デフォルト値は **OFF** です。
    
<blockquote>
Client IP属性は、**Live Events** または **Trace** には表示されません。これらで属性の値を確認するには、Client IP属性を使用して別の属性をエンリッチしてください。
</blockquote>

* **Enrichment Order Respects UI Order**：エンリッチメントの順序がユーザーインターフェイス上の表示順に従うようにするには、このオプションを有効にします。
    * デフォルト値は **ON** です。
* **Usage Report Start Date**（読み取り専用）：使用状況レポートのデフォルトの開始日として使用する日付を構成します。

## DataAccess

* **Event Data Storage**（読み取り専用）：アカウントでEvent Data Storageを有効にします。
    * Event Data Storageを有効にするには、署名済みの契約が必要です。
* **Audience Data Storage**（読み取り専用）：アカウントでAudience Data Storageを有効にします。
    * Audience Data Storageを有効にするには、署名済みの契約が必要です。
* **EventStore Retention Time**（読み取り専用）：EventStoreのデータを保持する期間を指定します。
    * デフォルト値は **30日** です。
* **EventDB Retention Time**（読み取り専用）：EventDBのデータを保持する期間を指定します。
    * デフォルト値は **90日** です。

## イベントアクティベーション

* **Enable Event Activation**（読み取り専用）：現在のプロファイルで、イベントアクティベーションと関連するコネクターを有効にします。
    * デフォルト値は **ON** です。

## リージョン

* **Region**（読み取り専用）：リージョンは、データの権威保存ロケーションです。通常は、顧客の大部分に最も近い地理的位置を選択してください。
    * 一部のお客様には、データを特定の地理的位置に保存することを義務付ける法的制限があります。
    * このプロファイルに最適なリージョンが不明な場合は、**Oregon** を選択し、Customer Success LeadershipにOptimal Authority Regionレポートを依頼してください。数日分のデータを収集した後、推奨リージョンが提示されます。
    
<blockquote>
不適切なリージョンで収集されたデータは破棄される可能性があります。
</blockquote>


## 1日あたりの訪問クエリ上限

* **Sample Size of Daily Visitors to Process**（読み取り専用）：**Audience Sizing** および **Audience Discovery** のクエリで結果を予測するために使用する訪問のサンプルサイズを指定します。
    * Audience Sizingジョブは、サンプル内の訪問だけでなく、一致した訪問全体に対して実行されます。詳細については、[Audience Sizing]()を参照してください。
    * デフォルト値は **100000** です。

## Predict

* **Enable Predict Premium**（読み取り専用）：プロファイルでPredict Premiumプランを有効にします。
    * この機能を有効または無効にする際は、現在の契約内容に合わせて **Max Number of Model Trainings** と **Max Number of Concurrently Deployed Models** を調整してください。

## 同意の適用

* **Legacy Consent Enforcement**：有効にすると、[従来の同意カテゴリ適用ルール](https://docs.tealium.com/server-side-consent-management/)が現在のプロファイルに適用されます。
    * 事前定義された同意カテゴリに基づく従来の同意条件を満たさない限り、イベントアクションはブロックされます。
    * 既存のプロファイルではデフォルトで有効です。新しく作成されたプロファイル、または[同意オーケストレーション](https://docs.tealium.com/about-consent-orchestration/)を使用するプロファイルでは無効です。
    * 同意オーケストレーションを無効にしても、従来の適用構成は変更されません。手動で調整しない限り、運用の継続性が維持されます。


<blockquote>
同意オーケストレーションにアクティブな目的グループがある間は、この構成をオンにできません。
</blockquote>
