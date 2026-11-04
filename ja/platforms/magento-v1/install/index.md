---
title: インストール
description: この記事では、Magento Connect Extension Marketplace の Tag Management Extension を使用して、Magento® 1 システムに Tealium をインストールする方法について説明します。
url: https://docs.tealium.com/ja/platforms/magento-v1/install/
---

<blockquote>
この手順は、Magento バージョン 1.5～1.14 に対応しています。バージョン 2.9 以降については、[Tealium for Magento 2](https://docs.tealium.com/ja/platforms/magento/install/)を参照してください。
</blockquote>


Magento Connect で Tealium Extension を追加して有効にするには、次の手順を実行します。

1. Magento アカウントを使用して Magento Extension Marketplace にログインします。
2. Marketplace で「Tealium」を検索し、**Tealium Tag Management** Extension をクリックします。
![](https://docs.tealium.com/images/platforms/magento-v1/magento1-1.png)
3. **Install Now** をクリックします。
![](https://docs.tealium.com/images/platforms/magento-v1/magento1-2.png)
4. 規約に同意するため、**Extension license terms** チェックボックスをオンにし、**Get Extension Key** をクリックします。
![](https://docs.tealium.com/images/platforms/magento-v1/magento1-3.png)
5. キーフィールドに **Extension Key** が表示されます。Extension Key をコピーします。
![](https://docs.tealium.com/images/platforms/magento-v1/magento1-4.png)
6. **Magento Admin Panel > System > Magento Connect > Magento Connect Manager** に移動します。
![](https://docs.tealium.com/images/platforms/magento-v1/magento1-5.png)
7. **Install New Extensions** で、Magento Extension Marketplace からコピーした Extension Key を空のフィールドに貼り付け、**Install** をクリックします。
![](https://docs.tealium.com/images/platforms/magento-v1/magento1-6.png)
8. **Extension dependencies** で、**Proceed** をクリックします。
![](https://docs.tealium.com/images/platforms/magento-v1/magento1-7.png)
9. コンソールの下に `Procedure completed. Please check the output frame for useful information and refresh the page to see the changes.` というメッセージが表示されるまで待ち、**Return to Admin** をクリックします。
![](https://docs.tealium.com/images/platforms/magento-v1/magento1-8.png)
10. **Magento Admin Panel > System > Configuration** に移動します。
11. 左側のナビゲーションで、**Tealium** 見出しの下にある **Tag Management** をクリックします。
![](https://docs.tealium.com/images/platforms/magento-v1/magento1-9.png)
12. アカウント情報を使用して構成構成を更新します。
    * **Enable**: `Yes`
    * **Account**: Tealium アカウント
    * **Profile**: Tealium プロファイル（デフォルトは `main`）
    * **Environment**: Tealium のパブリッシュ環境（`dev`、`qa`、または `prod`）
13. **Save Config** をクリックします。
![](https://docs.tealium.com/images/platforms/magento-v1/magento1-10.png)
これで、Magento 実装への Tealium のインストールが完了しました。[インストールを検証](https://docs.tealium.com/ja/platforms/javascript/install/#validate-installation)してください。