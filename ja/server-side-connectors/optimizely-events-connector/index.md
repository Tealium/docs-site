---
title: Optimizely イベントコネクタ構成ガイド
description: この記事では、Customer Data Hub アカウントで Optimizely イベントコネクタを構成する方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/optimizely-events-connector/
---
## コネクタアクション

| **アクション名**  | **AudienceStream** | **EventStream** |
|:-----------------------------|:-------------------|:----------------|
| イベント追跡（ユーザーをアクティブ化） | ✓  | ✓ |

## 構成の構成

コネクタマーケットプレイスに移動して新しいコネクタを追加します。コネクタを追加する一般的な手順については、[コネクタ概要]()の記事を読んでください。

コネクタを追加した後、以下の構成を構成します：

* **アカウントID**  
イベントを帰属させる Optimizely アカウント。
* **アクセストークン**  
**[Optimizely プロファイル &gt; API アクセス](https://app.optimizely.com/v2/profile/api)** にアクセスして取得できます。

## アクション構成 - パラメータとオプション

**次へ** をクリックするか、**アクション** タブに移動します。ここでコネクタアクションを構成します。

このセクションでは、各アクションのパラメータとオプションの構成方法について説明します。

### アクション - イベント追跡（ユーザーをアクティブ化）

#### パラメータ

| **パラメータ** | **説明**  |
|:--------------|:-----------------|
| ビジターID  | &lt;ul&gt;&lt;li&gt;(必須) ビジターの一意の識別子。&lt;/li&gt;&lt;/ul&gt;  |
| セッションID  | &lt;ul&gt;&lt;li&gt;イベントに対するセッションコンテキストを識別する一意の識別子（ある場合）。省略された場合、Optimizely のバックエンドはセッションを推測し、`visitor_id` から最初のイベントを受信したときにセッションを開始し、そのビジターに対して30分間イベントが受信されない場合にセッションを終了します。&lt;/li&gt;&lt;li&gt;最大セッションサイズは24時間です。&lt;/li&gt;&lt;/ul&gt; |
| プロジェクトID  | &lt;ul&gt;&lt;li&gt;(オプション) Recommendations 製品を使用している場合のみ、プロジェクトIDを渡す必要があります。&lt;/li&gt;&lt;/ul&gt;   |
| IP匿名化  | &lt;ul&gt;&lt;li&gt;Optimizely は通常、各リクエストのクライアントIPアドレスを保存します。&lt;/li&gt;&lt;li&gt;値は `true` または `false` です。&lt;ul&gt;&lt;li&gt;このフラグが `true` に構成されている場合、IPアドレスの最後のオクテットが切り捨てられてから保存されます。&lt;/li&gt;&lt;li&gt;`false` に構成されている場合、IPアドレス全体が保存されます。&lt;/li&gt;&lt;/ul&gt;&lt;/li&gt;&lt;li&gt;このAPIをウェブブラウザーやモバイルクライアントコンテキストで実装し、エンドユーザー識別情報の保存を制限するポリシーや規制の対象となる消費者にとって最も関連があります。&lt;/li&gt;&lt;li&gt;このフラグは、アカウントおよびプロジェクトの構成のIP匿名化構成とは独立しており、Optimizely クライアントがこのフラグをどのように構成するかを制御するだけです。&lt;/li&gt;&lt;li&gt;このフラグが構成されている場合、IPフィルタリング機能を使用する際には注意が必要です。完全なIPアドレスはフィルタとして機能しません（匿名化はイベントがIPによってフィルタリングされる前に行われます）。&lt;/li&gt;&lt;/ul&gt; |
| 決定の充実  | &lt;ul&gt;&lt;li&gt;値は `true` または `false` です。&lt;/li&gt;&lt;li&gt;Optimizely Easy Event Tracking 機能を有効にするために `true` に構成する必要があります。&lt;/li&gt;&lt;li&gt;このフィールドについての詳細は、[イベント API リファレンス](https://developers.optimizely.com/x/events/api/#api_reference)を参照してください。&lt;/li&gt;&lt;li&gt;[Optimizely がコンバージョンをどのようにカウントするか](https://help.optimizely.com/Analyze_Results/How_Optimizely_counts_conversions)も参照してください。&lt;/li&gt;&lt;/ul&gt;  |
| クライアント名 | &lt;ul&gt;&lt;li&gt;デバッグ目的で推奨されます。&lt;/li&gt;&lt;li&gt;このイベントを生成したシステムの一意の識別子。&lt;/li&gt;&lt;li&gt;慣例により、次の例に似た形式であるべきです：`organization_name/system_name`&lt;/li&gt;&lt;li&gt;イベント API の完全な説明については、[イベント API リファレンス](https://developers.optimizely.com/x/events/api/#api_reference)を参照してください。&lt;/li&gt;&lt;/ul&gt; |
| クライアントバージョン  | &lt;ul&gt;&lt;li&gt;デバッグ目的で推奨されます。&lt;/li&gt;&lt;li&gt;このイベントを生成したシステムのバージョン識別子。&lt;/li&gt;&lt;/ul&gt;   |
| タイムスタンプ | &lt;ul&gt;&lt;li&gt;(必須) イベントが生成されたタイムスタンプ。Unix エポックからのミリ秒単位でフォーマットされます。&lt;/li&gt;&lt;li&gt;マッピングされていない場合、コネクタの発火時間が使用されます。&lt;/li&gt;&lt;/ul&gt; |
| UUID  | &lt;ul&gt;&lt;li&gt;(必須) このイベントの一意の識別子。&lt;/li&gt;&lt;li&gt;`{{uuid}}` を使用して自動的に作成されます。&lt;/li&gt;&lt;li&gt;Optimizely のバックエンドは、誤ってまたは誤ってリプレイされたリクエストを重複排除するために使用します。&lt;/li&gt;&lt;li&gt;同じ `entity_id`、`uuid`、および `timestamp` を持つイベントを検出し、そのうちの1つだけを保存します。&lt;/li&gt;&lt;li&gt;送信する前に各イベントが一意の `uuid` または `timestamp` を使用していることを確認してください。&lt;/li&gt;&lt;/ul&gt;  |
| エンティティID | &lt;ul&gt;&lt;li&gt;(オプション) この属性に対応するエンティティのID。&lt;/li&gt;&lt;li&gt;カスタム属性 (`type=&#34;custom&#34;`) の場合のみ必要です。&lt;/li&gt;&lt;li&gt;他の属性タイプでは無効です。&lt;/li&gt;&lt;/ul&gt; |
| キー | &lt;ul&gt;&lt;li&gt;キー&lt;/li&gt;&lt;/ul&gt;  |
| 数量  | &lt;ul&gt;&lt;li&gt;数量&lt;/li&gt;&lt;/ul&gt;   |
| 収益 | &lt;ul&gt;&lt;li&gt;収益&lt;/li&gt;&lt;/ul&gt;  |
| タイプ  | &lt;ul&gt;&lt;li&gt;イベントのタイプ。&lt;/li&gt;&lt;li&gt;例えば、`decision_point` を示すためには、タイプは `campaign_activated` であるべきです。&lt;/li&gt;&lt;/ul&gt; |
| イベントタグ  | &lt;ul&gt;&lt;li&gt;(オプション) 追加のイベントプロパティ。&lt;/li&gt;&lt;li&gt;タグに関連するキー値属性。&lt;/li&gt;&lt;li&gt;使用する場合、`type` と `value` をキーとして含める必要があります。&lt;/li&gt;&lt;/ul&gt;  |
| イベントプロパティ  | イベントの特性または特性を定義するキー値ペア。  |
| キャンペーンID | &lt;ul&gt;&lt;li&gt;(必須) この実験を含むキャンペーンのID。&lt;/li&gt;&lt;/ul&gt;  |
| 実験ID | &lt;ul&gt;&lt;li&gt;(必須) ビジターが露出した実験のID。&lt;/li&gt;&lt;li&gt;パーソナライゼーションキャンペーンの場合、実験にバケットされていないビジターに対しては `null` を明示的に送信し、キャンペーンのリーチを正確に計算します。&lt;/li&gt;&lt;/ul&gt;  |
| バリエーションID  | &lt;ul&gt;&lt;li&gt;(必須) ビジターが露出したバリエーションのID。&lt;/li&gt;&lt;li&gt;パーソナライゼーションキャンペーンの場合、実験にバケットされていないビジターに対しては `null` を明示的に送信し、キャンペーンのリーチを正確に計算します。&lt;/li&gt;&lt;/ul&gt; |
| キャンペーンホールドバック | &lt;ul&gt;&lt;li&gt;値は `true` または `false` です。&lt;/li&gt;&lt;li&gt;`true` の場合、選択された体験はキャンペーンレベルで保留されました。&lt;/li&gt;&lt;li&gt;パーソナライゼーションの場合に必要です。それ以外の場合は省略します。&lt;/li&gt;&lt;/ul&gt;  |
| タイプ  | &lt;ul&gt;&lt;li&gt;(必須) `custom` である可能性があります&lt;/li&gt;&lt;/ul&gt;   |
| 値 | &lt;ul&gt;&lt;li&gt;必須&lt;/li&gt;&lt;/ul&gt;   |
| エンティティID | &lt;ul&gt;&lt;li&gt;カスタム属性タイプの場合に必要です。&lt;/li&gt;&lt;/ul&gt;  |

## 追加情報

* [Optimizely イベント API](https://docs.developers.optimizely.com/web/docs/event-api)