---
title: Optimizely 非同期タグ構成ガイド
description: Tealium のベストプラクティスは、すべてのタグを非同期で読み込むことです。この記事では、Optimizely を実装する際に Tealium のベストプラクティスに従う方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/optimizely-asynchronous-tag/
---
<blockquote>
Optimizely を同期的に実装するためのオプションについては、こちらの[記事](https://docs.tealium.com/optimizely-synchronous-implementation/)を参照してください。
</blockquote>


Optimizely 非同期タグを実装する方法は2つあります。どちらの方法を使用するかは、サイトのコンテンツとテスト要件によって決まります。この記事に記載されている順に、2つの方法を試すことをお勧めします。

**注:** どちらの方法も、`utag.js` ファイルがページ上で非同期にコーディングされていることを前提としています。

## 方法1（推奨）: Optimizely 非同期タグをバンドルしてすべてのページで読み込む

この方法では、タグがページ内の他の要素の読み込みをブロックしないため、推奨しています。

### 手順1: すべてのページで読み込むタグのバンドル機能を有効にする

1. 管理メニューで、**Configure Publish Settings**をクリックします。**Publish Configuration**ダイアログが表示されます。
1. **Bundle Tags Loading On All Pages**トグルを**オン**にします。これによりタグが `utag.js` とバンドルされ、ブラウザーによるネットワーク呼び出しの回数が削減されます。

### 手順2: Optimizely 非同期タグを追加して構成する

タグマーケットプレイスに移動し、新しいタグを追加します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

構成手順は次のとおりです。

1. プロジェクトIDを入力します。これは、Optimizely から提供されるスクリプトタグの末尾にある番号です。  
 例: `<script src="//cdn.optimizely.com/js/123456789.js"></script>`
1. **Advanced Settings**リストから、**Wait Flag = No**を選択します。  
1. **Load Rules**タブに進み、デフォルトの**Load on All Pages**ルールを選択します。  
1. **Data Mappings**タブに進み、データの送信先をマッピングします。データソースをタグの送信先にマッピングする方法については、[データマッピング](https://docs.tealium.com/about-data-mappings/)を参照してください。  


<blockquote>
非同期タグを使用してEコマースデータをトラッキングする場合は、[Eコマース拡張機能](https://docs.tealium.com/e-commerce-extension/)を使用して、そのデータを自動的にマッピングすることをお勧めします。
</blockquote>


| 送信先名 | 送信先変数 | 説明 | Eコマース拡張機能のマッピング（推奨） |
|:-----------------|:---------------------|:--------------------------------------------------------------|:-----------------------------------------------|
| プロジェクトID | `projectId` | Optimizely によって提供されるプロジェクト識別子 | 該当なし |
| 注文ID | `orderId` | 注文に割り当てられた一意の識別子 | `_corder` 変数がこの送信先にマッピングされます |
| 収益（セント単位） | `revenue` | 注文の小計金額（セント単位） | `_csubtotal` 変数がこの送信先にマッピングされます |
| イベント名 | `eventName` | コンバージョンイベントの名前／タイプ<br> デフォルトイベントは `purchase` です | 該当なし |

### 手順3: プロファイルを保存／パブリッシュする

**重要**: 非同期タグをできるだけ早く実行するには、`utag.js` ファイルをページ内のできるだけ上部に配置してください。utag.js は、HTML の &lt;body&gt; タグの先頭に配置することをお勧めします。Tealium が Optimizely の JavaScript ファイルを読み込み、残りの処理を行います。

## 方法2: Optimizely をブロッキングタグとして実行する

Optimizely は通常、ページ上で同期的に動作することを推奨しています。これにより「より早く」実行し、他のツール（Analytics ツールなど）が動作する前にテストを決定できるためです。ただし、Optimizely を十分早く、なおかつ非同期で実行する唯一の方法は、その `.js` ライブラリを別の場所から配信することです。この場合、Optimizely 非同期タグはブロッキングタグとなり、後続の非同期スクリプト（`utag.10.js` など）は、[ブロッキングタグ](https://docs.tealium.com/manage-templates/)の処理が完了するまで読み込まれません。


<blockquote>
最新バージョンをまだ使用していない場合は、`utag.js` のバージョンをアップグレードしてください。詳細については、[utag.js リリースノート](https://docs.tealium.com/ja/release-notes/?filter=tealium-universal-tag)を参照してください。
</blockquote>


1. 上記の手順2を繰り返し、Optimizely 非同期タグを追加して構成します。
1. **Advanced Settings**を展開し、**Custom Script Source**フィールドに `.js` ライブラリの場所を入力します。
1. プロファイルを**保存／パブリッシュ**します。

以上です。違いはわずかですが、これによって Optimizely ファイルの読み込み方法と、Optimizely の後に他のタグが読み込まれる方法が大きく変わります。