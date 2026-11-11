---
title: Floodlightタグ構成ガイド
description: この記事では、タグ管理アカウントでFloodlightタグを構成する方法について説明します。Floodlightタグは、以前は「DoubleClick Floodlight」という名称で提供されていました。
url: https://docs.tealium.com/ja/client-side-tags/floodlight-tag/
---

<blockquote>
Googleでは、[Floodlightタグ](https://docs.tealium.com/ja/client-side-tags/floodlight-gtagjs-tag/)を実装してGoogleグローバルサイトタグに移行することを推奨しています。
</blockquote>


## タグの構成

タグマーケットプレイスに移動して、新しいタグを追加します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加する際に、以下の構成を行います。

* **タイトル**（必須）   
タグインスタンスを識別するための、わかりやすいタイトルを入力します。
* **広告主ID**（必須）   
Floodlightアクティビティをトラッキングするソース広告主のIDです。このフィールドに「src」キーの値を入力します。
* **タイプ**（任意）   
Floodlightアクティビティのグループ／タイプを識別する8文字の文字列を入力します。
* **カテゴリ**（任意）  
トラッキング対象のFloodlightアクティビティを識別する8文字の文字列を入力します。
* **カウンタータイプ**（任意）  
ドロップダウンリストをクリックし、Floodlightアクティビティの発生頻度をカウントする方法を構成します。デフォルトでは「標準」方式に構成されています。  

<blockquote>
すべてのカウント方法は、自動的に小文字へ変換されます。
</blockquote>

  * **標準**：Floodlightが有効になっているWebページへの各訪問を、それぞれ個別のアクティビティとしてカウントします。
  * **ユニーク**：24時間以内のユニークユーザーによるコンバージョン数をカウントします。
  * **セッションごと**：ブラウザーセッションごとに、Floodlightアクティビティを1回だけカウントします。


<blockquote>
他のタグよりも優先度を高くするには、**タグ**タブのリストの先頭にこのタグを配置します。
</blockquote>


## 読み込みルール

すべてのページでタグを読み込むか、タグを読み込む条件を構成します。読み込みルールの詳細については、[読み込みルール](https://docs.tealium.com/about-load-rules/)のドキュメントを参照してください。


## データマッピング

データマッピングは、データレイヤー変数の値をベンダータグ内の対応する変数に送信します。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

以下のマッピングを使用できます。

|送信先| Floodlightパラメータ| 説明|
|---| ---| ---|
|ソース| `src`| アクティビティをトラッキングするソース広告主のIDです。|
|タイプ| `type`| アクティビティのグループ／タイプを識別する8文字の文字列です。|
|カテゴリ| `cat`| Floodlightアクティビティを識別する8文字の文字列です。|
|カウンタータイプ| countertype| Floodlightでコンバージョンを測定する方法です。詳しくは、[Floodlightコンバージョンのカウント方法](https://support.google.com/dcm/partner/answer/2823400?hl=en&ref_topic=4241549)を参照してください。|
|コンバージョン数| conversioncount| Floodlightで販売アクティビティをトラッキングする方法です。詳しくは、[Floodlight販売のカウント方法](https://support.google.com/dcm/partner/answer/2823400?hl=en&ref_topic=4241549)を参照してください。|
|U1～U10| `u1-u10`| カスタム変数です。詳しくは、[カスタムFloodlight変数](https://support.google.com/dcm/answer/2823222?hl=en&ref_topic=6094040)を参照してください。|
|注文ID| `ord`| トランザクションの一意の識別子です（\_corderを上書きします）。|
|小計| `cost`| トランザクションによって発生した収益額です（\_csubtotalを上書きします）。|
|商品IDのリスト| `prd=iN:`| 購入商品の商品IDです（\_cprodを上書きします）。詳しくは、[Floodlightタグへの購入詳細の追加](https://support.google.com/ds/answer/6026125?hl=en)を参照してください。|
|数量のリスト| `prd=qN:`| 購入商品の数量です（\_cquanを上書きします）。詳しくは、[Floodlightタグへの購入詳細の追加](https://support.google.com/ds/answer/6026125?hl=en)を参照してください。|
|価格のリスト| `prd=pN:`| 購入商品の価格です（\_cpriceを上書きします）。詳しくは、[Floodlightタグへの購入詳細の追加](https://support.google.com/ds/answer/6026125?hl=en)を参照してください。|

## ベンダーのドキュメント

詳細については、以下のベンダードキュメントを参照してください。

* [Floodlightについて](https://support.google.com/dcm/partner/answer/4304205?hl=en)
* [FloodlightのIframeタグと画像タグ](https://support.google.com/dcm/answer/2823450?hl=en&ref_topic=6094040)
* [カスタムFloodlight変数](https://support.google.com/dcm/partner/answer/2823222?hl=en)