---
title: インストール
description: Google Tag Manager向けTealium Collectのインストール方法について説明します。
url: https://docs.tealium.com/ja/platforms/google-tag-manager/install/
---
## 要件

* [Tealium Customer Data Hubアカウント](https://docs.tealium.com/introduction-to-customer-data-hub/)

## 仕組み

Google Tag Manager向けTealium Collect Tagは、ページごとに1回、TealiumからTealium Collect JavaScriptファイルを読み込むカスタムテンプレートです。

タグがトリガーされるイベントごとに、タグは自動的に`dataLayer`オブジェクトをキーと値のペアにフラット化し、データをTealiumのデータ収集エンドポイントに送信します。ファーストパーティデータ収集を使用する場合は、カスタムエンドポイントを使用できます。

フラット化される前のGoogle Tag Managerイベントは次のとおりです。

```
dataLayer.push({
  'ecommerce': {
    'purchase': {
      'actionField': {
        'id': 'T12345',
...
```

フラット化されると、次のTealiumイベントになります。

```
"tealium_event": "purchase"
"ecommerce.purchase.actionField.id": "T12345"
...
```

## インストール

Google Tag ManagerにTealium Collect Tagを追加するには、次の手順を実行します。

1. Google Tag Managerの左側のナビゲーションで、**テンプレート**をクリックします。
2. **タグ テンプレート**画面で、**ギャラリーを検索**をクリックします。
3. 「Tealium Collect Tag」を検索して選択します。
4. **ワークスペースに追加**をクリックしてテンプレートを追加します。
5. 「コミュニティ テンプレートを追加しますか？」画面で、**追加**をクリックします。

### 新しいタグの追加

Tealium Collect Tagのインスタンスを追加するには、次の手順を実行します。

1. Google Tag Managerの左側のナビゲーションで、**タグ**をクリックします。
2. **新規**ボタンをクリックします。
3. 「タグの構成」をクリックしてタグタイプを選択します。リストから「Tealium Collect Tag」を検索して選択します。
4. 「名前のないタグ」というテキストを置き換えるタグ名を入力します。

タグを追加したら、以下の構成を構成します。値が不明な場合は、オプションのフィールドを空欄のままにしてください。

* **Tealiumアカウント**：（必須）Tealiumのアカウント名。例：`companyXYZ`。
* **Tealiumプロファイル**：（必須）Tealiumのプロファイル名。例：`main`。
* **Tealiumデータソースキー**：（任意）サーバー側のTealium構成にあるデータソースキー。例：`abc123`。
* **データ収集エンドポイント**：（任意）Tealium Collectエンドポイントをファーストパーティのデータ収集エンドポイントで上書きします。例：`https://collect.example.co.uk/example-event-endpoint`。
* **データオブジェクト**：（任意）グローバルな`dataLayer`オブジェクトの代わりに使用するカスタムJavaScript変数。例：`{{myObject}}`。

### トリガー

ページビューのトラッキングには、組み込みの「All Pages」トリガーを使用します。イベントトラッキングを含めるには、すべてのイベントで発火する「All Events」トリガーを使用します。

Google Tag Managerで「All Events」トリガーを構成するには、次の手順を実行します。

1. Google Tag Managerの左側のナビゲーションで、**トリガー**をクリックします。
2. **新規**ボタンをクリックしてトリガーを追加します。
3. 「トリガーの構成」をクリックしてタグタイプを選択します。リストから「カスタム イベント」を検索して選択します。
3. 「正規表現一致を使用」にチェックを入れます。
4. 「イベント名」の正規表現に以下を入力します。
      ```
      ^(?!gtm.load)(?!gtm.dom)(?!gtm.init)(?!gtm.init_consent).*
      ```
5. **保存**をクリックし、カスタムトリガーに新しい名前を付けて、もう一度**保存**をクリックします。

このルールは、無視する必要があるGoogle Tag Manager固有の2つのイベント、`gtm.load `と`gtm.dom`を除くすべてのイベントでトリガーされます。

### データレイヤーエンリッチメント

Tealium Data Layer Enrichmentタグは、Customer Data Platform（CDP）からサーバー側属性を取得し、データレイヤーに挿入します。

Data Layer Enrichmentタグをインストールするには、次の手順を実行します。

1. Google Tag Managerの左側のナビゲーションで、**テンプレート**をクリックします。
2. **タグ テンプレート**画面で、**ギャラリーを検索**をクリックします。
3. 「Tealium Data Enrichment Tag」を検索して選択します。
4. **ワークスペースに追加**をクリックしてテンプレートを追加します。
5. 「コミュニティ テンプレートを追加しますか？」画面で、**追加**をクリックします。

## 検証

Tealium Collectタグがすべてのイベントで発火している場合、ページ上の`dataLayer.push`呼び出しごとにデータ収集イベントがTealiumへ送信されます。

デバッグコンソールの**ネットワーク**タブでは、`https://collect.tealiumiq.com/ACCOUNT/PROFILE/2/i.gif`に対するPOST呼び出しが送信されます。

イベントデータをリアルタイムで確認するには、[ライブイベント](https://docs.tealium.com/about-live-events/)を使用します。