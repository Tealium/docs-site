---
title: Nielsen Digital Content Ratings（DCR）- ページ測定タグ構成ガイド
description: この記事では、タグ管理アカウントで Nielsen Digital Content Ratings（DCR）- ページ測定タグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/nielsen-digital-content-ratings-dcr-page-measurement-tag/
---
## タグの構成

まず、タグマーケットプレイスに移動し、Nielsen Digital Content Ratings（DCR）- ページ測定タグをプロファイルに追加します（[タグの追加](https://docs.tealium.com/manage-tags/#add-a-tag)を参照）。

タグを追加したら、以下の構成を行います。

1. **クライアント ID**：Nielsen のクライアント識別子です。`nol_ci` キーで Nielsen に渡されます。
1. **サブブランド ID**：Nielsen のサブブランド ID です。`nol_vc` キーで Nielsen に渡されます。
1. **アプリ ID**：プレーヤー／サイトに割り当てられた一意の Nielsen ID です。`nol_apid` キーで Nielsen に渡されます。
1. **パブリッシャー名**：プレーヤー／サイトを識別するためのユーザー定義の文字列値です。`nol_apn` キーで Nielsen に渡されます。
1. **収集環境**：Nielsen 収集環境の場所です。`nol_sfcode` キーで Nielsen に渡されます。
1. **サイトセクションにパスを使用**：`yes` に構成すると、Web ページのパスにある最初のフォルダーがサイトセクションとして使用されます。最初のフォルダーが存在しない、または利用できない場合、**サイトセクション**の値はデフォルトで `home` になります。**サイトセクション**の値は、データマッピングでも構成できます（以下を参照）。


<blockquote>
サイトセクションのレポートで使用できる一意の値は、最大 25 個に制限されています。
</blockquote>


## ロードルール

[ロードルール](https://docs.tealium.com/about-load-rules/)は、サイト上でこのタグのインスタンスをいつ、どこで読み込むかを決定します。

推奨ロードルール：**すべてのページで読み込む**。

## データマッピング

データマッピングは、データレイヤー変数の値をベンダータグ内の対応する変数に送信します。詳しくは、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

Nielsen Digital Content Ratings（DCR）- ページ測定タグの宛先変数は、［データマッピング］タブに組み込まれています。利用可能なカテゴリーは次のとおりです。

### 標準

|**宛先名**| **説明**|
|---| ---|
|クライアント ID|Nielsen クライアント ID。ベンダー構成で構成された値を上書きします。詳しくは、上記の「タグの構成」を参照してください。|
|サブブランド ID|Nielsen サブブランド ID。ベンダー構成で構成された値を上書きします。詳しくは、上記の「タグの構成」を参照してください。|
|サイトセクション|カスタムサイトセクションを送信できます（一意の値は最大 25 個に制限されます）。`nol_assetname` キーで Nielsen に渡されます。マッピングが空の値を返した場合、**サイトセクション**はデフォルト値の `home` に構成されます。**注**：この宛先にマッピングする場合は、**タグ**構成で **サイトセクションにパスを使用**の切り替えを必ずオフにしてください。|
|カスタムセグメント A|カスタムセグメントのレポートで使用できる一意の値は、カスタムセグメント A、B、C の合計で最大 25 個に制限されています（`nol_segA + nol_segB + nol_segC <= 25`）。`nol_segA` キーで Nielsen に渡されます。|
|カスタムセグメント B|カスタムセグメントのレポートで使用できる一意の値は、カスタムセグメント A、B、C の合計で最大 25 個に制限されています（`nol_segA + nol_segB + nol_segC <= 25`）。`nol_segB` キーで Nielsen に渡されます。|
|カスタムセグメント C|カスタムセグメントのレポートで使用できる一意の値は、カスタムセグメント A、B、C の合計で最大 25 個に制限されています（`nol_segA + nol_segB + nol_segC <= 25`）。`nol_segC` キーで Nielsen に渡されます。|

## ベンダーのドキュメント

* [静的ページ測定 - 実装ガイド](https://engineeringforum.nielsen.com/sdk/developers/product-dcr-implementation-static-bsdk.php)
* [Static Lite ページ測定 - 実装ガイド](https://engineeringforum.nielsen.com/sdk/developers/product-dcr-implementation-static-lite-bsdk.php)