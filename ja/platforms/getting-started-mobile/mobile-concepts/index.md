---
title: モバイルの概念
description: モバイルソリューションの基本について説明します。
url: https://docs.tealium.com/ja/platforms/getting-started-mobile/mobile-concepts/
---
## Tealium Collect（推奨）

Tealium Collect は、モバイルアプリから Tealium Customer Data Hub にユーザーイベントを送信する軽量なデータ収集モジュールです。Tealium Collect モジュールを使用すると、サードパーティベンダーをインストール済み SDK としてではなく、サーバーサイドコネクタとして統合できます。

Tealium Collect は、[イベントのバッチ処理](https://docs.tealium.com/ja/platforms/getting-started-mobile/event-batching/)やその他の省電力技術を使用し、モバイルアプリケーションに次の利点をもたらします。

- アプリのサイズとメモリ使用量の削減
- ネットワークトラフィックの最適化
- バッテリー使用量の最小化

[サーバーサイド](https://docs.tealium.com/ja/platforms/getting-started-mobile/server-side/)でのデータ送信について詳しく説明します。

## タグ管理

タグ管理は、モバイルアプリ内でタグ管理を利用できるようにするモジュールです。このクライアントサイドソリューションは、非表示の WebView を使用して、標準的な Web ベースのベンダータグをアプリ内で実行します。サーバーサイド API をサポートしていないサードパーティベンダーとの統合には、タグ管理モジュールを使用します。

タグ管理モジュールには、次の利点があります。

- [タグ管理拡張機能](https://docs.tealium.com/about-extensions/)を使用した高度なデータレイヤーのカスタマイズ。
- [Tealium Collect タグ](https://docs.tealium.com/tealium-collect-tag/)を使用したクライアントサイドとサーバーサイドのサポート。


<blockquote>
Tealium Collect モジュールと Tealium Collect タグ（タグ管理モジュール経由）を併用するとトラッキングが重複するため、併用しないでください。
</blockquote>


[クライアントサイド](https://docs.tealium.com/ja/platforms/getting-started-mobile/client-side/)ソリューションについて詳しく説明します。

## データレイヤー

データレイヤーは、デジタルプロパティでトラッキングするアクティビティを、ベンダーに依存しない使いやすい形式で表現したものです。各プラットフォームのインストール環境で提供される標準の組み込みデータレイヤー変数に加えて、アプリから取得した動的な値をカスタムデータレイヤー変数に構成します。

モバイルで使用できる[データレイヤー変数](https://docs.tealium.com/ja/platforms/getting-started-mobile/data-layer/)について詳しく説明します。

## リモートコマンド

リモートコマンドは、ネイティブアプリ内の機能をトリガーするためのクライアントサイドソリューションです。カスタムのネイティブ機能やサードパーティ SDK との統合には、リモートコマンドを使用します。リモートコマンドは、JSON ファイルまたはタグ管理のリモートコマンドタグを使用して構成します。

[リモートコマンド](https://docs.tealium.com/ja/platforms/remote-commands/)について詳しく説明します。

## ライフサイクルトラッキング

各プラットフォームには固有のライフサイクルモジュールがあり、アプリのライフサイクルイベント（起動、復帰、休止）と関連データを自動的にトラッキングできます。

## モバイルプロファイル

タグ管理モジュールを使用するアプリには、モバイル用に有効化された対応するプロファイルがタグ管理に必要です。モバイルプロファイルには、組み込みのモバイルデータレイヤー変数と、アプリのアップデートをデプロイせずに調整できる Tealium SDK の追加構成が含まれます。

[モバイルプロファイルの作成](https://docs.tealium.com/create-mobile-profile/)について詳しく説明します。

## データ管理

一部のデータレイヤー変数は、アプリのライフサイクル全体を通じて一貫した状態に保つ必要があります。トラッキング呼び出しのたびにこれらの変数を含める代わりに、いずれかの保存ソリューションを使用して、変更頻度の低いデータレイヤー変数を構成します。

### 永続保存

永続保存に追加されたデータレイヤー変数は、ユーザーがアプリをアンインストールするか、アプリのデータを手動で消去するまで保持されます。各永続データ変数は、すべてのトラッキングに自動的に含まれます。

### 揮発性保存

揮発性保存に追加されたデータレイヤー変数は、強制終了や再起動などによってアプリがメモリから消去されるまで保持されます。各揮発性データ変数は、すべてのトラッキング呼び出しに自動的に含まれます。揮発性データはディスクに保存されないため、デバイス上のアプリのディスク使用量には影響しません。

### ライブラリの移行

古いライブラリ（Java、Objective-C、または Swift 1.x）から新しいライブラリ（Kotlin または Swift 2.x）にアップグレードすると、永続データは自動的に移行されます。移行されるデータには、ユーザーの同意構成、ライフサイクルデータ、Tealium Visitor ID が含まれます。

最新の [Tealium for Kotlin](https://docs.tealium.com/ja/platforms/android-kotlin/data-layer/) および [Tealium for Swift](https://docs.tealium.com/ja/platforms/ios-swift/data-layer/) ライブラリについて詳しく説明します。