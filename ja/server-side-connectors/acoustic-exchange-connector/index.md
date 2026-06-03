---
title: Acoustic Exchangeコネクタ構成ガイド
url: https://docs.tealium.com/ja/server-side-connectors/acoustic-exchange-connector/
---## 要件

* アコースティックエクスチェンジアカウント
* Tealiumイベントエンドポイント認証キー

## コネクタアクション

| アクション名 | AudienceStream | EventStream |
| --- | :---: | :---: |
|カート放棄イベントの公開| ✓| ✗|
|カート購入イベントの公開| ✓| ✓|
|イベントの公開| ✓| ✓|

## 構成の構成

**コネクタマーケットプレイス**に移動し、新しいコネクタを追加します。コネクタの追加方法の一般的な指示については、[コネクタ概要]()の記事を参照してください。

コネクタを追加した後、以下の構成を構成します：

* **エンドポイント認証キー**
  * 必須
  * エンドポイント認証キーを入力します。
  * 詳細については、[エンドポイント概要](https://help.goacoustic.com/hc/en-us/articles/360043302213-Endpoints-overview)を参照してください。

## アクション構成 - パラメータとオプション

**次へ**をクリックするか、**アクション**タブに移動します。ここでコネクタアクションを構成します。

このセクションでは、各アクションのパラメータとオプションの構成方法について説明します。

### アクション: カート放棄イベントの公開

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|チャネル|  &lt;ul&gt;&lt;li&gt;必須&lt;/li&gt;&lt;li&gt;イベントが観察されたチャネルを選択します。&lt;/li&gt;&lt;li&gt;詳細については、[イベントカタログ](https://developer.goacoustic.com/acoustic-exchange/docs/acoustic-exchange-event-catalog)を参照してください。&lt;/li&gt;&lt;/ul&gt; |
|サブチャネル|  &lt;ul&gt;&lt;li&gt;推奨&lt;/li&gt;&lt;li&gt;イベントが観察された場所をさらに分類するためのサブチャネルを選択します。&lt;/li&gt;&lt;li&gt;選択したチャネルに適切な事前定義されたサブチャネルがない場合は、カスタム値として手動で入力するか、空白のままにします。&lt;/li&gt;&lt;/ul&gt; |

### アクション: カート購入イベントの公開

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|チャネル|  &lt;ul&gt;&lt;li&gt;必須&lt;/li&gt;&lt;li&gt;イベントが観察されたチャネルを選択します。&lt;/li&gt;&lt;li&gt;詳細については、[イベントカタログ](https://developer.goacoustic.com/acoustic-exchange/docs/acoustic-exchange-event-catalog)を参照してください。&lt;/li&gt;&lt;/ul&gt; |
|サブチャネル|  &lt;ul&gt;&lt;li&gt;推奨&lt;/li&gt;&lt;li&gt;イベントが観察された場所をさらに分類するためのサブチャネルを選択します。&lt;/li&gt;&lt;li&gt;選択したチャネルに適切な事前定義されたサブチャネルがない場合は、カスタム値として手動で入力するか、空白のままにします。&lt;/li&gt;&lt;/ul&gt; |

### アクション: イベントの公開

##### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|イベントタイプ|  &lt;ul&gt;&lt;li&gt;必須: イベントタイプを選択します。&lt;/li&gt;&lt;li&gt;詳細と利用可能なイベントのリストについては、[ダイナミックイベントライブラリ](https://exchange-us-1.goacoustic.com/#/taxonomy)を参照してください。&lt;/li&gt;&lt;/ul&gt; |
|チャネル|  &lt;ul&gt;&lt;li&gt;必須&lt;/li&gt;&lt;li&gt;イベントが観察されたチャネルを選択します。&lt;/li&gt;&lt;li&gt;詳細については、[イベントカタログ](https://developer.goacoustic.com/acoustic-exchange/docs/acoustic-exchange-event-catalog)を参照してください。&lt;/li&gt;&lt;/ul&gt; |
|サブチャネル|  &lt;ul&gt;&lt;li&gt;推奨&lt;/li&gt;&lt;li&gt;イベントが観察された場所をさらに分類するためのサブチャネルを選択します。&lt;/li&gt;&lt;li&gt;選択したチャネルに適切な事前定義されたサブチャネルがない場合は、カスタム値として手動で入力するか、空白のままにします。&lt;/li&gt;&lt;/ul&gt; |

