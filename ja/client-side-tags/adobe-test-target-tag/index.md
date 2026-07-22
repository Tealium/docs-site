---
title: Adobe Test & Target タグ構成ガイド
description: Adobe Test & Targetは、マーケターがオンラインコンテンツとオファーを顧客にとってより関連性の高いものにし続けるために必要な機能を提供し、より高いコンバージョンを実現します。
url: https://docs.tealium.com/ja/client-side-tags/adobe-test-target-tag/
---
## タグ仕様

**名前**: Test & Target

**ベンダー**: Adobe

**タイプ**: パーソナライゼーション

## 要件

**サービス**: Adobe Marketing Cloud アカウント

**構成**:

* クライアントコード
* タイムアウト
* グローバル mbox 名（同期バージョン）

## Tealium iQ タグ管理でのタグ構成

### ステップ 1. タグを追加する

Tealium iQの**タグマーケットプレイス**では、さまざまなタグを提供しています。プロファイルにタグを追加する方法については、[こちら](https://docs.tealium.com/manage-templates/)をクリックしてください。

Tealiumは、Test & Target タグの非同期バージョンと同期バージョンの両方をサポートしています。各バージョンはタグマーケットプレイスで別々のタグとして存在しますが、非同期バージョンの使用を推奨します。フリッカーに関する懸念がある場合は、[フリッカーフリー Test & Target](https://docs.tealium.com/flicker-free-test-and-target/)ソリューションをチェックしてください。これにより、Test & Target タグを非同期でロードし、フリッカーの発生を避けることができます。


<blockquote>
非同期タグと一緒に[Test & Target コンテンツ変更拡張機能](https://docs.tealium.com/adobe-target-content-modification-extension/)を追加して構成する必要があります。同期バージョンでは拡張機能は使用されません。
</blockquote>


### ステップ 2. タグを構成する

#### 非同期

ベストプラクティスとして、Test & Targetの非同期バージョンの使用を推奨します。使用するバージョンによって構成がいくつか異なります。非同期バージョンの場合、以下の構成を行います：

![](https://docs.tealium.com/images/client-side-tags/basic-configuration-1.png)

1. **タイトル** (必須): タグインスタンスを識別するための説明的なタイトルを入力します。
1. **クライアントコード** (必須): Adobeによって割り当てられたクライアントIDを入力します。
1. **タイムアウト** (必須): タグがAdobeからの応答を待つ時間（ミリ秒単位）を入力します。サーバーからの応答がない場合、タグの呼び出しは中止されます。5000ミリ秒以上を構成することを推奨します。
1. **訪問追跡ID** (オプション): このフィールドを使用して、Test and TargetとSiteCatalyst間で訪問を追跡できます。この構成は `mbox.js` ファイルの `var imsOrgId = 'XXXXXXXXXXXXXXXXXXXXXXXX@AdobeOrg'` として見つけることができます。

Test & Target タグの構成が完了しました。

#### 同期

Test & Targetの同期バージョンは、構成にわずかな違いがあり、タグの**詳細構成**を変更する必要があります。このタグを同期的にロードする予定の場合、`utag.js` ファイルも同期的にロードする必要があります。同期的な `utag.js` コードの取得方法については、[How utag.sync.js works](https://docs.tealium.com/utag-sync/)を参照してください。

![](https://docs.tealium.com/images/client-side-tags/basic-configuration-2.png)

1. **タイトル** (必須): タグインスタンスを識別するための説明的なタイトルを入力します。
1. **クライアントコード** (必須): Adobeによって割り当てられたクライアントIDを入力します。
1. **グローバル mbox 名** (必須): グローバルに隠されたmboxの名前を入力します。Adobeは通常ここで `global` を使用します。タグは自動的に `mboxCreate` を呼び出してmboxを作成します。
1. **訪問追跡ID** (オプション): このフィールドを使用して、Test and TargetとSiteCatalyst間で訪問を追跡できます。この構成は `mbox.js` ファイルの `var imsOrgId = 'XXXXXXXXXXXXXXXXXXXXXXXX@AdobeOrg'` として見つけることができます。
1. **詳細構成** (必須): 次の詳細構成を変更します：
  * **待機フラグ** を `No` に構成します。
  * **同期ロード** を `Yes` に構成します。
![](https://docs.tealium.com/images/client-side-tags/basic-configuration-3.png)

テストコンテンツのさらなる構成は、Test & Targetのユーザーインターフェースを通じて行われます。

### ステップ 3. ロードルールを適用する

[ロードルール](https://docs.tealium.com/about-load-rules/)は、このタグのインスタンスをいつ、どこでロードするかを決定します。**すべてのページでロード**ルールがデフォルトのロードルールです。特定のページでこのタグをロードする場合は、関連する条件を持つ新しいロードルールを作成します。

**ベストプラクティス**: 非同期バージョンの場合、デフォルトの**すべてのページでロード**を選択したままにして、すべてのページでこのタグをロードすることをお勧めします。テストの条件を制御するには、Test & Target 拡張機能を使用します。

### ステップ 4. マッピングを構成する

[マッピング](https://docs.tealium.com/about-data-mappings/)は、データレイヤー内のデータソースからベンダータグの対応する宛先変数にデータを送信するシンプルなプロセスです。

* Test & Targetの非同期バージョンの場合、マッピングは**静的パラメータ**フィールドのTest & Target コンテンツ変更拡張機能を通じて処理されます。
* Test & Targetの同期バージョンではマッピングはサポートされていません。


