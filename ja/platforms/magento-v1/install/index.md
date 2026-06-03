---
title: インストール
description: この記事では、Magento Connect Extension MarketplaceからTealium iQタグ管理拡張機能を使用して、Magento® 1システムにTealiumをインストールする方法を示しています。
url: https://docs.tealium.com/ja/platforms/magento-v1/install/
---
 この手順はMagentoバージョン1.5から1.14に対応しています。バージョン2.9以降の場合は、[Tealium for Magento 2](/ja/platforms/magento/install/)を参照してください。 

Magento ConnectでTealium拡張機能を追加して有効にするには：

1. MagentoアカウントでMagento拡張機能マーケットプレイスにログインします。
2. マーケットプレイスで「Tealium」と検索し、**Tealiumタグ管理**拡張機能をクリックします。
![](/images/platforms/magento-v1/magento1-1.png)
3. **今すぐインストール**をクリックします。
![](/images/platforms/magento-v1/magento1-2.png)
4. **拡張機能ライセンス条項**のチェックボックスを選択して条項に同意し、**拡張キーを取得**をクリックします。
![](/images/platforms/magento-v1/magento1-3.png)
5. **拡張キー**がキーフィールドに表示されます。拡張キーをコピーします。
![](/images/platforms/magento-v1/magento1-4.png)
6. **Magento管理パネル &gt; システム &gt; Magento Connect &gt; Magento Connect Manager**に移動します。
![](/images/platforms/magento-v1/magento1-5.png)
7. **新しい拡張機能をインストール**の下で、Magento拡張機能マーケットプレイスからコピーした拡張キーを空のフィールドに貼り付け、「インストール」をクリックします。
![](/images/platforms/magento-v1/magento1-6.png)
8. **拡張機能の依存関係**の下で、「進行」をクリックします。
![](/images/platforms/magento-v1/magento1-7.png)
9. コンソールの下に「手続きが完了しました。有用な情報が出力フレームに表示されるのを確認し、ページを更新して変更を確認してください。」というメッセージが表示されるのを待ち、**管理者に戻る**をクリックします。
![](/images/platforms/magento-v1/magento1-8.png)
10. **Magento管理パネル &gt; システム &gt; 構成**に移動します。
11. 左側のナビゲーションで、**Tealium**の見出しの下で**タグ管理**をクリックします。
![](/images/platforms/magento-v1/magento1-9.png)
12. アカウント情報で構成を更新します：
    * **有効**: `Yes`
    * **アカウント**: あなたのTealiumアカウント
    * **プロファイル**: あなたのTealiumプロファイル（デフォルトは`main`）
    * **環境**: あなたのTealium公開環境（`dev`、`qa`、または`prod`）
13. **構成を保存**をクリックします。
![](/images/platforms/magento-v1/magento1-10.png)
おめでとうございます！これで、Magento実装にTealiumがインストールされました。[インストールを検証する](/ja/platforms/javascript/install/#validate-installation)ことを忘れないでください。