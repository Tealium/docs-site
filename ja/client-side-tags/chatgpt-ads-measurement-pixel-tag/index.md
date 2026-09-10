---
title: ChatGPT広告測定ピクセルタグ
description: この記事では、Tealium iQタグ管理アカウントでChatGPT広告測定ピクセルタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/chatgpt-ads-measurement-pixel-tag/
---
ChatGPT広告測定ピクセルを使用すると、ウェブサイト上のコンバージョンや顧客アクションを測定し、ChatGPT広告キャンペーンを最適化することができます。

## タグのヒント

* **イベント**タブを使用して、データレイヤー変数をChatGPT広告の標準イベントタイプのいずれかに接続します。タグはマッチしたトリガーごとに1回の測定を行います。
* **構成**タブを使用して、発火ごとに**ピクセルID**または**カスタムSDK URL**を上書きします（例：マルチブランドプロファイルの場合）。イベントレベルのオプションと同意、および**Eコマース**タブで注文合計、通貨、製品ごとの配列を使用します。**イベント固有のパラメータ**タブを使用して、単一イベントのいずれかを上書きします。
* グローバル値はイベントごとに自動的にフィルタリングされます。例えば、`plan_id`は`subscription_created`、`trial_started`、`custom`イベントにのみ添付されます。
* ページビューと購入はデフォルトで自動発火します。**自動ページビュー**および**自動注文作成**オプションを介して無効にします。
* 以下のEコマース拡張パラメータをサポートします：
    * 小計（`_csubtotal`）
    * 通貨（`_ccurrency`）
    * 注文ID（`_corder`）
    * 製品IDリスト（`_cprod`）
    * 製品名リスト（`_cprodname`）
    * カテゴリリスト（`_ccat`）
    * 数量リスト（`_cquan`）
    * 価格リスト（`_cprice`）
* **金額**と**製品金額**は主要単位でマッピングされます（例：129.99）。タグはChatGPT広告測定ピクセルAPIに従って整数の小単位に変換します。
* **製品タイプ**がマッピングされていない場合、内容はデフォルトで`product`になり、すべての呼び出しがベンダーの検証を通過します。
* カスタムChatGPT広告イベントを発火するには、**イベント**または**イベント固有のパラメータ**タブで**カスタム**を選択し、表示されるフィールドにベンダーイベント名を入力します。ここでマッピングされたイベント名がChatGPT広告の標準イベントリストにない場合、その名前で`custom`イベントとして自動的にルーティングされます。
* **ピクセルID**はOpenAIアカウントチームから取得します。ChatGPT広告マネージャーを通じたセルフサービスのプロビジョニングはサポートされていません。
* `utag.gdpr.getConsentState()`を介してTealiumの同意状態を尊重し、同意が拒否された場合は発火をスキップします。**同意**先をマッピングして、直接Measurement Pixel SDKに許可または撤回を転送します。
* **ユーザーオブジェクト**フィールド（メール、電話、IPなど）は送信しないでください。

## タグの構成

タグマーケットプレースにアクセスして新しいタグを追加します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加する際には、以下の構成を構成します：

* **ピクセルID**：あなたのChatGPT広告ピクセルID。この値はOpenAIアカウントチームから取得します。
* **デバッグモード**：ブラウザコンソールでMeasurement Pixel SDKのデバッグログを有効にします。
* **カスタムSDK URL**：（オプション）基本URLを上書きします。
* **自動ページビュー**：すべてのTealiumビューイベントで`page_viewed`を自動キューします（デフォルト`true`）。`page_viewed`が明示的な**イベント**タブトリガーからすでにキューされている場合はスキップします。
* **自動注文作成**：**Eコマース**拡張機能が`_corder`を構成し、`order_created`がまだキューされていない場合、`order_created`を自動キューします（デフォルト`true`）。
* **イベントID生成**：すべてのOpenAIトラッキングイベントに対して一意のイベントIDを自動生成します。

## 読み込みルール

すべてのページでタグを読み込むか、タグが読み込まれる条件を構成します。詳細については、[読み込みルールについて](https://docs.tealium.com/about-load-rules/)を参照してください。

## データマッピング

データマッピングは、データレイヤー変数からベンダータグの対応する宛先変数へのデータ送信プロセスです。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

利用可能なカテゴリは次のとおりです：

### 構成

| 変数 | タイプ/値 | 説明 |
|:---------|:-----|:------------|
| `pixel_id` | `String` | ピクセルID |
| `custom_sdk_url` | `String` | カスタムSDK URL |


### 一般

| 変数 | タイプ/値 | 説明 |
|:---------|:-----|:------------|
| `event_id` | `String` | イベントID |
| `plan_id` | `String` | プランID |
| `consent` | `String` | 同意 |


### Eコマース

| 変数 | タイプ/値 | 説明 |
|:---------|:-----|:------------|
| `amount` | `Integer` | 金額（`_csubtotal`を上書き） |
| `currency` | `String` | 通貨（`_ccurrency`を上書き） |
| `product_id` | `Array` | 製品ID（`_cprod`を上書き） |
| `product_name` | `Array` | 製品名（`_cprodname`を上書き） |
| `product_type` | `Array` | 製品タイプ（`_ccat`を上書き） |
| `product_quantity` | `Array` | 製品数量（`_cquan`を上書き） |
| `product_amount` | `Array` | 製品金額（`_cprice`を上書き） |
| `product_currency` | `Array` | 製品通貨（`_ccurrency`を上書き） |


### イベント固有のパラメータ

イベントをマッピングするには、[イベントマッピングの作成](https://docs.tealium.com/ja/iq-tag-management/data-mappings/manage/#add-an-event-mapping)を参照してください

| イベント | 説明 |
|:------|:------------|
| `event_id` | イベントID |
| `amount` | 金額（`_csubtotal`を上書き） |
| `currency` | 通貨（`_ccurrency`を上書き） |
| `plan_id` | プランID |
| `id` | 製品ID（`_cprod`を上書き） |
| `name` | 製品名（`_cprodname`を上書き） |
| `content_type` | 製品タイプ（`_ccat`を上書き） |
| `quantity` | 製品数量（`_cquan`を上書き） |
| `amount` | 製品金額（`_cprice`を上書き） |
| `currency` | 製品通貨（`_ccurrency`を上書き） |