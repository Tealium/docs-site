---
title: Tealium Tools ブラウザ拡張機能
description: Tealium Tools 拡張機能は、Tealium のデプロイメントを管理するための標準ツールセットを提供し、開発者コミュニティからカスタムツールを作成および共有するための強力なフレームワークを提供します。
url: https://docs.tealium.com/ja/iq-tag-management/tealium-tools/browser-extension/
---
Tealium Tools 拡張機能は、以下のブラウザで利用可能です：

* Google Chrome
* Microsoft Edge

## インストール

### Chrome

Google Chrome に Tealium Tools 拡張機能をインストールするには：

1. 新しい Chrome ウィンドウで、[Tealium Tools Chrome 拡張機能](https://chrome.google.com/webstore/detail/tealium-tools/gidnphnamcemailggkemcgclnjeeokaa)にアクセスします。
1. **+ Chrome に追加**をクリックします。
1. **拡張機能を追加**をクリックして確認します。  
ボタンが**Chrome に追加済み**と表示され、Chrome ツールバーの右上に Tealium アイコンが表示されることを確認します。
1. Chrome ウィンドウの右上にある Tealium アイコンをクリックして Tealium Tools を開き、使用するツールを選択します。

### Edge

Microsoft Edge に Tealium Tools アドオンをインストールするには：

1. 新しい Edge ウィンドウで、[Tealium Tools Edge アドオン](https://microsoftedge.microsoft.com/addons/detail/tealium-tools/idhdcghfaooedcikdpjmbkfknlckhpfo)にアクセスします。
1. **取得**をクリックします。
1. **拡張機能を追加**をクリックして確認します。  
ボタンの下のテキストが**ブラウザにアドオンが既にインストールされています**と表示されることを確認します。
1. **拡張機能**アイコンをクリックします。
1. **Tealium Tools**の横にある表示ボタンをクリックします。Tealium アイコンが Edge ツールバーの右上に表示されます。
1. Edge ウィンドウの右上にある Tealium アイコンをクリックして Tealium Tools を開き、使用するツールを選択します。

## インターフェース

Tealium Tools ウィンドウは、2つのメインタブに整理されており、**ユーザープロファイルアイコン**の下に追加のオプションがあります。

### メインタブ

* **ホーム**  
公式の Tealium 組み込みツールが含まれています。  
    ![](https://docs.tealium.com/images/iq-tag-management/tealium-tools-browser-extension.png)
* **ツールカタログ**  
Tealium、パートナー、時にはクライアントからの貢献者によって作成された公式の Tealium 組み込みツールとコミュニティツールのカタログです。Tealium は公式にコミュニティツールをサポートしていないことに注意してください。

### ユーザープロファイルオプション

ユーザープロファイルアイコンをクリックして、次の追加オプションにアクセスします：

* **ログイン**  
  ログイン資格情報を管理し、シングルサインオン（SSO）を構成します。詳細については、[SSO の使用](#using-sso)を参照してください。
* **構成**  
  ツールの動作をカスタマイズし、ツールの環境スイッチャーなどのドメインや環境の構成を行います。詳細については、[カスタムドメインまたはパスオーバーライドを使用した環境スイッチャーの使用](https://docs.tealium.com/environment-switcher/#using-the-environment-switcher-with-custom-domains-or-path-overrides)を参照してください。
* **情報**  
  バージョンの詳細、ビルド情報を表示し、コミュニティタグがコミュニティツールにラベル付けされていることを学びます。
* **フィードバック**  
  拡張機能から直接問題を報告したり、提案を送信したりします。

## SSO の使用

シングルサインオン（SSO）を構成して使用するには：

1. **Tealium Tools** 拡張機能を開きます。
1. 右上隅にあるプロファイルアイコンをクリックします。
1. **構成**をクリックします。
1. **デフォルトとして SSO を使用する**にチェックを入れます。
1. **構成を更新**をクリックしてツールをリロードします。

**ログイン**構成に戻り、**SSO ログイン**をクリックしてシングルサインオンでログインします。

![](https://docs.tealium.com/images/iq-tag-management/tealium-tools-sso-login.png)

## 公式 Tealium ツール

以下は、拡張機能に組み込まれている Tealium ツールのリストです：

* [**Tealium iQ**](https://my.tealiumiq.com)  
iQ タグ管理インターフェースへのブックマークリンク。
* [**Web Companion**](https://docs.tealium.com/web-companion/)  
タグ構成を監査し、サイト上のデータを検査し、新しい構成を迅速かつ簡単に作成およびテストするためのブラウザツール。
* [**Tealium University**](https://university.tealium.com/)  
自己学習コースを含む Tealium のオンライン学習ポータルへのブックマークリンク、および対面/講師主導のトレーニングへのアクセス。
* [**AudienceStream Trace**](https://docs.tealium.com/about-trace/)  
Universal Data Hub の構成をテストするために必要なツールを提供します。Trace を使用すると、定義されたワークフローのすべての詳細を観察し、属性が正しく更新され、ルールが適切に構成され、予想通りにアクションが発火することを確認できます。Trace はリアルタイムで動作するため、何がうまくいっているか、何を調整する必要があるかをすぐに知ることができます。
* [**Optimizely Helper**](https://docs.tealium.com/optimizely-helper/)  
Tealium AudienceStream を使用して、マーケターはオーディエンスを発見し、訪問プロファイルを豊かにし、デジタルタッチポイント間の顧客インタラクションを繋ぎ合わせることができます。AudienceStream と Optimizely の両方を使用することで、ユーザーは AudienceStream で作成されたオーディエンスを活用し、Optimizely でターゲットを絞った実験を構築することができます。
* [**Environment Switcher**](https://docs.tealium.com/environment-switcher/)  
環境スイッチャーは、ページにロードされる Tealium ファイル (utag.js, utag.sync.js) を環境 (Dev, QA, Prod, Custom) やアカウント、プロファイルを指定して変更する強力なテストツールです。
* [**Tealium Docs**](https://docs.tealium.com/ja/)
Tealium の公式ドキュメントへのブックマークリンク。これは実装者や開発者にとっての出発点です。
* [**Knowledge Base**](https://support.tealiumiq.com/en/support/solutions)
Tealium のナレッジベースへのブックマークリンク。ここで検索してサポートを見つけることができます。

## コミュニティツール

* **Account Stats Report**
クライアントサイド (iQ) とサーバーサイド (CDH) の使用統計を CSV ファイルにエクスポートします。  
* **Bulk Edit Assets (Client-Side)**
複数の変数、ロードルール、タグ、または拡張機能を一度に管理し、それらのアクティブ状態を切り替えたり、一括で削除したりします。  
* **Connector Action Export**
コネクタアクションをエクスポートし、名前、ID、および属性マッピング（ソースと宛先）を CSV ファイルに含めます。  
* **Connector Logs Download**
成功したアクションとエラーの詳細なログを表示し、エラーレポートをダウンロードするオプションがあります。  
* **Cookie Helper**
現在のページで直接クッキー値を取得または構成します。  
* **CSS Selector Tool**
ページ上の単一の要素に一意に一致する最短の jQuery セレクタを特定します。  
* **File Import Logs Download**
File Import および Omnichannel プロセスのログをダウンロードします。  
* **Profile Copy/Paste (Client-Side)**
あるアカウントから別のアカウントに TiQ プロファイル全体をコピーします。注意：個々の要素は選択できません。  
* **Profile Exporter**
プロファイルデータ、データレイヤー、タグ、ルールなどを CSV ファイルにエクスポートします。  
* **Tag Mappings Export (Client-Side)**
タグのデータマッピングをエクスポートし、ロードルールで使用される変数やマッピングを含みます。  
* **UDO Inspector**
Universal Data Object (UDO) の技術的なビューを取得します。

## アンインストール

### Chrome

Google Chrome ブラウザ用の Tealium Tools 拡張機能を削除する手順は次のとおりです：

1. Chrome ブラウザウィンドウで、[Tealium Tools Chrome 拡張機能](https://chrome.google.com/webstore/detail/tealium-tools/gidnphnamcemailggkemcgclnjeeokaa)にアクセスします。
1. **Chrome から削除**をクリックします。確認ダイアログが表示されます。
1. 再度**削除**をクリックして確認します。

### Edge

Microsoft Edge ブラウザ用の Tealium Tools アドオンを削除する手順は次のとおりです：

1. Edge ブラウザウィンドウで、[Tealium Tools Edge アドオン](https://microsoftedge.microsoft.com/addons/detail/tealium-tools/idhdcghfaooedcikdpjmbkfknlckhpfo)にアクセスします。  
1. **削除**をクリックします。確認ダイアログが表示されます。
1. 再度**削除**をクリックして確認します。


## 追加情報

* **[カスタム Tealium ツールのリスト](https://support.tealiumiq.com/en/support/solutions/articles/36000363424-list-of-custom-tealium-tools)**  
利用可能なカスタムツールに関する詳細情報。