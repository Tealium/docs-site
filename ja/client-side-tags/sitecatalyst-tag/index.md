---
title: SiteCatalyst タグ構成ガイド
description: SiteCatalystは、訪問があなたのサイトとどのようにやり取りするかを追跡するWebアナリティクスを提供するAdobeのサービスとしてのソフトウェアアプリケーションです。
url: https://docs.tealium.com/ja/client-side-tags/sitecatalyst-tag/
---
## タグの仕様と要件

### 仕様

**名前**: SiteCatalyst

**ベンダー**: Adobe

**タイプ**: アナリティクス

### 必須

**サービス**: SiteCatalyst アカウント

**構成**:

* S-Code バージョン
* レポートスイート
* サーバー
* セキュアサーバー
* ネームスペース
* 内部リンクフィルター

## Tealium iQでのタグ構成

### 1. タグを追加

Tealium iQのタグマーケットプレイスは多種多様なタグを提供しています。詳細は[こちら](https://docs.tealium.com/about-tag-marketplace/)をご覧ください。

### 2. タグを構成

こちらはSiteCatalystタグの構成リストです。構成値はSiteCatalystから提供された`s_code`ファイルで見つけることができます。

![](https://docs.tealium.com/images/client-side-tags/no-title-1081i487822e9a007e208.png)

![](https://docs.tealium.com/images/client-side-tags/no-title-1080if5f98fdd321f2089.png)

1. **タイトル**: (必須) タグを識別するための説明的なタイトルを入力してください。
1. **S-Code バージョン**: (必須) 使用するSiteCatalystのバージョンを選択してください。H20からH27までがサポートされています。
1. **レポートスイート**: (必須) SiteCatalystレポートスイートの名前を入力してください。この値は`s_code.js`ファイルの`s.account`として見つけることができます。
1. **サーバー**: (必須) データ収集サーバー情報を入力してください。この値は`s_code.js`ファイルの`s.trackingServer`として見つけることができます。
1. **セキュアサーバー**: (必須) セキュア(`https`)データ収集サーバー情報を入力してください。この値は`s_code.js`ファイルの`s.trackingServerSecure`として見つけることができます。
1. **ネームスペース**: (必須) この値は`s_code.js`ファイルの`s.namespace`として見つけることができます。
1. **自動リンク追跡**: (オプション) デフォルト選択は`Yes`で、推奨される選択です。これを`No`に構成する場合、Tealiumの[リンク追跡拡張機能](https://docs.tealium.com/jquery-onhandler-extension/)で全ての自動リンク追跡を複製する必要があります。
カスタム追跡のために`Yes`を選択しても、Tealiumのリンク追跡拡張機能を使用することができます。

1. **ダウンロードタイプ**: (オプション) このフィールドには、ダウンロードされた際にダウンロードリンクとして追跡したいファイル拡張子のタイプをリストアップしてください。例えば、`zip`,`exe`,`wav`,`mp3`,`mov`,`mpg`,`avi`,`wmv`,`pdf`,`doc`,`docx`,`xls`,`xlsx`,`ppt`,`pptx`などです。
1. **内部リンクフィルター**: (オプション) ここに値を入力しないと、すべてのリンククリックがSiteCatalystレポートで退出リンクとして報告されます。JavaScriptアクティビティをトリガーするリンククリックを適切に追跡するためには、フィールドに`javascript`を含める必要があります。この値は`s_code.js`ファイルの`s.linkInternalFilters`として見つけることができます。
1. **通貨コード**: (オプション) 収益データに使用する通貨の3文字の通貨コードを入力してください。デフォルト値は`USD`です。これはSiteCatalystがレポートスイートで収益データを理解するデフォルトの通貨です。サイトで別の通貨で取引が行われた場合、SiteCatalystは通貨変換を行うことができます。この値は`s_code.js`ファイルの`s.currencyCode`として見つけることができます。
1. **ダイナミックアカウントの使用**: (オプション) ドメインに基づいて異なるレポートスイートにデータを送信したい場合は`Yes`に構成してください。
1. **ダイナミックアカウントリスト**: (オプション) レポートスイートとそれに対応するドメインのリストを入力して、ドメインに基づいてレポートスイートを動的に構成します。例えば: `testreportsuite=testing.example.com,qa.example.com;prodreportsuite=www.example.com`
1. **S-オブジェクト名**: (必須) 完全に別の実装を行う予定がない限り、デフォルトの`s`に構成してください。
1. **クリア変数**: (オプション) 各トラッキングリクエスト後にグローバル`s`オブジェクトに構成されたprops、eVars、およびイベントをクリアするには、これを`Yes`に構成してください。
1. **パートナー**: (オプション) ここにパートナーIDを入力してください。これはAdobe AudienceManagerを使用する場合にのみ必要ですので、Adobe AudienceManagerを使用していない場合は空白のままにしてください。パートナーIDの値は`DIL.create`コールで見つけることができます。

**ヒント**: このタグができるだけ早く読み込まれるように、タグタブのリストの上部にこのタグを配置してください。タグの読み込みが早ければ早いほど、訪問の活動を早くキャプチャすることができます。

### 3. 読み込みルールを適用

[読み込みルール](https://docs.tealium.com/about-load-rules/)は、このタグのインスタンスをいつ、どこで読み込むかを決定します。**すべてのページに表示**ルールがデフォルトの読み込みルールです。特定のページでこのタグを読み込むには、関連する条件を持つ新しい読み込みルールを作成してください。

**注意**: SiteCatalystはアナリティクスタグなので、サイト全体で読み込むことをお勧めします。そのため、デフォルトの**すべてのページに読み込む**選択をそのままにすることをお勧めします。

### 4. マッピングを構成

[マッピング](https://docs.tealium.com/ja/iq-tag-management/data-mappings/manage/)は、データレイヤーのデータソースからベンダータグの対応する宛先変数にデータを送信するプロセスです。

製品文字列を適切にフォーマットし、収益データをSiteCatalystレポートスイートに送信するには、Tealium iQプロファイルに[E-Commerce Extension](https://docs.tealium.com/e-commerce-extension/)を追加して構成する必要があります。


<blockquote>
最新のテンプレート更新では、linkTrackVarsとlinkTrackEventsが自動的に構成されます。最新のものにテンプレートを更新する必要があるかもしれません。
</blockquote>


### 標準マッピング

* **pageName**
* **channel**
* **server**
* **hier1からhier3**
* **VisitorID**
* **s\_account**: この宛先にマッピングして、アカウント構成を動的に構成します。

### イベント

マッピングを使用して次のイベントをトリガーできます:

* **prodView**
* **scOpen**
* **scAdd**
* **scRemove**
* **scView**
* **scCheckout**
* **purchase**
* **event1からevent100**

SiteCatalystでのイベント追跡についての詳細は、[こちら](https://docs.tealium.com/sitecatalyst-firing-multiple-events-and-event-serialization/)をクリックしてください。

#### 製品レベルのイベント

ここでのマッピングはこれらのイベントを製品文字列に追加します。

* `PRODUCTS_event1`から`PRODUCTS_event100`

#### Props

データソースをこれらの宛先にマッピングして、それらをSiteCatalystのpropsとして送信します。

* `prop1`から`prop75`

#### eVars

データソースをこれらの宛先にマッピングして、それらをSiteCatalystのeVarsとして送信します。

* `eVar1`から`eVar75`

#### マーチャンダイジングeVars

データソースをこれらの宛先にマッピングして、それらをSiteCatalystのマーチャンダイジングeVarsとして送信します。

* `PRODUCTS_eVar1`から`PRODUCTS_eVAr75`

#### コマース

データソースをこれらの宛先にマッピングして、コマースデータをSiteCatalystに送信します。このデータの多くはE-Commerce Extensionを通じて自動的に送信されます。

* **purchaseID**
* **transactionID**
* **state**
* **zip**
* **製品ID (`PRDOCUTS_id`) \{Array\}**
* **製品カテゴリ (`PRODUCTS_category`) \{Array\}**
* **製品数量 (`PRODUCTS_quantity`) \{Array\}**
* **製品価格 (`PRODUCTS_price`) \{Array\}**

#### その他

以下の宛先にデータソースをマッピングして、リストデータとdoneActionパラメータを送信します。

* リンク追跡 - doneActionパラメータ (H25のみ)
* list1からlist3


## ベンダー文書

* [一般的なウェブサイト](http://www.adobe.com/products/sitecatalyst.html)
* [サポートサイト](http://helpx.adobe.com/sitecatalyst.html)

