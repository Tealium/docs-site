---
title: インストール
description: Tealium CollectをGoogle Tag Managerにインストールする方法を学びます。
url: https://docs.tealium.com/ja/platforms/google-tag-manager/install/
---
## 必要条件

* [Tealium Customer Data Hubアカウント]()

## 仕組み

Google Tag ManagerのTealium Collectタグは、カスタムテンプレートで、ページごとに一度TealiumからTealium Collect JavaScriptファイルをロードします。

各タグがトリガーされるイベントごとに、タグは自動的に`dataLayer`オブジェクトをキーと値のペアにフラット化し、データをTealiumのデータ収集エンドポイントに投稿します。ファーストパーティのデータ収集を使用している場合は、カスタムエンドポイントを使用することができます。

以下のGoogle Tag Managerイベントは、フラット化される前のものです：
```
dataLayer.push({
  &#39;ecommerce&#39;: {
    &#39;purchase&#39;: {
      &#39;actionField&#39;: {
        &#39;id&#39;: &#39;T12345&#39;,
...
```

フラット化された後、以下のようなTealiumイベントになります：
```
&#34;tealium_event&#34;: &#34;purchase&#34;
&#34;ecommerce.purchase.actionField.id&#34;: &#34;T12345&#34;
...
```

## インストール

Google Tag Manager経由でTealium Collectタグを追加するには：

1. Google Tag Managerで、左のナビゲーションで**テンプレート**をクリックします。
2. **タグテンプレート**画面で、**ギャラリーを検索**をクリックします。
3. &#34;Tealium Collectタグ&#34;を検索して選択します。
4. **ワークスペースに追加**をクリックしてテンプレートを追加します。
5. &#34;コミュニティテンプレートを追加してもよろしいですか？&#34;画面で、**追加**をクリックします。

### 新しいタグを追加

Tealium Collectタグのインスタンスを追加するには：

1. Google Tag Managerで、左のナビゲーションで**タグ**をクリックします。
2. **新規**ボタンをクリックします。
3. &#34;タグ構成&#34;をクリックしてタグタイプを選択します。リストから&#34;Tealium Collectタグ&#34;を検索して選択します。
4. &#34;Untitled Tag&#34;のテキストを置き換えるタグ名を提供します。

タグを追加した後、以下の構成を行います。値が不明な場合は、オプションのフィールドを空白にしておきます。

* **Tealiumアカウント**（必須）：Tealiumのアカウント名。例えば、`companyXYZ`。  
* **Tealiumプロファイル**（必須）：Tealiumのプロファイル名。例えば、`main`。  
* **Tealiumデータソースキー**（オプション）：サーバーサイドのTealium構成からのデータソースキー。例えば、`abc123`。  
* **データ収集エンドポイント**（オプション）：ファーストパーティのデータ収集エンドポイントでTealium Collectエンドポイントを上書きします。例えば、`https://collect.example.co.uk/example-event-endpoint`。  
* **データオブジェクト**（オプション）：グローバルな`dataLayer`オブジェクトの代わりに使用するカスタムJavaScript変数。例えば、`{{myObject}}`。

### トリガー

ページビュートラッキングには、組み込みの&#34;All Pages&#34;トリガーを使用します。イベントトラッキングを含めるには、すべてのイベントに対して発火する&#34;All Events&#34;トリガーを使用します。

Google Tag Managerで&#34;All Events&#34;トリガーを構成するには：

1. Google Tag Managerで、左のナビゲーションで**トリガー**をクリックします。
2. **新規**ボタンをクリックしてトリガーを追加します。
3. &#34;トリガー構成&#34;をクリックしてタグタイプを選択します。リストから&#34;カスタムイベント&#34;を検索して選択します。
3. &#34;正規表現マッチングを使用する&#34;チェックボックスを選択します。
4. &#34;イベント名&#34;の正規表現（regex）に以下を入力します：    
      ```
      ^(?!gtm.load)(?!gtm.dom)(?!gtm.init)(?!gtm.init_consent).*
      ```
5. **保存**をクリックし、カスタムトリガーに新しい名前を付けて、再度**保存**をクリックします。

このルールは、`gtm.load`と`gtm.dom`（Google Tag Managerに特有の2つのイベントで、無視したいもの）を除くすべてのイベントに対してトリガーします。

### データレイヤーのエンリッチメント

Tealium Data Layer Enrichmentタグは、Tealium AudienceStreamからのサーバーサイドの属性を取得し、それらをデータレイヤーに注入します。

Data Layer Enrichmentタグをインストールするには：

1. Google Tag Managerで、左のナビゲーションで**テンプレート**をクリックします。
2. **タグテンプレート**画面で、**ギャラリーを検索**をクリックします。
3. &#34;Tealium Data Enrichmentタグ&#34;を検索して選択します。
4. **ワークスペースに追加**をクリックしてテンプレートを追加します。
5. &#34;コミュニティテンプレートを追加してもよろしいですか？&#34;画面で、**追加**をクリックします。

## 検証

Tealium Collectタグがすべてのイベントで発火している場合、ページ上のすべての`dataLayer.push`呼び出しはTealiumにデータ収集イベントを送信します。

デバッグコンソールの**ネットワーク**タブでは、POST呼び出しが`https://collect.tealiumiq.com/ACCOUNT/PROFILE/2/i.gif`に送信されます。

[ライブイベント]()を使用して、リアルタイムでイベントデータを確認します。


