---
title: 複数のFloodlightタグの構成
description: この記事では、Tealium iQタグ管理アカウントで複数のFloodlightタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/configuring-multiple-floodlight-tags/
---もし多くのFloodlightタグを持っており、それぞれがわずかに異なる構成を持ちながらも、同じロード基準に基づいている場合（例えば、URLの異なるパス）、Floodlightタグの複数の類似したインスタンスを構成するのではなく、それぞれに異なるロードルールと構成値を持つようにする代わりに、それらを追加の構成を使用してFloodlightタグの1つのインスタンスに組み合わせることができます。


<blockquote>
Googleは、[Floodlightタグ](https://docs.tealium.com/ja/client-side-tags/floodlight-gtagjs-tag/)を実装することにより、Googleグローバルサイトタグへの移行を推奨しています。
</blockquote>


## 仕組み

このマルチタグソリューションは、データマッピングを使用してFloodlightパラメータを動的に構成し、データレイヤー変数に基づいてFloodlight値を構成するためのルックアップテーブルを使用します。ルックアップテーブルは、エントリごとに複数の値を含む区切り文字列を作成し、それをJavaScript Code拡張を使用して個々のFloodlightパラメータに分割します。

## 新しいデータレイヤー変数

Floodlightタグとルックアップテーブル拡張のデータマッピングには、以下の変数が必要です。"dc_"プレフィックスは、これらの変数がFloodlight構成に使用されることを思い出させるためのベストプラクティスです。

以下を作成します：

* **dc\_advertiserId** (マッピング)
* **dc\_type** (マッピング)
* **dc\_category** (マッピング)
* **dc\_counterType** (マッピング)
* **dc\_settings** (ルックアップテーブル拡張)

## データマッピング

このマルチタグソリューションでは、Floodlightパラメータはルックアップテーブル拡張の出力に基づいて動的に構成されるため、値はタグ構成でデータマッピングを使用して構成する必要があります。

以下のデータマッピングを構成します：

* `dc_advertiserId` を `src` に構成
* `dc_counterType` を `countertype` に構成
* `dc_type` を `type` に構成
* `dc_category` を `cat` に構成

これらを完了すると、マッピングは以下のようになります：

![](https://docs.tealium.com/images/client-side-tags/doubleclick-multi-tag-data-mappings.png)

## 拡張機能

このソリューションでは、発火させる予定のすべてのFloodlightタグを構築するために3つの拡張機能を使用します。以下の拡張機能が追加され、ここに表示される順序で並べ替える必要があります：

* **ルックアップテーブル**  
これは、選択基準（この場合はURLのパス名）に基づいて区切り文字列を構成します。
* **データ値の構成**  
これは、ルックアップテーブルからの区切り文字列を別々のFloodlight変数に変換します。
* **JavaScriptコード**  
これは、タグが発火するための値が存在することを確認し、そうでなければタグを抑制します。

### ルックアップテーブル拡張

この拡張機能は、基準変数に基づいて区切り文字列を構成するために使用されます。この例では、基準変数は`pathname`変数で、区切り文字列は以下の形式で構成された`dc_settings`変数です：

```
ADVERTISER ID|TYPE|CATEGORY|COUNTERTYPE
```

この拡張機能を追加するには：

1. [ルックアップテーブル拡張](https://docs.tealium.com/lookup-table-extension/)を追加します。
1. **タイトル**を構成します。例えば、"DC Settings"。
1. **スコープ**を先ほど追加したFloodlightタグに構成します。
1. **Lookup Value In**に：`pathname`を構成します。
1. **Destination**に：`dc_settings`を構成します。
1. **Variable Type**に：Stringを構成します。
1. **Match Type**に：Containsを構成します。

各ルックアップテーブルエントリには、URLのパス名と区切り文字列の値が含まれます。この例では、以下のエントリを使用します：

|**Pathname**| **Output**|
|---| ---|
|/test1/test| 321123|Testing|Test001|standard|
|/test2/test/something.htm| 321123|Testing|Test002|standard|
|/test1/docs| 321123|Docs|Test003|standard|

ルックアップテーブル拡張は以下のように表示されるべきです：

![](https://docs.tealium.com/images/client-side-tags/doubleclick-multi-tag-lookup-table.png)


<blockquote>
長いリストを管理するために**CSVからインポート...**オプションを使用します。
</blockquote>


### データレイヤー拡張の構成

この拡張機能は、区切り文字列を別々のFloodlight変数に分割します。

この拡張機能を追加するには：

1. [データ値構成拡張](https://docs.tealium.com/set-data-values-extension/)を追加します。
1. **タイトル**を構成します。例えば："Floodlight Parameters"。
1. **スコープ**を先ほど追加したFloodlightタグに構成します。
1. Floodlightパラメータごとに変数を構成します：

|**Set Variable**| **Value Type**| **Value**|
| --- | --- | --- |
|dc\_advertiserId| JS Code| **b['dc_settings'].split("&#124;")[0]** |
| dc\_type| JS Code| **b['dc_settings'].split("&#124;")[1]**|
| dc\_category| JS Code| **b['dc_settings'].split("&#124;")[2]**|
| dc\_counterType| JS Code| **b['dc_settings'].split("&#124;")[3]**|

拡張機能は以下のように表示されるべきです：

![](https://docs.tealium.com/images/client-side-tags/doubleclick-multi-tag-set-data.png)


<blockquote>
`dc_settings`が入力されていることを確認するために**条件を追加**を使用します。これにより、値があるときだけ実行されることが保証されます。
</blockquote>


### JavaScriptコード

この拡張機能は、ルックアップテーブル拡張が値を出力しなかった場合、つまりタグが発火するものがない場合、Floodlightタグを抑制します。これにより、Floodlightタグに"All Pages"ロードルールを構成したままにしておくことができ、現在のページに対する構成がない場合には発火しないようにすることができます。

この拡張機能を追加するには：

1. [JavaScript Code拡張](https://docs.tealium.com/advanced-javascript-code-extension/)を追加します。
1. **タイトル**を構成します。例えば："Check Value"。
1. **スコープ**を先ほど追加したFloodlightタグに構成します。
1. 以下のコードを入力します：  
```
if(b['dc_settings']===''){
    return false;
}
```

1. テストのために変更を公開します。