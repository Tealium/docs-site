---
title: オムニチャネルファイルステータスAPIについて
description: オムニチャネルファイルステータスAPIは、オムニチャネルファイルの詳細なステータス情報を提供します。
url: https://docs.tealium.com/ja/api/v2/omnichannel-file-status/about/
---
## 仕組み
オムニチャネルファイルステータスAPIは、ファイルがインポートされたタイミング、処理方法、および処理エラーの詳細を示すファイルステータスを返します。

## 前提条件

オムニチャネルファイルステータスAPIを使用するには、以下が必要です：

* 構成済みの[ファイルインポートデータソース](https://docs.tealium.com/about-file-import/)
* Tealium iQタグ管理からのAPIキー

## 認証


<blockquote>
ベアラートークンはすべてのAPI呼び出しを認証するために使用され、APIキーではありません。APIキーは認証呼び出しでのみ使用されます。
</blockquote>


APIキーからベアラートークンを生成する方法については、[はじめに](https://docs.tealium.com/api-authentication/)ガイドを参照してください。
