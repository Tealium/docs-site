---
title: Twitterキャンペーンコネクタ構成ガイド
description: この記事では、Twitterキャンペーンコネクタの構成方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/twitter-campaigns-connector/
---
## コネクタアクション

| アクション名 | AudienceStream | EventStream |
| --- | :---: | :---: |
|ラインアイテムにターゲティング基準を追加| ✓| ✗|
|ラインアイテムからターゲティング基準を削除| ✓| ✗|

## 構成の構成

コネクタマーケットプレイスに移動し、新しいコネクタを追加します。コネクタを追加する一般的な手順については、[コネクタ概要]()の記事を参照してください。

コネクタを追加した後、以下の構成を構成します：

* **広告アカウントID**
  * 必須。
  * Twitterの広告アカウントIDを提供します。
  * アカウントIDは、ログインした状態でのアカウントのURLにあります。
  * 例：URLが`https://ads.twitter.com/accounts/1234abcd/`の場合、アカウントIDは`1234abcd`です。

## アクション構成 - パラメータとオプション

**次へ**をクリックするか、**アクション**タブに移動します。ここでコネクタアクションを構成します。

このセクションでは、各アクションのパラメータとオプションの構成方法について説明します。

### アクション - ラインアイテムにターゲティング基準を追加

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|ラインアイテム|  &lt;ul&gt;&lt;li&gt;必須&lt;/li&gt;&lt;li&gt;更新するラインアイテム。&lt;/li&gt;&lt;/ul&gt; |
|広範囲キーワード|  &lt;ul&gt;&lt;li&gt;広範囲キーワード&lt;/li&gt;&lt;/ul&gt; |
|正確なキーワード|  &lt;ul&gt;&lt;li&gt;正確なキーワード&lt;/li&gt;&lt;/ul&gt; |
|ユーザーのフォロワー|  &lt;ul&gt;&lt;li&gt;ユーザーのフォロワー&lt;/li&gt;&lt;/ul&gt; |
|興味|  &lt;ul&gt;&lt;li&gt;興味&lt;/li&gt;&lt;/ul&gt; |
|ネガティブな正確なキーワード|  &lt;ul&gt;&lt;li&gt;ネガティブな正確なキーワード&lt;/li&gt;&lt;/ul&gt; |
|ネガティブキーワード|  &lt;ul&gt;&lt;li&gt;ネガティブキーワード&lt;/li&gt;&lt;/ul&gt; |
|ネガティブフレーズキーワード|  &lt;ul&gt;&lt;li&gt;ネガティブフレーズキーワード&lt;/li&gt;&lt;/ul&gt; |
|フレーズキーワード|  &lt;ul&gt;&lt;li&gt;フレーズキーワード&lt;/li&gt;&lt;/ul&gt; |
|ユーザーのフォロワーに似ている|  &lt;ul&gt;&lt;li&gt;ユーザーのフォロワーに似ている&lt;/li&gt;&lt;/ul&gt; |

### アクション - ラインアイテムからターゲティング基準を削除

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|ラインアイテム|  &lt;ul&gt;&lt;li&gt;必須。&lt;/li&gt;&lt;li&gt;更新するラインアイテム。&lt;/li&gt;&lt;/ul&gt; |
|ターゲティング基準|  &lt;ul&gt;&lt;li&gt;必須。&lt;/li&gt;&lt;li&gt;ラインアイテムから削除するターゲティング基準。&lt;/li&gt;&lt;/ul&gt; |
