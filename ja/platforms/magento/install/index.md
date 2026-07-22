---
title: インストール
description: この記事では、Magento® 2 システムに Tealium iQ タグ管理拡張機能を Magento Marketplace からインストールする方法を示しています。
url: https://docs.tealium.com/ja/platforms/magento/install/
---
## 必要条件

以下の項目が必要です：

* アクティブな Tealium iQ タグ管理アカウント
* あなたの Tealium アカウント ID
* あなたの Tealium プロファイル名
* 使用する Tealium 環境（prod、qa、dev、またはカスタム）

## 動作原理

Magento 用 Tealium 拡張機能は、さまざまなページタイプにわたってユニバーサルデータオブジェクト（UDOs）を実装および拡張するための最小限のボイラープレートコードの堅牢な実装を提供します。Magento の依存性注入とレイアウトシステムを活用することで、UDOs の作成と拡張のプロセスを簡素化します。

拡張機能には、新しい UDO を作成する際にボイラープレートコードをスキャフォールドするシンプルなスクリプトが含まれています。それは、拡張する可能性のある任意の UDO を指定し、新しい UDO が表示されるサイトのページを指定することができます。完了すると、特定のユースケースに対するデータ固有のロジックを記入する必要があるスキャフォールドされたテンプレートが作成されます。

Magento の詳細については、[Magento Documentation](http://devdocs.magento.com/)を参照してください。

## インストール


<blockquote>
以下の手順は Ubuntu サーバー環境のコマンドを使用しています。他のサーバー環境の場合は、コマンドを適宜調整してください。
</blockquote>


Magento システムに Tealium をインストールするには：

1. **メンテナンスモードを有効にする**：拡張機能をインストールする前に、ユーザーの問題を避けるためにメンテナンスモードを有効にします。メンテナンスモードを有効にするには、次のコマンドを実行します：
   ```
   php bin/magento maintenance:enable
   ```
1. **Tealium フォルダをコピーする**：[GitHub](https://github.com/Tealium/integration-magento2/tree/DependencyUpdates)から `app/code/Tealium/Tags` 内の Magento フォルダに Tealium フォルダをコピーします。`app/code/Tealium/Tags` が存在しない場合は、作成します。
1. **変更を更新する**：変更を更新するために、次のコマンドを実行します：
   ```
   php bin/magento setup:upgrade
   php bin/magento setup:di:compile
   php bin/magento setup:static-content:deploy -f
   php bin/magento cache:flush
   ```
1. **メンテナンスモードを無効にする**：インストールが完了したら、ユーザーがサイトにアクセスできるようにメンテナンスモードを無効にします。メンテナンスモードを無効にするには、次のコマンドを実行します：
   ```
   php bin/magento maintenance:disable
   ```

## 構成

Magento 2 を構成するには、次の手順を実行します：

1. 管理パネルで、**Stores > Configuration > Tealium > Tag Management** に移動します。
1. 拡張機能を有効にし、Tealium iQ アカウント、プロファイル、および環境を入力します。
1. ファーストパーティドメインを使用している場合は、**First Party Domain** フィールドにクライアントドメインを入力します。
1. プレーンテキストの顧客メールアドレスを許可する場合は、**Allow plain text customer email** ドロップダウンリストの下で **No** を選択します。それ以外の場合、メールアドレスは SHA-256 ハッシュを使用して暗号化されます。

## テスト

Tealium と Magento の構成が正しく機能していることを確認するために、次のテストを使用します：

* [Code Sniffer](https://developer.adobe.com/commerce/marketplace/guides/sellers/code-sniffer/)
* [Installation and Varnish Tests](https://developer.adobe.com/commerce/marketplace/guides/sellers/installation-and-varnish-tests/)
* [MFTF Commerce-supplied Tests](https://developer.adobe.com/commerce/marketplace/guides/sellers/mftf-magento/)
