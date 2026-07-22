---
title: Floodlight タグ構成ガイド
description: この記事では、Tealium iQタグ管理アカウントでフラッドライトタグを構成する方法を説明します。フラッドライトタグは以前、「DoubleClick Floodlight」としてマーケティングされていました。
url: https://docs.tealium.com/ja/client-side-tags/floodlight-tag/
---

<blockquote>
Googleは、[フラッドライトタグ](https://docs.tealium.com/ja/client-side-tags/floodlight-gtagjs-tag/)を実装することでGoogleグローバルサイトタグへの移行を推奨しています。
</blockquote>


## タグの構成

新しいタグを追加するためにタグマーケットプレイスに移動します。タグの追加方法の一般的な指示については、[タグの概要](https://docs.tealium.com/about-tags/)記事を参照してください。

タグを追加する際には、以下の構成を行います：

* **タイトル** (必須)   
タグインスタンスを識別するための記述的なタイトルを入力します。
* **広告主ID** (必須)   
これは、フラッドライト活動を追跡しているソース広告主のIDです。このフィールドに"src"キーの値を入力します。
* **タイプ** (任意)   
フラッドライト活動のグループ/タイプを識別する8文字の文字列を入力します。
* **カテゴリ** (任意)  
追跡されているフラッドライト活動を識別する8文字の文字列を入力します。
* **カウンタータイプ** (任意)  
ドロップダウンリストをクリックし、フラッドライト活動が発生する頻度を数える方法を構成します。デフォルトでは、これは"Standard"方法に構成されています。  

<blockquote>
すべてのカウント方法は自動的に小文字になります。
</blockquote>

  * **Standard**: これは、フラッドライトが有効なウェブページへの各訪問を別々の活動としてカウントします。
  * **Unique**: これは、24時間以内のユニークなユーザーによるコンバージョンの数をカウントします。
  * **Per Session**: これは、ブラウザーセッションごとにフラッドライト活動を1つだけカウントします。


<blockquote>
このタグを**Tags**タブのリストの上部に配置して、他のタグよりも高い優先順位を与えます。
</blockquote>


## ロードルール

すべてのページでタグをロードするか、タグがロードされる条件を構成します。ロードルールについての詳細は、[ロードルール](https://docs.tealium.com/about-load-rules/)のドキュメンテーションを参照してください。


## データマッピング

マッピングは、データレイヤー変数からベンダータグの対応する宛先変数にデータを送信するプロセスです。タグ宛先に変数をマップする方法については、[データマッピング](https://docs.tealium.com/ja/iq-tag-management/data-mappings/manage/)を参照してください。

以下のマッピングが利用可能です：

|宛先| フラッドライトパラメータ| 説明|
|---| ---| ---|
|Src| `src`| 活動を追跡しているソース広告主のID。|
|Type| `type`| 活動のグループ/タイプを識別する8文字の文字列。|
|Category| `cat`| フラッドライト活動を識別する8文字の文字列。|
|Counter Type| countertype| フラッドライトがコンバージョンを測定する方法。[フラッドライトのコンバージョンカウント方法](https://support.google.com/dcm/partner/answer/2823400?hl=en&ref_topic=4241549)について詳しく読む。|
|Conversion Count| conversioncount| フラッドライトが販売活動を追跡する方法。[フラッドライトの販売カウント方法](https://support.google.com/dcm/partner/answer/2823400?hl=en&ref_topic=4241549)について詳しく読む。|
|U1-U10| `u1-u10`| カスタム変数。[カスタムフラッドライト変数](https://support.google.com/dcm/answer/2823222?hl=en&ref_topic=6094040)について詳しく読む。|
|Order ID| `ord`| トランザクションの一意の識別子（\_corderを上書き）|
|Sub Total| `cost`| トランザクションによって生成された収益の額（\_csubtotalを上書き）|
|List of Product IDs| `prd=iN:`| 購入の製品ID（\_cprodを上書き）。[フラッドライトタグに購入詳細を追加する](https://support.google.com/ds/answer/6026125?hl=en)について詳しく読む。|
|List of Quantities| `prd=qN:`| 購入の製品数量（\_cquanを上書き）。[フラッドライトタグに購入詳細を追加する](https://support.google.com/ds/answer/6026125?hl=en)について詳しく読む。|
|List of Prices| `prd=pN:`| 購入の製品価格（\_cpriceを上書き）。[フラッドライトタグに購入詳細を追加する](https://support.google.com/ds/answer/6026125?hl=en)について詳しく読む。|

## ベンダーのドキュメンテーション

追加の情報については、以下のベンダーのドキュメンテーションを参照してください。

* [フラッドライトについて](https://support.google.com/dcm/partner/answer/4304205?hl=en)
* [フラッドライトのIframeとImageタグ](https://support.google.com/dcm/answer/2823450?hl=en&ref_topic=6094040)
* [カスタムフラッドライト変数](https://support.google.com/dcm/partner/answer/2823222?hl=en)

