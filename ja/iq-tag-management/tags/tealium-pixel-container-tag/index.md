---
title: Tealium Pixel Container タグ
description: Tealium Pixel Containerは、同じページに最大8つのピクセルをロードできるタグです。このタグは、タグマーケットプレイスにまだ追加されていないベンダータグを実装するために使用できます。
url: https://docs.tealium.com/ja/iq-tag-management/tags/tealium-pixel-container-tag/
---
Pixel Containerタグが使用される場合のほとんどで、より多くのオプションを提供する[Tealium Generic Tag]()がより良い選択です。Pixel Containerは、同じロードルールを使用する複数のシンプルなタグを追加する際に最適です。

## タグの種類

このタグは、画像とiframeの2つの形式をサポートしています。正しい形式を決定することが適切な構成には不可欠です。以下のガイドラインを使用して、どのタイプを扱っているかを特定してください。タグのコードが以下のパターンのいずれかに一致する場合、構成時に対応するタグタイプを選択してください。

### 画像

画像タグのコードスニペットには通常、以下のいずれかが含まれます：

* `new Image()`
* `&lt;img src=&#34;https://`
* `document.write(&#34;&lt;img src=&#34; ... &#34;&gt;&#34;);`

例えば、ベンダーがこのようなスニペットを提供するかもしれません：

```html
&lt;img src=&#34;http://ads.example.net/track?src=1234567&amp;type=abcde123&amp;cat=fghij456&#34; width=&#34;1&#34; height=&#34;1&#34; style=&#34;display:none&#34;&gt;
```

このピクセルを構成するには、`src` URLを抽出して**Pixel URL**フィールドに入力します：

`http://ads.example.net/track?src=1234567&amp;type=abcde123&amp;cat=fghij456`

### Iframe

Iframeタグのコードスニペットには通常、以下のいずれかが含まれます：

* `document.createElement(&#39;iframe&#39;)`
* `&lt;iframe src=&#34;https://`
* `document.write(&#34;&lt;iframe src=&#34; ... &#34;&gt;&lt;/iframe&#34;);`

例えば、ベンダーがこのようなスニペットを提供するかもしれません：

```html
&lt;iframe src=&#34;http://ads.example.net/track?src=1234567&amp;type=abcde123&amp;cat=fghij456&#34; width=&#34;1&#34; height=&#34;1&#34; frameborder=&#34;0&#34;&gt;&lt;/iframe&gt;
```

このピクセルを構成するには、`src` URLを抽出して**Pixel URL**フィールドに入力します：

`http://ads.example.net/track?src=1234567&amp;type=abcde123&amp;cat=fghij456`

## タグの構成

まず、タグマーケットプレイスにアクセスして、プロファイルにTealium Pixel Containerを追加します。

![](/images/iq-tag-management/tags/tealium_pixel_container_tag.png)

タグを追加した後、以下の構成を構成します：

* **Title**: デフォルトは`Tealium Pixel (or Iframe) Container`です。お好みでカスタム名に置き換えることができます。
* **Type**: タグのタイプを選択します。
* **Auto Cache Bust:** 有効にすると、各ピクセルURLにランダムに生成された値がクエリパラメータとして追加されます。この値は、ブラウザーや広告サーバーがピクセルのキャッシュバージョンを提供するのを防ぎます。たとえば、ピクセルURLが`https://ads.example.net/track?src=1234567`の場合、タグは次のように発火します：`https://ads.example.net/track?src=1234567&amp;_rnd=0.7351829476`
* **Cache Bust Name**: (オプション) キャッシュバストパラメータのカスタム名をデフォルトの`_rnd`の代わりに指定します。たとえば、`ord`を入力すると、タグは次のように発火します：`https://ads.example.net/track?src=1234567&amp;ord=0.7351829476`
* **Pixel 1-8**: ロードする各ピクセルのURL。各URLが`http://`, `https://`, または`//`で始まることを確認してください。
* **Pixel 1-8 Title**: 各ピクセルにタイトルを提供します。

## 動的値の置換

このタグは動的値の置換をサポートしており、Pixel 1-8の構成フィールドで直接データレイヤー変数を参照することができます。これにより、データレイヤーに基づいて動的なタグURLを作成する柔軟性が提供されます。ピクセルURLにデータレイヤー変数を挿入するには、変数名を`@@`で囲んで参照します。たとえば、URLのパスに`account_id`というデータレイヤー変数を挿入するには、次のような値を入力します：`//example.com/path/@@account_id@@/i.gif`

データレイヤー変数を置換するためには、以下のプレフィックスを使用します：

* **Universal Data Object**:`@@variable@@`
* **JavaScript Page Variable**: `@@js\_page.variable@@`
* **Meta Tag**: `@@meta.variable@@`
* **Querystring Parameter**: `@@qp.variable@@`
* **Cookie Value**: `@@cp.variable@@`

## ロードルール

[ロードルール]()は、サイト上でこのタグのインスタンスをいつ、どこでロードするかを決定します。

## データマッピング

このタグはデータマッピングをサポートしていません。すべてのパラメータはピクセルのURLに構成する必要があります。