---
title: Adition タギングコネクタ構成ガイド
description: この記事では、Adition タギングコネクタの構成方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/adition-tagging-connector/
---
## コネクタアクション

| アクション名 | AudienceStream | EventStream |
| --- | :---: | :---: |
|訪問をタグ付け| ✓| ✗|

## 構成の構成

**コネクタマーケットプレイス**にアクセスし、新しいコネクタを追加します。コネクタを追加する一般的な手順については、[コネクタ概要]()の記事を参照してください。

コネクタを追加した後、以下の構成を構成します：

## アクション構成 - パラメータとオプション

**次へ**をクリックするか、**アクション**タブに進みます。ここでコネクタアクションを構成します。

このセクションでは、各アクションのパラメータとオプションの構成方法について説明します。

### アクション - 訪問をタグ付け

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|エンドポイント URL|  &lt;ul&gt;&lt;li&gt;オプション。&lt;/li&gt;&lt;li&gt;デフォルトのエンドポイントは &lt;https://ad13.adfarm1.adition.com/tagging&gt;&lt;/li&gt;&lt;li&gt;割り当てられたエンドポイント URL を提供してください。&lt;/li&gt;&lt;li&gt;提供された場合、デフォルトのエンドポイントを上書きします&lt;/li&gt;&lt;li&gt;例：&lt;ul&gt;&lt;li&gt;&lt;https://adfarm1.adition.com/tagging&gt;&lt;/li&gt;&lt;li&gt;&lt;https://ad1.adfarm1.adition.com/tagging&gt;&lt;/li&gt;&lt;li&gt;&lt;https://ad2.adfarm1.adition.com/tagging&gt;&lt;/li&gt;&lt;li&gt;&lt;https://ad3.adfarm1.adition.com/tagging&gt;&lt;/li&gt;&lt;li&gt;&lt;https://ad11.adfarm1.adition.com/tagging&gt;&lt;/li&gt;&lt;li&gt;&lt;https://ad13.adfarm1.adition.com/tagging&gt;&lt;/li&gt;&lt;/ul&gt; &lt;/li&gt;&lt;/ul&gt; |
|クライアント ID|  &lt;ul&gt;&lt;li&gt;Adition クライアント ID を提供してください。&lt;/li&gt;&lt;li&gt;例: `3133`&lt;/li&gt;&lt;/ul&gt; |
|タグ|  &lt;ul&gt;&lt;li&gt;Aditionで構成されたキーとサブキーにカスタム値をマッピングします。&lt;/li&gt;&lt;li&gt;例: 文字列 `current` を `tag[tealium.abc_de]` にマッピング。&lt;/li&gt;&lt;li&gt;複数のマッピングを追加できます&lt;/li&gt;&lt;/ul&gt; |
|Adition Cookie|  &lt;ul&gt;&lt;li&gt;Adition cookie 同期からの値を含む文字列変数をクッキー名 `UserID1` にマッピングします。&lt;/li&gt;&lt;/ul&gt; |
