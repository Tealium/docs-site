---
title: Google Publisher Tag セットアップガイドとマッピング
description: この記事では、タグ管理アカウントで Google Publisher Tag を構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/google-publisher-tag/
---Google Publisher Tag は主に広告タグとして使用され、広告スロットと、広告でターゲットにする条件やオーディエンスを定義できます。このタグを適切に構成することで、単一または複数の広告を表示できます。

## 要件

* DFP アカウント
* ネットワークコード
* 広告ユニット
* 広告スロットのクリエイティブサイズ

## タグの構成

タグマーケットプレイスに移動して、新しいタグを追加します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加するときに、次の項目を構成します。

* **タイトル**：タグのインスタンスを識別するためのわかりやすいタイトルを入力します。デフォルトの **Google Publisher Tag(GPT)** を使用することもできます。
* **NC+TAU**：広告スロットのネットワークコード（NC）とターゲット広告ユニット（TAU）を入力します。これらの値は DFP アカウントで確認できます。たとえば、`/1234/travel/asia/food` の場合、NC は `1234`、ターゲット広告ユニットは `/travel/asia/food` です。
* 広告スロットの**幅**と**高さ**を入力します。
* **Div ID**：広告スロット用の `<div>` コンテナの ID を入力します。一般的な形式は `div-gpt-ad-#########-#` です。  
例：`div-gpt-ad-123456789-0`
* **空の Div を折りたたむ**：広告が配信されなかった場合に、スロットを折りたたむかどうかを選択します。デフォルト値は **Yes** です。**No** に切り替えると、空のスロットが表示されます。
* **ライブラリ**：`gpt.js` ライブラリコードの読み込み元を選択します。
  * **Google**：（デフォルト）Google のサーバーからライブラリコードを読み込みます。
  * **Tealium**：（推奨）Web ページ上の Tealium のコードを介してライブラリコードを読み込みます。ネットワークリクエスト数が減り、ページの読み込みが速くなるため、この構成を推奨します。


<blockquote>
これらの構成は、マッピングツールボックスから構成することもできます。
</blockquote>


## 読み込みルール

すべてのページでタグを読み込むか、タグを読み込む条件を構成します。読み込みルールの詳細については、[読み込みルール](https://docs.tealium.com/about-load-rules/)のドキュメントを参照してください。

**ベストプラクティス**：ターゲット広告スロットを含むすべてのページで、このタグを読み込んでください。

## データマッピング

マッピングとは、データレイヤー内のデータソースから、ベンダータグの対応する宛先変数にデータを送信する処理です。このタグの宛先変数は、データマッピングツールボックスで確認できます。

タグの宛先にデータをマッピングする方法については、[データソースのマッピング](https://docs.tealium.com/about-data-mappings/#mapping_data_sources)を参照してください。

|宛先名|宛先変数|説明|
|---|---|---|
|ネットワークコード|`networkcode`|このコードは、DFP アカウントの管理タブで確認できます。|
|ターゲット広告ユニット|`adunit`|ターゲットとする広告ユニットです。|
|高さ|`height`|広告スロットの高さです。|
|幅|`weight`|広告スロットの幅です。|
|スロットレベルのターゲティングを構成|`setTargeting_slot`|ターゲット広告スロットの `key:value` パラメータを構成します。<br>例：`.setTargeting("interests", "sports");`|
|ページレベルのターゲティングを構成|`myvar`|ページ上のすべての広告スロットに対して `key:value` パラメータを構成します。<br>注："myvar" をカスタムターゲティングパラメータ名に置き換えてください。<br>例：`googletag.pubads().setTargeting("topic","sports");`|
|複数スロットの構成|`gptSlots`|単一ページのスロット配列を定義します（[詳細は以下を参照](#multiple_slots)）。<br>注：マッピング元のデータソースに配列が含まれていることを確認してください。|
|空の DIV を折りたたむ|`collapseEmptyDivs`|広告が配信されなかった広告スロットを折りたたみます。<br>注：データソースの値に `true` または `false` が含まれていることを確認してください。|
|パブリッシャー提供 ID|`publisherProvidedId`|フリークエンシーキャップやその他のオーディエンスベースの処理で使用する、パブリッシャー提供 ID の値を構成します。|

## 複数の広告スロット用にタグを構成する

単一の広告スロットに GPT を追加して構成する作業は、非常に簡単です。ただし、同じ手順で複数の広告スロットを構成する場合、表示するすべての広告に対して GPT のインスタンスを追加する必要があるため、手間がかかります。より効率的な方法は、すべてのスロット構成を配列に格納し、その配列を GPT インスタンスの**複数スロットの構成**宛先にマッピングすることです。このような配列を作成するには、[JavaScript コード拡張機能](https://docs.tealium.com/javascript-code-extension/)を使用できます。各広告のスロット構成は、次の順序で定義してください。

ネットワークコード + ターゲット広告ユニット、使用可能なクリエイティブサイズ、広告コンテナの DIV ID、スロットレベルのターゲティング名と値のペア

### JavaScript コード拡張機能の使用

`googletag.cmd.push` 関数を使用して、ページに表示するすべての広告のスロット構成を配列として定義する JavaScript コードを記述します。

1. 拡張機能タブに移動し、拡張機能マーケットプレイスから [JavaScript コード拡張機能](https://docs.tealium.com/javascript-code-extension/)を追加します。
1. 拡張機能のスコープを **Google Publisher Tag(GPT)** に構成します。
1. 通常のエディターと同じように JavaScript コードを記述します。コードを囲む `<script>` タグは含めないでください。

以下は、単一の GPT を使用して 3 つの広告スロットを構成するサンプルコードです。

```js
googletag.cmd.push(function() {
   googletag.defineSlot("/111/example.com/electronics", [700, 200], "div-gpt-ad-987654321-0").addService(googletag.pubads()).setTargeting("slot_var", "tv");
   googletag.defineSlot("/222/example.com/electronics", [250, 170], "div-gpt-ad-987654321-1").addService(googletag.pubads()).setTargeting("slot_var", "dvd player");
   googletag.defineSlot("/333/example.com/electronics", [300, 100], "div-gpt-ad-987654321-2").addService(googletag.pubads()).setTargeting("slot_var", "smartphone");
   googletag.pubads().enableSingleRequest();
   googletag.pubads().enableSyncRendering();
   googletag.enableServices();
});
```


<blockquote>
`googletag.cmd.push` の代わりに `u.gptSlots.push()` メソッドを使用し、データソースから NC+TAU 値を参照することもできます。<br>
例：`u.gptSlots.push([b.GPT_SlotID, [[728, 90]], 'div-gpt-ad-987654321-0', {"place":"london","theme":"sports"}]);`
</blockquote>


## ベンダーのドキュメント

* [GPT の概要](https://support.google.com/admanager/answer/181073?hl=en)
* [GPT を使用したターゲティングとサイズの構成](https://support.google.com/dfp_sb/answer/1698183?hl=en)
* [空の div 要素の折りたたみ](https://support.google.com/dfp_sb/answer/3419382?hl=en&ref_topic=4409240)
* [タグのサンプル](https://support.google.com/dfp_sb/answer/1651549?hl=en&ref_topic=4409240)