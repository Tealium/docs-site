---
title: Adition タギングコネクタ構成ガイド
description: この記事では、Adition タギングコネクタの構成方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/adition-tagging-connector/
---
## コネクタアクション

| アクション名 | 訪問プロファイル | イベントデータ |
| --- | :---: | :---: |
|訪問をタグ付け| ✓| ✗|

## 構成の構成

コネクタマーケットプレイスに移動し、新しいコネクタを追加します。詳細については、[about-connectors](https://docs.tealium.com/about-connectors/)を参照してください。

コネクタを追加した後、以下の構成を構成します。

## アクション構成 - パラメータとオプション

**続行**をクリックして、コネクタアクションを構成します。アクションの名前を入力し、リストからアクションタイプを選択します。

### アクション - 訪問をタグ付け

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|エンドポイントURL| <ul><li>（任意）デフォルトのエンドポイントは <https://ad13.adfarm1.adition.com/tagging> です。</li><li>割り当てられたエンドポイントURLを指定します。</li><li>指定した場合、デフォルトのエンドポイントが上書きされます。</li><li>例：<ul><li><https://adfarm1.adition.com/tagging></li><li><https://ad1.adfarm1.adition.com/tagging></li><li><https://ad2.adfarm1.adition.com/tagging></li><li><https://ad3.adfarm1.adition.com/tagging></li><li><https://ad11.adfarm1.adition.com/tagging></li><li><https://ad13.adfarm1.adition.com/tagging></li></ul></li></ul> |
|クライアントID| <ul><li>AditionのクライアントIDを指定します。</li><li>例：`3133`</li></ul> |
|タグ| <ul><li>Aditionで構成されているキーおよびサブキーにカスタム値をマッピングします。</li><li>例：文字列`current`を`tag[tealium.abc_de]`にマッピングします。</li><li>複数のマッピングを追加できます。</li></ul> |
|Adition Cookie| <ul><li>Adition Cookie Syncから取得した値を含む文字列変数を、Cookie名`UserID1`にマッピングします。</li></ul> |