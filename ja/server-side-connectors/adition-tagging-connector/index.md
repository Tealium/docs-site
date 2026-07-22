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

**コネクタマーケットプレイス**にアクセスし、新しいコネクタを追加します。コネクタを追加する一般的な手順については、[コネクタ概要](https://docs.tealium.com/about-connectors/)の記事を参照してください。

コネクタを追加した後、以下の構成を構成します：

## アクション構成 - パラメータとオプション

**次へ**をクリックするか、**アクション**タブに進みます。ここでコネクタアクションを構成します。

このセクションでは、各アクションのパラメータとオプションの構成方法について説明します。

### アクション - 訪問をタグ付け

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|エンドポイント URL|  <ul><li>オプション。</li><li>デフォルトのエンドポイントは <https://ad13.adfarm1.adition.com/tagging></li><li>割り当てられたエンドポイント URL を提供してください。</li><li>提供された場合、デフォルトのエンドポイントを上書きします</li><li>例：<ul><li><https://adfarm1.adition.com/tagging></li><li><https://ad1.adfarm1.adition.com/tagging></li><li><https://ad2.adfarm1.adition.com/tagging></li><li><https://ad3.adfarm1.adition.com/tagging></li><li><https://ad11.adfarm1.adition.com/tagging></li><li><https://ad13.adfarm1.adition.com/tagging></li></ul> </li></ul> |
|クライアント ID|  <ul><li>Adition クライアント ID を提供してください。</li><li>例: `3133`</li></ul> |
|タグ|  <ul><li>Aditionで構成されたキーとサブキーにカスタム値をマッピングします。</li><li>例: 文字列 `current` を `tag[tealium.abc_de]` にマッピング。</li><li>複数のマッピングを追加できます</li></ul> |
|Adition Cookie|  <ul><li>Adition cookie 同期からの値を含む文字列変数をクッキー名 `UserID1` にマッピングします。</li></ul> |
