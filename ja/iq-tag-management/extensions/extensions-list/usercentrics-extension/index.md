---
title: Usercentrics拡張機能
description: TealiumのUsercentrics拡張機能は、サードパーティのCMPサポートを有効にするために使用されます。この拡張機能は、タグ管理とコンセント管理の間の統合を簡素化し、特定のタグにデータ処理サービスをマッピングすることを可能にします。
url: https://docs.tealium.com/ja/iq-tag-management/extensions/extensions-list/usercentrics-extension/
---
## 動作原理

Tealium iQタグ管理のUsercentrics拡張機能は、CMPポリシーがソースレベルで強制されるように使用され、ユーザーの同意構成に応じてタグのブロックまたは発火を行います。

データ処理サービスのJSONオブジェクトテキストをブラウザのブックマークにインポートするためのシンプルなブックマークレット機能が使用され、これを使用してマッピングテーブルを作成します。

使用するには、拡張機能を追加し、必要な情報を入力してから、マッピングテーブルを使用してタグに同意構成をマッピングします。この方法を使用すると、実装時間が大幅に短縮され、CMPサービスにマッピングされるまでタグの発火を防ぐことで追加の保護層が提供されます。

Usercentricsのデータ処理サービスにマッピングされていないタグが追加された場合のプライバシーリスクの露出を防ぐために、拡張機能がアクティブになるとマッピングされたタグのみが発火します。

## 前提条件

