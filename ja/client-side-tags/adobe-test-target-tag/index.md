---
title: Adobe Test & Targetタグ構成ガイド
description: Adobe Test & Targetは、マーケターがオンラインコンテンツやオファーを継続的に顧客との関連性が高いものへ改善し、コンバージョンを向上させるために必要な機能を提供します。
url: https://docs.tealium.com/ja/client-side-tags/adobe-test-target-tag/
---
## タグの仕様

**名前**: Test & Target

**ベンダー**: Adobe

**タイプ**: パーソナライゼーション

## 要件

**サービス**: Adobe Marketing Cloudアカウント

**構成**:

* クライアントコード
* タイムアウト
* グローバルmbox名（同期バージョン）

## タグの構成

### ステップ1：タグを追加する

タグマーケットプレイスに移動して、新しいタグを追加します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

Tealiumは、Test & Targetタグの非同期バージョンと同期バージョンの両方をサポートしています。各バージョンは、タグマーケットプレイスで個別のタグとして提供されています。ただし、非同期バージョンの使用を推奨します。ちらつきが懸念される場合は、[ちらつきのないTest & Target](https://docs.tealium.com/flicker-free-test-and-target/)ソリューションを確認してください。このソリューションを使用すると、Test & Targetタグを非同期で読み込み、ちらつきの発生を回避できます。


<blockquote>
非同期タグとともに、[Test & Target Content Modification拡張機能](https://docs.tealium.com/adobe-target-content-modification-extension/)を追加して構成する必要があります。同期バージョンでは、この拡張機能を使用しません。
</blockquote>


### ステップ2：タグを構成する

#### 非同期

ベストプラクティスとして、Test & Targetの非同期バージョンを使用することを推奨します。使用するバージョンによって、構成にはいくつかの違いがあります。非同期バージョンでは、次の項目を構成します。

![](https://docs.tealium.com/images/client-side-tags/basic-configuration-1.png)

1. **タイトル**: （必須）タグインスタンスを識別するためのわかりやすいタイトルを入力します。
1. **クライアントコード**: （必須）Adobeから割り当てられたクライアントIDを入力します。
1. **タイムアウト**: （必須）Test & Targetサーバーが応答していないと判断するまで、Adobeからの応答を待機する時間をミリ秒単位で入力します。サーバーから応答がない場合、タグ呼び出しは停止します。5000ミリ秒以上に構成することを推奨します。
1. **訪問トラッキングID**: （任意）このフィールドを使用すると、Test and TargetとSiteCatalystの間で訪問を追跡できます。この構成は、`mbox.js`ファイル内の`var imsOrgId = 'XXXXXXXXXXXXXXXXXXXXXXXX@AdobeOrg'`として確認できます。

これで、Test & Targetタグの構成は完了です。

#### 同期

Test & Targetの同期バージョンは構成が若干異なり、タグの**詳細構成**を変更する必要があります。このタグを同期的に読み込む場合は、`utag.js`ファイルも同期的に読み込む必要があります。同期`utag.js`コードの取得方法については、[utag.sync.jsの仕組み](https://docs.tealium.com/utag-sync/)を参照してください。

![](https://docs.tealium.com/images/client-side-tags/basic-configuration-2.png)

1. **タイトル**: （必須）タグインスタンスを識別するためのわかりやすいタイトルを入力します。
1. **クライアントコード**: （必須）Adobeから割り当てられたクライアントIDを入力します。
1. **グローバルmbox名**: （必須）グローバルに非表示となるmboxの名前を入力します。通常、Adobeではここに`global`を使用します。タグは`mboxCreate`を自動的に呼び出してmboxを作成します。
1. **訪問トラッキングID**: （任意）このフィールドを使用すると、Test and TargetとSiteCatalystの間で訪問を追跡できます。この構成は、`mbox.js`ファイル内の`var imsOrgId = 'XXXXXXXXXXXXXXXXXXXXXXXX@AdobeOrg'`として確認できます。
1. **詳細構成**: （必須）次の詳細構成を変更します。
  * **待機フラグ**を`No`に構成します。
  * **同期読み込み**を`Yes`に構成します。

![](https://docs.tealium.com/images/client-side-tags/basic-configuration-3.png)

テストコンテンツに関するその他の構成は、Test & Targetのユーザーインターフェイスで行います。

### ステップ3：読み込みルールを適用する

[読み込みルール](https://docs.tealium.com/about-load-rules/)は、このタグのインスタンスをいつ、どこで読み込むかを決定します。デフォルトの読み込みルールは、**すべてのページで読み込む**ルールです。特定のページでこのタグを読み込むには、該当する条件を指定した新しい読み込みルールを作成します。

**ベストプラクティス**: デフォルトの**すべてのページで読み込む**を選択したままにし、このタグをすべてのページで読み込むことを推奨します。非同期バージョンでは、Test & Target拡張機能を使用して、テストを読み込む条件を制御できます。

### ステップ4：マッピングを構成する

[マッピング](https://docs.tealium.com/about-data-mappings/)とは、データレイヤー内のデータソースから、ベンダータグ内の対応する宛先変数へデータを送信するための簡単なプロセスです。

* Test & Targetの非同期バージョンでは、マッピングはTest & Target Content Modification拡張機能の**静的パラメータ**フィールドで処理されます。
* Test & Targetの同期バージョンでは、マッピングはサポートされていません。