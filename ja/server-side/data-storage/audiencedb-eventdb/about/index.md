---
title: AudienceDBとEventDBについて
description: この記事では、AudienceDBとEventDBの操作方法について説明します。
url: https://docs.tealium.com/ja/server-side/data-storage/audiencedb-eventdb/about/
---
EventDBとAudienceDBをアカウントとプロファイルで有効にするには、カスタマーサクセスマネージャーに連絡してください。

## 動作原理

AudienceDBとEventDBサービスは、PostgreSQLに基づいたデータウェアハウスであるAmazon Redshiftに構造化されたオーディエンスデータとイベントデータを保存します。お好みのSQLクライアントやビジネスインテリジェンス（BI）ツールを使用して、Amazon Redshiftでデータをクエリしたり分析したりすることができます。

EventDBはEventStoreをデータソースとして使用し、EventStore S3バケットからTealiumが提供するAmazon Redshiftデータベースにデータをインポートします。

AudienceStoreはAudienceDBをアクティブにするための前提条件ではありません。これらのサービスは独立して運用されます。AudienceDBは、各訪問セッションの終了時に訪問プロファイルデータを保存します。

AudienceDBとEventDBが有効になった後、保存される属性を選択する必要があります。詳細については、[AudienceDBとEventDBの構成]()を参照してください。

### データ保存タイミング

新しいデータは、Redshiftクラスターの負荷に応じて、EventDBとAudienceDBに30分から90分以内に保存されます。

### データベーススキーマ

EventDBとAudienceDBが有効になると、Amazon Redshiftにデータを保存するためのデータベースが作成されます。各プロファイルは同じRedshiftインスタンス内に独自のデータベーススキーマを持ち、それぞれのデータベーススキーマ（プロファイル）に対してユーザー名とパスワードがあります。AudienceDBとEventDBのデータベーススキーマは、プロファイルに対してEventDBまたはAudienceDBが有効になったときに自動的に作成されます。

### データ保持

EventDBとAudienceDBに保存されたデータは、契約で定められた期間、Amazon RedShiftに保持されます。イベント、訪問、または訪問レコードが有効期限に達すると、そのレコードは自動的に削除されます。訪問レコードが更新された場合でも、有効期限は変わらず、レコードは削除されます。

契約の条件を確認するためにアカウントマネージャーに連絡してください。

詳細については、[サーバーサイドアカウント構成]()を参照してください。

#### EventDBとAudienceDBに保存された属性の変更

EventDBに以前追加された属性を削除すると、その属性はEventDBに送信されなくなり、EventDBからも削除されます。EventDBの属性の変更はEventStoreファイルには影響しません。

AudienceDBに以前追加された属性を削除すると、その属性はAudienceDBに送信されなくなり、AudienceDBからも削除されます。AudienceDBの属性の変更はAudienceStoreファイルには影響しません。

## テーブル、ビュー、および正規化ビュー

Redshiftデータベースのテーブルの列名は、属性タイプと内部属性IDによって命名されます。データのビューと正規化ビューはテーブルと同じデータを含んでいますが、クエリを書きやすくするためにユーザーフレンドリーな名前が使われています。正規化ビューの名前はビューの名前に似ていますが、テーブル名から属性IDが省略されています。テーブル名とビュー名は次のように作成されます：

* **テーブル名**  
列名は属性タイプと属性IDの組み合わせです。  
例：`badge_30`
* **ビュー名**  
列名はユーザーフレンドリーな名前と属性IDの組み合わせです。  
例：`visitor - badge - fan (30)`
* **正規化ビュー名**  
列名は属性IDなしのユーザーフレンドリーな名前です。  
例：`visitor - badge - fan`

ビューと正規化ビューは、`SUM()`、`MIN()`、`MAX()`などの集計を含むクエリの実行を簡素化します。

## AudienceDBのテーブル

訪問と訪問の属性は、その属性タイプと名前に応じてデータベーステーブルの列に保存されます。オーディエンスは訪問テーブルの列として保存されます。テーブルのキーは`visit_id`または`visitor_id`です。

訪問と訪問データのための次のテーブルがあります：

* 訪問/セッションデータ：`visits`
* 訪問データ：`visitors`

さらに、特別な属性タイプのための次のテーブルが存在します：

* 配列：`visit_arrays`, `visitor_arrays`
* 文字列のセット：`visit_lists`, `visitor_lists`
* 集計：`visit_tallies`, `visitor_tallies`

詳細については、[AudienceDBデータガイド]()を参照してください。

## EventDBのテーブル

EventDBのテーブルデータには、イベントフィードのすべてのイベントのイベント属性が含まれます。テーブルの列名は属性タイプと名前によって命名され、一部の属性は内部IDを参照しています。標準のUniversal Data Object (UDO)変数は`udo_`プレフィックスで命名され、ほとんどの列名は対応する属性名と一致します。例：`udo_event_name`。追加情報については、[ライブイベントとフィード]()を参照してください。

Tealium Collectタグからのイベントデータには、ページで実行されたタグとページパフォーマンスメトリックに関する情報も含まれます。詳細については、[Tealium Collect]()を参照してください。

イベントデータのための次のテーブルがあります：

* イベントフィードデータ：`events_{FEED}`
