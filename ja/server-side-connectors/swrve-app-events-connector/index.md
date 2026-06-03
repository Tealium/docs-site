---
title: Swrveアプリイベントコネクタ構成ガイド
description: この記事では、Swrveコネクタの構成方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/swrve-app-events-connector/
---
## コネクタアクション

| アクション名 | AudienceStream | EventStream |
| --- | :---: | :---: |
|イベントを送信| ✓| ✓|
|ユーザーを更新| ✓| ✓|

## 構成の構成

コネクタマーケットプレイスに移動し、新しいコネクタを追加します。コネクタを追加する一般的な手順については、[コネクタ概要]()の記事を参照してください。

コネクタを追加した後、以下の構成を構成します：

* **アプリケーションID**
  * 必須。
  * Swrveアプリケーションの**統合構成**画面で表示できます。

* **APIキータイプ**
  * 必須。
  * 適用可能なAPIキータイプを選択します。
  * 詳細については、次を参照してください：[APIキーの管理](https://docs.swrve.com/getting-started/integrate-your-app/#Managing_your_API_keys)。

* **APIキー**
  * 必須。
  * APIキーの値を提供します。

* **リージョン**
  * 必須。
  * 適用可能なデータセンターリージョンを選択します。

## アクション構成 - パラメータとオプション

**次へ**をクリックするか、**アクション**タブに移動します。ここでコネクタアクションを構成します。

このセクションでは、各アクションのパラメータとオプションの構成方法について説明します。

### アクション - イベントを送信

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|ユーザーID|  &lt;ul&gt;&lt;li&gt;必須&lt;/li&gt;&lt;li&gt;イベントが関連するユニークなユーザー識別子。&lt;/li&gt;&lt;/ul&gt; |
|イベント名|  &lt;ul&gt;&lt;li&gt;必須&lt;/li&gt;&lt;li&gt;文字列&lt;/li&gt;&lt;li&gt;イベントの名前。&lt;/li&gt;&lt;li&gt;例：`app_started`&lt;/li&gt;&lt;li&gt;名前はドット表記を使用して階層を示すことができます。&lt;/li&gt;&lt;li&gt;名前は文字、数字、ダッシュ、アンダースコア、ドットのみを含む必要があります。&lt;/li&gt;&lt;li&gt;最初の有効な文字列がイベント名として取られます。&lt;/li&gt;&lt;li&gt;例えば、名前**level.start/**が提供された場合、それは`level.start`と解釈されます。&lt;/li&gt;&lt;/ul&gt; |
|アプリバージョン|  &lt;ul&gt;&lt;li&gt;ユーザーが現在使用しているアプリケーションのバージョン。&lt;/li&gt;&lt;/ul&gt; |
|カスタムペイロード|  &lt;ul&gt;&lt;li&gt;属性をカスタムペイロードのペアにマッピングします。&lt;/li&gt;&lt;li&gt;詳細については、次を参照してください：[カスタムペイロードガイド](https://docs.swrve.com/swrves-apis/api-guides/events-api-payloads-guide/)。&lt;/li&gt;&lt;/ul&gt; |

### アクション - ユーザーを更新

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|ユーザーID|  &lt;ul&gt;&lt;li&gt;必須&lt;/li&gt;&lt;li&gt;イベントが関連するユニークなユーザー識別子。&lt;/li&gt;&lt;/ul&gt; |
|ユーザーが開始|  &lt;ul&gt;&lt;li&gt;`false`と指定された場合、イベントは一部のパフォーマンス指標にはカウントされません。&lt;/li&gt;&lt;li&gt;プロパティが他の値を持つか指定されていない場合、イベントは通常どおりすべてのパフォーマンス指標にカウントされます。&lt;/li&gt;&lt;/ul&gt; |
|アプリバージョン|  &lt;ul&gt;&lt;li&gt;ユーザーが現在使用しているアプリケーションのバージョン。&lt;/li&gt;&lt;/ul&gt; |
|カスタムペイロード|  &lt;ul&gt;&lt;li&gt;属性をカスタムペイロードのペアにマッピングします。&lt;/li&gt;&lt;li&gt;詳細については、次を参照してください：[カスタムペイロードガイド](https://docs.swrve.com/swrves-apis/api-guides/events-api-payloads-guide/)。&lt;/li&gt;&lt;/ul&gt; |
