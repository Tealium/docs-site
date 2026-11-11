---
title: MediaMathコネクタ構成ガイド
description: この記事では、MediaMathコネクタの構成方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/mediamath-connector/
---## コネクタアクション

| アクション名 | ビジタープロファイル | イベントデータ |
| --- | :---: | :---: |
|カスタムデータを送信| ✓| ✗|

## API情報

このコネクタでは、次のベンダーAPIを使用します。

* API名：MediaMath Ingest API
* APIバージョン：v1
* APIエンドポイント：`https://ingest-default.prod.octane.mediamath.com`

## 構成の構成

コネクタマーケットプレイスに移動し、新しいコネクタを追加します。コネクタを追加する一般的な手順については、[コネクタについて](https://docs.tealium.com/ja/server-side/connectors/manage/)の記事を参照してください。

オーディエンスとトリガーを選択した後、**続行**をクリックし、次に**コネクタを追加**をクリックします。コネクタの名前を入力し、次の項目を構成します。

* **MediaMath広告主ID**  
（必須）MediaMath広告主ID。

コネクタの構成が完了したら、**完了**をクリックします。

## アクション構成 — パラメータとオプション

**続行**をクリックして、コネクタアクションを構成します。アクション名を入力し、ドロップダウンメニューからアクションタイプを選択します。

以下のセクションでは、各アクションのパラメータとオプションの構成方法について説明します。


<blockquote>
Tealium属性をMediaMathカスタム属性にマッピングすると、データをキーと値のペアとして渡すことができます。カスタム属性は、送信前にMediaMathで作成し、許可リストに登録しておく必要があります。
</blockquote>


### アクション — カスタムデータを送信

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|マッピングID| （必須）MediaMathから提供されるマッピングID。|
|MediaMathユーザーID| （必須）ビジターのMediaMath識別子。[MediaMath Cookie Matchingタグ](https://docs.tealium.com/mediamath-cookie-matching-service-tag/)を実装すると、ビジターのMediaMath固有ユーザーID（UUID）が`mediamathid`としてEvent Streaming API Hubに送信されます。|
|ピクセルID| （必須）MediaMathから提供される、構成済みのピクセルID。|