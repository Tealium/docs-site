---
title: IBM WebSphere Commerce 統合ガイド
description: IBM Websphere CommerceのTealium拡張機能は、IBM Websphereソリューション内でTealium iQタグ管理を統合するのに役立つように設計されています。この拡張機能を使用して、Tealiumのユニバーサルデータオブジェクト（UDO）をサイトのデータレイヤーに追加できます。
url: https://docs.tealium.com/ja/partners-and-industries/tech-partners/ibm-websphere-commerce-integration-guide/
---
このドキュメントは、IBM Websphereベースのeコマースサイト内でTealium iQタグ管理を統合する必要がある開発者向けです。IBM Websphere Commerce製品のコアおよびそのeコマース機能に精通していることが前提です。

## 互換性に関する注意

IBMはこのバージョンのTealium拡張機能を認定し、Tealiumを統合パートナーとして追加しました。B2B E-Commerce Engineのサポートはまだテストされていません。

## 統合

### Websphere拡張機能のインストール

Tealium拡張機能は、TGZ形式のパッケージファイルとして配布されます：[tealium-websphere-commerce.tgz](https://docs.tealium.com/images/tech-partners/tealium-websphere-commerce.tgz)。

拡張機能をインストールするには、以下の詳細な場所に圧縮ファイルの内容を解凍します。以下の指示では、`AuroraStorefrontAssetStore`プロジェクトとストアID`10152`を使用しています。これらの値を自分のものに置き換えてください。

Tealium拡張機能をインストールするには：

1. `TealiumUDO.jsp`ファイルと関連する`.jspf`ファイルを`/Stores/WebContent/AuroraStorefrontAssetStore/Tealium`ディレクトリに配置します。
2. `tealium_udo_helper_1_2_0a.jar`ファイル（またはそれ以降のバージョン）を`/Stores/WebContent/WEB-INF/lib/`ディレクトリに配置します。![](https://docs.tealium.com/images/tech-partners/ibmwebsphere1.png)
3. 拡張機能をアクティブにするには、以下のエントリをデータベースに挿入し、Websphere Commerceウェブサーバーを再起動します：
```
  insert into storeconf (storeent_id, name, value, optcounter) values (10152, 'wc.pgl.jspInclude_Tealium_TealiumUDO', '/AuroraStorefrontAssetStore/Tealium/TealiumUDO.jsp', 0);
  insert into storeconf (storeent_id, name, value, optcounter) values (10152, 'wc.tealium.account', 'myaccount', 0);
  insert into storeconf (storeent_id, name, value, optcounter) values (10152, 'wc.tealium.profile', 'myprofile', 0);
  insert into storeconf (storeent_id, name, value, optcounter) values (10152, 'wc.tealium.environment', 'prod', 0);
  ```
4. `/Stores/WebContent/AuroraStoreFrontAssetStore/Common/EnvironmentSetup.jspf`ファイルで`env_includeJSPFExtension`変数を`true`に構成します

### iQタグ管理の構成

Tealiumデータレイヤーからアナリティクスタグにデータを渡すには、iQタグ管理でデータレイヤーのデータポイントを特定する必要があります：

1. iQタグ管理にログインし、**Data Layer**タブに移動します。
1. **Add Data Source**の隣のドロップダウンをクリックし、**Add Common Data Sources**をクリックします。
1. **Provider Bundles**の下で**IBM WebSphere Commerce**を選択し、**Import This Bundle**をクリックします。![](https://docs.tealium.com/images/tech-partners/ibmwebsphere2.png)
1. **Close**をクリックします。
1. iQタグ管理プロファイルに変更を**Save/Publish**します。

### 検証

実装を検証するには、サイトに移動してページソースを表示します。ページのソースで`utag_data`（TealiumのUDO）を探します。また、配布パッケージに含まれる`Validation.txt`ファイルを参照して、特定のコマースページに関するサンプル値を確認できます。

プロキシツールまたはChrome開発者ツールを使用して、ブラウザが`utag.js`ファイルをロードしていることを確認します。iQタグ管理でタグをアクティブにした後、Charles Proxy、HTTP Fox、またはChrome開発者ツールを使用して、アナリティクスベンダーにデータが渡されていることを確認できます。![](https://docs.tealium.com/images/tech-partners/ibmwebsphere3.png)

`wc.tealium.account`および`wc.tealium.profile`の値は、それぞれサイトに関連付けられたTealiumアカウントとプロファイルです。