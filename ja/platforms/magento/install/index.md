---
title: インストール
description: この記事では、Magento Marketplace のタグ管理拡張機能を使用して、Magento® 2 システムに Tealium をインストールする方法について説明します。
url: https://docs.tealium.com/ja/platforms/magento/install/
---
## 要件

以下の項目が必要です。

* 有効なタグ管理アカウント
* Tealium アカウント ID
* Tealium プロファイル名
* 使用する Tealium 環境（prod、qa、dev、またはカスタム）

## 仕組み

Tealium for Magento 拡張機能は、さまざまなページタイプにわたってユニバーサルデータオブジェクト（UDO）を実装および拡張するための、最小限のボイラープレートコードによる堅牢な実装を提供します。このモジュールでは、Magento で規定されている依存性注入およびレイアウトシステムを活用することで、UDO の作成と拡張のプロセスを簡素化します。

この拡張機能には、新しい UDO の作成時にボイラープレートコードのひな形を生成するシンプルなスクリプトが含まれています。新しい UDO が拡張する既存の UDO と、新しい UDO を表示するサイトのページを指定できます。完了すると、特定のユースケースに応じたデータ固有のロジックを追加するためのひな形テンプレートが作成されます。

Magento の詳細については、[Magento ドキュメント](http://devdocs.magento.com/)を参照してください。

## インストール


<blockquote>
以下の手順では、Ubuntu サーバー環境用のコマンドを使用します。その他のサーバー環境では、必要に応じてコマンドを調整してください。
</blockquote>


Magento システムに Tealium をインストールするには、次の手順を実行します。

1. **メンテナンスモードを有効にする**：ユーザーへの影響を避けるため、拡張機能をインストールする前にメンテナンスモードを有効にします。メンテナンスモードを有効にするには、次のコマンドを実行します。
   ```
   php bin/magento maintenance:enable
   ```
1. **Tealium フォルダーをコピーする**：[GitHub](https://github.com/Tealium/integration-magento2/tree/DependencyUpdates) から Tealium フォルダーを、Magento フォルダー内の `app/code/Tealium/Tags` にコピーします。`app/code/Tealium/Tags` が存在しない場合は作成してください。
1. **変更を反映する**：変更を反映するため、次のコマンドを実行します。
   ```
   php bin/magento setup:upgrade
   php bin/magento setup:di:compile
   php bin/magento setup:static-content:deploy -f
   php bin/magento cache:flush
   ```
1. **メンテナンスモードを無効にする**：インストールが完了したら、ユーザーがサイトにアクセスできるようにメンテナンスモードを無効にします。メンテナンスモードを無効にするには、次のコマンドを実行します。
   ```
   php bin/magento maintenance:disable
   ```

## 構成

Magento 2 を構成するには、次の手順を実行します。

1. 管理パネルで、**Stores > Configuration > Tealium > Tag Management** に移動します。
1. 拡張機能を有効にし、タグ管理のアカウント、プロファイル、および環境を入力します。
1. ファーストパーティドメインを使用している場合は、**First Party Domain** フィールドにクライアントドメインを入力します。
1. 顧客のメールアドレスをプレーンテキストで使用できるようにするには、**Allow plain text customer email** ドロップダウンリストで **No** を選択します。それ以外の場合、メールアドレスは SHA-256 ハッシュを使用して暗号化されます。

## テスト

Tealium と Magento の構成が連携して正常に動作していることを確認するには、次のテストを使用します。

* [Code Sniffer](https://developer.adobe.com/commerce/marketplace/guides/sellers/code-sniffer/)
* [インストールおよび Varnish テスト](https://developer.adobe.com/commerce/marketplace/guides/sellers/installation-and-varnish-tests/)
* [Commerce 提供の MFTF テスト](https://developer.adobe.com/commerce/marketplace/guides/sellers/mftf-magento/)