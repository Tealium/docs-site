---
title: 複数の Floodlight タグの構成
description: この記事では、タグ管理アカウントで複数の Floodlight タグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/configuring-multiple-floodlight-tags/
---読み込み条件（URL 内の異なるパスなど）は同じでも、構成が少しずつ異なる Floodlight タグが多数ある場合、読み込みルールと構成値が異なる類似した Floodlight タグのインスタンスを複数構成する代わりに、追加構成を使用して 1 つの Floodlight タグのインスタンスにまとめることができます。


<blockquote>
Google では、[Floodlight タグ](https://docs.tealium.com/ja/client-side-tags/floodlight-gtagjs-tag/)を実装して Google グローバルサイトタグに移行することを推奨しています。
</blockquote>


## 仕組み

このマルチタグソリューションでは、データマッピングを使用して Floodlight パラメータを動的に構成し、ルックアップテーブルを使用してデータレイヤー変数に基づく Floodlight の値を構成します。ルックアップテーブルは、エントリごとに複数の値を含む区切り文字付き文字列を作成します。この文字列は、JavaScript コード拡張機能を使用して個別の Floodlight パラメータに分割できます。

## 新しいデータレイヤー変数

Floodlight タグのデータマッピングとルックアップテーブル拡張機能には、以下の変数が必要です。「dc_」プレフィックスは、これらの変数が Floodlight の構成に使用されることを示すためのベストプラクティスです。

以下を作成します。

* **dc\_advertiserId**（マッピング）
* **dc\_type**（マッピング）
* **dc\_category**（マッピング）
* **dc\_counterType**（マッピング）
* **dc\_settings**（ルックアップテーブル拡張機能）

## データマッピング

このマルチタグソリューションでは、Floodlight パラメータがルックアップテーブル拡張機能の出力に基づいて動的に構成されるため、タグ構成内でデータマッピングを使用して値を構成する必要があります。

以下のデータマッピングを構成します。

* `dc_advertiserId` を `src` に構成
* `dc_counterType` を `countertype` に構成
* `dc_type` を `type` に構成
* `dc_category` を `cat` に構成

完了すると、マッピングは次のようになります。

![](https://docs.tealium.com/images/client-side-tags/doubleclick-multi-tag-data-mappings.png)

## 拡張機能

このソリューションでは、配信するすべての Floodlight タグを構成するために 3 つの拡張機能を使用します。以下の拡張機能を追加し、ここに示す順序で並べる必要があります。

* **ルックアップテーブル**  
選択条件（この例では URL のパス名）に基づいて、区切り文字付き文字列を構成します。
* **データ値の構成**  
ルックアップテーブルから取得した区切り文字付き文字列を、個別の Floodlight 変数に変換します。
* **JavaScript コード**  
タグを配信するための値が存在することを確認します。値がない場合はタグを抑制します。

### ルックアップテーブル拡張機能

この拡張機能は、条件変数に基づいて区切り文字付き文字列を構成するために使用します。この例では、条件変数は `pathname` 変数であり、区切り文字付き文字列は、次の形式で構成された `dc_settings` 変数です。

```
ADVERTISER ID|TYPE|CATEGORY|COUNTERTYPE
```

この拡張機能を追加するには、次の手順を実行します。

1. [ルックアップテーブル拡張機能](https://docs.tealium.com/lookup-table-extension/)を追加します。
1. **タイトル**を構成します。例：「DC 構成」。
1. **スコープ**を、追加した Floodlight タグに構成します。
1. **検索対象の値**を `pathname` に構成します。
1. **宛先**を `dc_settings` に構成します。
1. **変数タイプ**を「文字列」に構成します。
1. **一致タイプ**を「含む」に構成します。

ルックアップテーブルの各エントリには、URL のパス名と区切り文字付き文字列値が含まれます。この例では、以下のエントリを使用します。

|**パス名**| **出力**|
|---| ---|
|/test1/test| 321123|Testing|Test001|standard|
|/test2/test/something.htm| 321123|Testing|Test002|standard|
|/test1/docs| 321123|Docs|Test003|standard|

ルックアップテーブル拡張機能は次のようになります。

![](https://docs.tealium.com/images/client-side-tags/doubleclick-multi-tag-lookup-table.png)


<blockquote>
長いリストを管理するには、**CSV からインポート...**オプションを使用してください。
</blockquote>


### データレイヤー構成拡張機能

この拡張機能は、区切り文字付き文字列を個別の Floodlight 変数に分割します。

この拡張機能を追加するには、次の手順を実行します。

1. [データ値の構成拡張機能](https://docs.tealium.com/set-data-values-extension/)を追加します。
1. **タイトル**を構成します。例：「Floodlight パラメータ」。
1. **スコープ**を、追加した Floodlight タグに構成します。
1. Floodlight パラメータごとに変数を構成します。

|**構成する変数**| **値のタイプ**| **値**|
| --- | --- | --- |
|dc\_advertiserId| JS コード| **b['dc_settings'].split("&#124;")[0]** |
| dc\_type| JS コード| **b['dc_settings'].split("&#124;")[1]**|
| dc\_category| JS コード| **b['dc_settings'].split("&#124;")[2]**|
| dc\_counterType| JS コード| **b['dc_settings'].split("&#124;")[3]**|

拡張機能は次のようになります。

![](https://docs.tealium.com/images/client-side-tags/doubleclick-multi-tag-set-data.png)


<blockquote>
値が存在する場合にのみ実行されるようにするには、**条件を追加**を使用して `dc_settings` に値が構成されていることを確認してください。
</blockquote>


### JavaScript コード

この拡張機能は、ルックアップテーブル拡張機能が値を出力しなかった場合、つまり配信するタグがない場合に、Floodlight タグを抑制します。これにより、Floodlight タグに「すべてのページ」の読み込みルールを構成したままにしても、現在のページに対応する構成がない場合はタグが配信されません。

この拡張機能を追加するには、次の手順を実行します。

1. [JavaScript コード拡張機能](https://docs.tealium.com/advanced-javascript-code-extension/)を追加します。
1. **タイトル**を構成します。例：「値の確認」。
1. **スコープ**を、追加した Floodlight タグに構成します。
1. 次のコードを入力します。  
```
if(b['dc_settings']===''){
    return false;
}
```

1. テストのために変更内容をパブリッシュします。