* **Usercentricsの実装に関する知識**  
現在または計画中のUsercentricsの実装についての知識が必要です。コンセント管理プラットフォーム（CMP）のすべてのデータ処理サービスを取得するには、[Usercentrics直接実装ガイド](https://docs.usercentrics.com/#/direct-implementation-guide)の指示に従ってください。
* **最初の実装にはテスト環境を使用する**  
最初の実装にはテスト環境を使用し、拡張機能内でマッピングテーブルを作成するためにCMPに完全にアクセスすることをお勧めします。テスト環境を使用することで、開発環境に拡張機能を適用する前にエンドユーザーデータが処理されることはありません。  
すべてのデータ処理サービスを対応するタグにマッピング完了後、製品環境にリリースすることができ、Tealium iQタグ管理がエンドユーザーのプライバシー構成（同意）の強制を行います。

## 要件

* Tealium Universal Tag (`utag.js`)、バージョン4.48。`utag.js`テンプレートの更新に関する詳細は、ナレッジベースの記事[utag.jsの最新バージョンへの更新のベストプラクティス](https://support.tealiumiq.com/en/support/solutions/articles/36000363470)を参照してください。
* Usercentrics CMPはTealium iQタグ管理の前にロードする必要があります。そのため、以下のいずれかを行う必要があります：
    * Usercentricsスクリプト（タグ）をウェブサイトのHTMLコード内に直接実装します。  
    **- または -**
    * 下記のUsercentricsタグの実装セクションに進み、Tealium iQタグ管理内でタグを実装する手順に従います。

* Tealium iQタグ管理のためのデータ処理サービスをUsercentrics CMP構成で作成します。  
詳細については、Usercentricsのドキュメント、[データ属性の割り当て](https://docs.usercentrics.com/#/direct-implementation-guide?id=assign-a-data-attribute)を参照してください。構成手順を始める前に、データ処理サービスの名前を知っておく必要があります。

## Usercentricsタグの実装

以下の手順を使用して、JavaScript Code拡張機能を使用してTealium iQタグ管理内でUsercentricsタグを実装します：

1. **Tealium iQタグ管理 &gt; 拡張機能 &gt; 拡張機能を追加**に進み、**JavaScript Code**拡張機能を選択してUsercentrics V1またはUsercentrics V2のスクリプトを追加します。
1. **JavaScript Code**拡張機能を追加します。  
    もしJavaScript Code拡張機能を以前に使用したことがなく、使用方法を学ぶ必要がある場合は、JavaScript Code拡張機能を参照してください。

1. 拡張機能の名前を**Usercentricsタグ**とし、スコープを**プリローダー**に構成します。
1. 次のいずれかの例のスクリプトを使用して拡張機能を作成します：  
    * **Usercentrics V1スクリプト**：Usercentrics CMP v1をサポートします。  
        ```js
        (function(a, b, c, d) {
                    b = document;
                    c = &#39;script&#39;;
                    d = b.createElement(c);
                    d.src=&#34;XXXXXXXXXXX&#34;; // Usercentrics CMPバージョン1スクリプトのURL。
                    d.type = &#39;text/java&#39; &#43; c;
                    d.async = true;
                    d.id = &#39;XXXXXXXXX&#39;; // Usercentrics構成ID
                    a = b.getElementsByTagName(c)[0];
                    a.parentNode.insertBefore(d, a);
                }
                )();
        ```
    * **Usercentrics V2スクリプト**：Usercentrics CMP V2ブラウザSDKをサポートします。  
        ```js
        (function(a, b, c, d) {
                    b = document;
                    c = &#39;script&#39;;
                    d = b.createElement(c);
                    d.src=&#34;XXXXXXXXXXX&#34;; // Usercentrics CMPバージョン2スクリプトのURL。
                    d.type = &#39;text/java&#39; &#43; c;
                    d.async = true;
                    d.id = &#39;usercentrics-cmp&#39;;
                    d.setAttribute(&#39;data-settings-id&#39;, &#34;XXXXXXXXXXX&#34;); // Usercentrics構成ID
                    a = b.getElementsByTagName(c)[0];
                    a.parentNode.insertBefore(d, a);
                }
                )();
        ```

1. JavaScript Code拡張機能を環境に保存して公開します。

## TealiumのUsercentrics CMPでデータ処理サービスを作成する

ユーザーの同意構成が強制され、第三者が許可された場合にのみデータを処理できるようにするために、UsercentricsアカウントでTealiumデータ処理サービスを作成する必要があります。

Tealium iQタグ管理のためのデータ処理サービスをUsercentrics CMPアカウントで作成するための以下の手順を使用します：

1. **Usercentrics**アカウントに進みます。
1. **Tealium iQタグ管理**のための最新のデータ処理テンプレートを選択します。
1. テンプレートを**必須**としてマークして、オプトアウトができないようにします。  
Tealium iQタグ管理のサービス名をカスタマイズした場合、CMP拡張機能によって自動的に検出されません。  
このドキュメントの構成セクションで、サービス名入力フィールドを使用してカスタムサービス名を手動で追加します。

## 拡張機能の構成

このセクションの手順では、拡張機能を追加し、ブックマークレットをインストールし、データ処理サービスをコピーし、データ処理サービスをインポートし、タグをデータ処理サービスにマッピングする方法を説明します。

### 拡張機能の追加

Usercentrics拡張機能を追加するための以下の手順を使用します：

1. **iQタグ管理 &gt; 拡張機能 &gt; 拡張機能を追加**に進み、**プライバシー**タブをクリックします。
1. Usercentrics拡張機能のいずれかを選択します：**Usercentrics V1**または**Usercentrics V2**。  
組織で現在使用しているバージョンに対応するバージョンを選択します。
1. **タイトル**フィールドに、この拡張機能に使用する意味のあるタイトルを入力します。  
**スコープ**フィールドは変更できません。
1. **構成ID**（オプショナル）  
**Usercentrics** **構成ID**の下で、**構成ID**フィールドに手動でUsercentricsの`Settings_ID`を追加できます。  
このステップは必要ない場合があります。データ処理サービスをインポートする際にUsercentrics構成IDが拡張機能に自動的に追加されます。

1. **Tealium iQサービス名**の下で、**サービス名**フィールドにUsercentrics内で与えられたTealiumデータ処理サービスの正確な名前を入力します。  
    ![](/images/iq-tag-management/usercentrics-extension-rollback-domain-conditions.png)
1. **サービスマッパー**ブックマークレットをインストールして使用する次のセクションに進みます。
### Service Mapper ブックマークレットのインストール

ブックマークレットをインストールするには、以下の手順に従ってください：

1. **Bookmarklet** ボタンをクリックします。  
**Usercentrics Service Mapper Bookmarklet** ダイアログが表示されます。
1. **Usercentrics Service Mapper** リンクをクリックし、ブックマークレットをブラウザのブックマークバーにドラッグアンドドロップします。  
    ![](/images/iq-tag-management/usercentrics-bookmarklet-modal.png)  
ブックマークレットがブラウザバーに表示されます。
1. **閉じる** をクリックして、Usercentrics Service Mapper Bookmarklet ウィンドウを閉じます。

### マッピングテーブルの作成

データ処理サービスをコピーしてインポートし、マッピングテーブルを作成するには、以下の手順に従ってください：

1. 別のブラウザタブを開き、CMPが実装されている Usercentrics テスト環境に移動し、**Usercentrics Service Mapper** ブックマークレットを起動します。  
データ処理サービスの JSON オブジェクトのテキストが表示されるポップアップウィンドウが表示されます。
1. このウィンドウから全てのテキストをコピーします。
1. **Tag Management** の Usercentrics 構成ダイアログに戻り、**インポート** ボタンをクリックします。  
**インポートサービス** ダイアログが表示されます。
1. 次の例に示すように、コピーした JSON テキストをウィンドウに貼り付けます。  
    ![](/images/iq-tag-management/code-usercentrics-import-sample-pasted.png)
1. **マッピングテーブルを作成** をクリックします。  
あなたの Usercentrics 構成 ID と Tealium iQ サービス名が自動的に入力され、データ処理サービスへのサービスマッピングがマッピングテーブルに表示されます。  
マッピングテーブルは、新しいタグが導入された場合や Usercentrics 構成のデータ処理サービスが変更された場合に、このドキュメントのマッピングテーブル更新セクションに記載されているように更新する必要があります。

### データ処理サービスをタグにマッピング

データ処理サービスをタグにマッピングするには、以下の手順に従ってください：

1. マッピングテーブルの各項目で、**To UID** フィールドをクリックし、事前に用意されたリストから適切なタグ UID を選択します。  
データ処理サービスに複数のタグをマッピングすることができます。  
    ![](/images/iq-tag-management/usercentrics-extensions-service-mappings-dropdown.png)
1. ブックマークレットは自動的に **Tealium Tag Management** と **Usercentrics** のリスト項目をマッピングテーブルに追加します。
1. 同意強制に使用されない **Tealium Tag Management** と **Usercentrics** サービスを削除するためにゴミ箱アイコンを使用します。
1. （オプション）**サービスを追加** をクリックして手動で追加のサービスを追加し、それに応じてマッピングします。  
完了すると、ページの再読み込みなしですぐに同意が強制され、エンドユーザーのプライバシー構成がデータ処理が行われる前に強制されることが保証されます。
1. 変更を保存して公開します。

### マッピングテーブルの更新

新しいタグが導入された場合や Usercentrics 構成内のデータ処理サービスが変更された場合には、マッピングテーブルを更新する必要があります。構成手順で説明されているブックマークレット機能を使用し、プロセスを繰り返して更新します。

インポート機能は、次のように既存のデータ処理サービスを識別します：

* データ処理サービスが既に存在する場合、マッピングには影響しません。
* データ処理サービスが削除された場合、マッピングエントリも削除されます。
* データ処理サービスが新しく導入された場合、マッピングテーブルに新しい行項目が追加され、少なくとも1つの対応するタグをマッピングする必要があります。

## トラブルシューティング

典型的なイベント、ログメッセージ、注意が必要なエラーメッセージを表示するには、コンソールログを有効にします。

コンソールログを有効にするには、以下の手順に従ってください：

1. [JavaScript (Web) デバッグ](/ja/platforms/javascript/debugging/) に移動し、デバッグクッキーを追加する手順に従います。
1. デバッグクッキーが構成された後、`&#34;/SENDING|\*\*\*\*/&#34;` フィルターを使用して関連するエントリのみを表示します。

## FAQ

#### この拡張機能はモバイルインストールで使用できますか？

いいえ。iOSやAndroidなどのモバイルインストールでは、Tealium Tag Management Usercentrics 拡張機能はサポートされていません。
