---
title: Optimizely イベントコネクタ構成ガイド（レガシー）
description: この記事では、Customer Data Hub アカウントで Optimizely イベントコネクタを構成する方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/optimizely-events-connector-legacy/
---
このコネクタの[更新バージョン]()が現在利用可能です。このバージョンは、システムに既に構成されている場合は引き続き使用できますが、マーケットプレイスではもう提供されていません。

## コネクタアクション

| アクション名 | AudienceStream | EventStream |
| --- | :---: | :---: |
|イベント送信| ✗| ✓|

## 構成の構成

コネクタマーケットプレイスにアクセスし、新しいコネクタを追加します。コネクタを追加する一般的な手順については、[コネクタ概要]()の記事を参照してください。

コネクタを追加した後、以下の構成を構成します：

* **パーソナルトークン**
  * 認証には、次のリンクから生成されたリクエストヘッダーのトークンを使用します：&lt;http://app.optimizely.com/v2/profile/api&gt;。
  * このドキュメントのすべてのAPIリクエスト例は、同じヘッダーを使用します。
  * 認証の詳細については、[パーソナルトークン](https://developers.optimizely.com/x/authentication/personal-token)を参照してください。

## アクション構成 - パラメータとオプション

**次へ**をクリックするか、**アクション**タブに進みます。ここでコネクタアクションを構成します。

このセクションでは、各アクションのパラメータとオプションの構成方法について説明します。

### アクション - イベント送信

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|アカウントID|  &lt;ul&gt;&lt;li&gt;これらのイベントが帰属するOptimizelyアカウント。&lt;/li&gt;&lt;/ul&gt; |
|決定の充実|  &lt;ul&gt;&lt;li&gt;値は `true` または `false`。&lt;/li&gt;&lt;li&gt;Optimizely Easy Event Tracking機能を有効にするには `true` に構成します。&lt;/li&gt;&lt;li&gt;このフィールドの詳細については、[イベントAPIリファレンス](https://developers.optimizely.com/x/events/api/#api_reference)を参照してください。&lt;/li&gt;&lt;li&gt;[Optimizelyがコンバージョンをどのようにカウントするか](https://help.optimizely.com/Analyze_Results/How_Optimizely_counts_conversions)も参照してください。&lt;/li&gt;&lt;/ul&gt; |
|キャンペーンID|  &lt;ul&gt;&lt;li&gt;(必須) この実験を含むキャンペーンのID。&lt;/li&gt;&lt;/ul&gt; |
|実験ID|  &lt;ul&gt;&lt;li&gt;(必須) 訪問が参加した実験のID。&lt;/li&gt;&lt;li&gt;パーソナライゼーションキャンペーンの場合、実験にバケットされていない訪問には `null` を明示的に送信し、キャンペーンのリーチを正確に計算します。&lt;/li&gt;&lt;/ul&gt; |
|バリエーションID|  &lt;ul&gt;&lt;li&gt;(必須) 訪問が参加したバリエーションのID。&lt;/li&gt;&lt;li&gt;パーソナライゼーションキャンペーンの場合、実験にバケットされていない訪問には `null` を明示的に送信し、キャンペーンのリーチを正確に計算します。&lt;/li&gt;&lt;/ul&gt; |
|キャンペーンホールドバック|  &lt;ul&gt;&lt;li&gt;値は `true` または `false`。&lt;/li&gt;&lt;li&gt;`true` の場合、選択された体験はキャンペーンレベルで保留されました。&lt;/li&gt;&lt;li&gt;パーソナライゼーションの場合に必要です。それ以外の場合は省略します。&lt;/li&gt;&lt;/ul&gt; |
|タイムスタンプ|  &lt;ul&gt;&lt;li&gt;(必須) イベントが生成されたタイムスタンプ。Unixエポックからのミリ秒でフォーマットされます。&lt;/li&gt;&lt;li&gt;ユーザーが値を提供しない場合、デフォルトで `{{unixTimestampMs}}` を送信します。&lt;/li&gt;&lt;/ul&gt; |
|UUID|  &lt;ul&gt;&lt;li&gt;(必須) このイベントの一意の識別子。&lt;/li&gt;&lt;li&gt;`{{uuid}}` を使用して自動的に作成されます。&lt;/li&gt;&lt;li&gt;Optimizelyのバックエンドは、同じ `entity_id`、`uuid`、および `timestamp` を持つイベントを検出し、そのうちの1つだけを保存します。&lt;/li&gt;&lt;li&gt;送信前に各イベントが一意の `uuid` または `timestamp` を使用していることを確認してください。&lt;/li&gt;&lt;/ul&gt; |
|エンティティID|  &lt;ul&gt;&lt;li&gt;(オプション) この属性に対応するエンティティのID。&lt;/li&gt;&lt;li&gt;カスタム属性 (`type=&#34;custom&#34;`) の場合のみ必要です。&lt;/li&gt;&lt;li&gt;他の属性タイプでは無効です。&lt;/li&gt;&lt;/ul&gt; |
|イベント名|  &lt;ul&gt;&lt;li&gt;このイベントのイベントキー（別名 API 名）。&lt;/li&gt;&lt;/ul&gt; |
|イベントデータ|  &lt;ul&gt;&lt;li&gt;キーと値のペアでの追加イベントデータ。&lt;/li&gt;&lt;/ul&gt; |
|タグ|  &lt;ul&gt;&lt;li&gt;(オプション) タグに関連するキー値属性。&lt;/li&gt;&lt;li&gt;使用する場合、`type` と `value` をキーとして含める必要があります。&lt;/li&gt;&lt;/ul&gt; |
|イベントタイプ|  &lt;ul&gt;&lt;li&gt;イベントのタイプ。&lt;/li&gt;&lt;li&gt;例えば、`decision_point` を示すためには、タイプは `campaign_activated` であるべきです。&lt;/li&gt;&lt;/ul&gt; |
|イベント値|  &lt;ul&gt;&lt;li&gt;イベントに関連するスカラー値。&lt;/li&gt;&lt;li&gt;これは収益以外の数値であるべきです。&lt;/li&gt;&lt;/ul&gt; |
|訪問ID|  &lt;ul&gt;&lt;li&gt;(必須) 訪問の一意の識別子。&lt;/li&gt;&lt;/ul&gt; |
|属性|  &lt;ul&gt;&lt;li&gt;このリクエストの時点でこの訪問に関連する属性。&lt;/li&gt;&lt;/ul&gt; |
|セッションID|  &lt;ul&gt;&lt;li&gt;これらのイベントのセッションコンテキスト（ある場合）を識別する一意の識別子。&lt;/li&gt;&lt;li&gt;省略された場合、Optimizelyのバックエンドはセッションを推測し、与えられた `visitor_id` から最初のイベントを受け取ったときにセッションを開始し、その訪問に対して30分間イベントが受信されない場合にセッションを終了します。&lt;/li&gt;&lt;li&gt;最大セッションサイズは24時間です。&lt;/li&gt;&lt;/ul&gt; |
|IP匿名化|  &lt;ul&gt;&lt;li&gt;Optimizelyは通常、各リクエストのクライアントIPアドレスを保存します。&lt;/li&gt;&lt;li&gt;値は `true` または `false`。&lt;ul&gt;&lt;li&gt;このフラグが `true` に構成されている場合、IPアドレスの最後のオクテットは切り捨てられてから保存されます。&lt;/li&gt;&lt;li&gt;`false` に構成されている場合、IPアドレス全体が保存されます。&lt;/li&gt;&lt;/ul&gt; &lt;/li&gt;&lt;li&gt;このAPIの消費者がウェブブラウザーやモバイルクライアントのコンテキストで実装され、エンドユーザーの識別情報の保存を制限するポリシーや規制の対象となっている場合に最も関連があります。&lt;/li&gt;&lt;li&gt;このフラグは、アカウントおよびプロジェクトの構成のIP匿名化構成とは独立しており、Optimizelyクライアントがこのフラグを構成する方法のみを制御します。&lt;/li&gt;&lt;li&gt;このフラグが構成されている場合、IPフィルタリング機能を使用する際には注意が必要です。完全に修飾された明示的なIPアドレスはフィルタとして機能しません（匿名化はイベントがIPによってフィルタリングされる前に行われます）。&lt;/li&gt;&lt;/ul&gt; |
|クライアント名|  &lt;ul&gt;&lt;li&gt;デバッグ目的で推奨されます。&lt;/li&gt;&lt;li&gt;このイベントを生成したシステムの一意の識別子。&lt;/li&gt;&lt;li&gt;慣例により、次の例に似た形式であるべきです：`organization_name/system_name`&lt;/li&gt;&lt;li&gt;イベントAPIの完全な説明については、[イベントAPIリファレンス](https://developers.optimizely.com/x/events/api/#api_reference)を参照してください。&lt;/li&gt;&lt;/ul&gt; |
|クライアントバージョン|  &lt;ul&gt;&lt;li&gt;デバッグ目的で推奨されます。&lt;/li&gt;&lt;li&gt;このイベントを生成したシステムのバージョン識別子。&lt;/li&gt;&lt;/ul&gt; |
|プロジェクトID|  &lt;ul&gt;&lt;li&gt;(オプション) Recommendations製品を使用している場合のみ、プロジェクトIDを渡す必要があります。&lt;/li&gt;&lt;/ul&gt; |
