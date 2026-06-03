---
title: AIエージェントのためのドキュメント
description: AIエージェントおよび大規模言語モデルとともにTealiumのドキュメントの使用方法を学びます。
url: https://docs.tealium.com/ja/administration/resources/docs-for-agents/
---
Tealiumのドキュメントは、AIエージェントおよび大規模言語モデル（LLM）に最適化された形式で提供されています。標準的なHTMLページに加えて、すべてのドキュメントは構造化されたインデックスファイル（llms.txt）および個々のページのマークダウンバージョンとして利用可能です。

これらの形式はトークンの使用を減らし、解析の精度を向上させ、AIエージェントがTealiumのドキュメントを発見し処理するのを容易にします。

## llms.txt

`llms.txt`形式は、AIエージェントが確実に解析できる方法でドキュメントのセクションとページリンクをリストする構造化された、機械可読のインデックスです。Tealiumのドキュメントの発見と取得を改善し、完全なHTMLページをクローリングする場合と比較してトークンのオーバーヘッドを削減します。

### メインインデックス

メインのllms.txtファイルは、すべてのドキュメントエリアのトップレベルディレクトリです。各エリアを説明とそのセクションインデックスへのリンクとともにリストします。

* [/llms.txt](/ja/llms.txt)

### セクションインデックス

各ドキュメントエリアには、そのエリア内のページの完全なインデックスを含む独自のllms.txtファイルがあります：

* [タグ管理](/ja/iq-tag-management/llms.txt): クライアントサイドのタグ管理ドキュメント。
* [サーバーサイド](/ja/server-side/llms.txt): イベント、オーディエンス、機能、データソース、インサイトを含むサーバーサイドのドキュメント。
* [API](/ja/api/llms.txt): 開発者APIのドキュメントとリファレンスガイド。
* [Webインストール](/ja/platforms/web-install/llms.txt): JavaScriptライブラリとタグマネージャー統合を含むWebプラットフォームのインストールガイド。
* [モバイルインストール](/ja/platforms/mobile-install/llms.txt): iOS SDK、Android SDK、クロスプラットフォームフレームワークを含むモバイルプラットフォームのインストールガイド。
* [クライアントサイドタグ](/ja/client-side-tags/llms.txt): 個々のクライアントサイドタグとベンダー統合のドキュメント。
* [サーバーサイドコネクタ](/ja/server-side-connectors/llms.txt): 個々のサーバーサイドコネクタとベンダー統合のドキュメント。
* [管理](/ja/administration/llms.txt): ユーザーアクセス、権限、セキュリティ構成を含むプラットフォーム管理。
* [同意](/ja/consent/llms.txt): クライアントサイドおよびサーバーサイド環境での同意の取得、解釈、および施行。
* [ガイド](/ja/guides/llms.txt): Tealiumを効果的に使用するための実用的なガイドと戦略。
* [予測](/ja/predict/llms.txt): 機械学習によるオーディエンス予測のためのPredict MLドキュメント。
* [パートナーと業界](/ja/partners-and-industries/llms.txt): 業界特有の統合とパートナーシップのドキュメント。

## マークダウン

すべてのドキュメントページはマークダウンファイルとして利用可能です。これらのファイルは、HTMLマークアップやその他のサイト固有の構文を含まないページ内容を含んでいます。

マークダウンバージョンは、AIエージェントの処理に対してHTMLに比べていくつかの利点を提供します：

* トークンが少ない: プレーンなマークダウンはHTMLよりもコンパクトです。
* 明確な構造: 見出し、リスト、コードブロックが明確です。
* より良い解析: タグを削除する必要がなく、レンダリングのアーティファクトを扱う必要がありません。
* 一貫したフォーマット: すべてのページが同じマークダウン規約に従います。

### マークダウンバージョンへのアクセス

任意のドキュメントページのマークダウンバージョンにアクセスするには、ページのURLに`/index.md`を追加します。

例：

* HTMLバージョン: [/iq-tag-management/getting-started/what-is-tealium-iq/](/ja/iq-tag-management/getting-started/what-is-tealium-iq/)
* マークダウンバージョン: [/iq-tag-management/getting-started/what-is-tealium-iq/index.md](/ja/iq-tag-management/getting-started/what-is-tealium-iq/index.md)

## 言語サポート

すべてのllms.txtインデックスとマークダウンページは英語と日本語で利用可能です。

llms.txtインデックスの場合：

* 英語メインインデックス: [/llms.txt](/ja/llms.txt)
* 日本語メインインデックス: [/ja/llms.txt](/ja/llms.txt)

セクションインデックスは同じパターンに従います：

* 英語: `/{area}/llms.txt`
* 日本語: `/ja/{area}/llms.txt`

マークダウンページの場合：

* 英語: `/{path}/index.md`
* 日本語: `/ja/{path}/index.md`