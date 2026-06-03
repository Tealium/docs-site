---
title: Iterableコネクタ構成ガイド（廃止）
description: この記事では、Customer Data HubアカウントでIterableコネクタを構成する方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/iterable-connector-deprecated/
---
このコネクタは現在廃止され、タグマーケットプレイスでは利用できなくなりました。
現在のコネクタについては、[Iterableコネクタ構成ガイド]()を参照してください。

## コネクタのアクション

| アクション名 | AudienceStream | EventStream |
| --- | :---: | :---: |
|イベントの追跡| ✗| ✓|
|ユーザーの追加または更新| ✓| ✗|
|ユーザーをリストに登録| ✓| ✗|
|ユーザーをリストから解除| ✓| ✗|
|特定のメールアドレスにメールを送信| ✓| ✗|

## 構成の構成

コネクタマーケットプレイスに移動し、新しいコネクタを追加します。コネクタを追加する一般的な手順については、[コネクタ概要]()の記事を参照してください。

コネクタを追加した後、以下の構成を構成します：

* **APIキー**  
Iterableインターフェースの左側のナビゲーションメニューに移動し、**Integrations &amp;gt; API Keys**をクリックしてAPIキーを見つけます。

## アクション構成 - パラメータとオプション

**次へ**をクリックするか、**アクション**タブに移動します。ここでコネクタアクションを構成します。

このセクションでは、各アクションのパラメータとオプションの構成方法について説明します。

### アクション - イベントの追跡

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|メール|  &lt;ul&gt;&lt;li&gt;ユーザーを識別するためには、メールまたはuserIDのいずれかを渡す必要があります&lt;/li&gt;&lt;li&gt;両方が渡された場合、メールが優先されます&lt;/li&gt;&lt;li&gt;詳細情報については、以下のベンダードキュメンテーションを参照してください：&lt;ul&gt;&lt;li&gt;[イベントとイベントプロパティAPIドキュメンテーション](https://support.iterable.com/hc/en-us/articles/206430615-Events-and-Event-Properties)&lt;/li&gt;&lt;/ul&gt; &lt;/li&gt;&lt;/ul&gt; |
|イベント名|  &lt;ul&gt;&lt;li&gt;イベントの名前&lt;/li&gt;&lt;/ul&gt; |
|作成日時|  &lt;ul&gt;&lt;li&gt;イベントが発生した時間&lt;/li&gt;&lt;li&gt;指定されていない場合、イベントが受信された時間に構成されます&lt;/li&gt;&lt;li&gt;Unixタイムスタンプを期待します&lt;/li&gt;&lt;/ul&gt; |
|ユーザーID|  &lt;ul&gt;&lt;li&gt;`updateUser`コールに渡されたユーザーID&lt;/li&gt;&lt;/ul&gt; |
|キャンペーンID|  &lt;ul&gt;&lt;li&gt;コンバージョンに関連付けられたキャンペーン&lt;/li&gt;&lt;/ul&gt; |
|テンプレートID|  &lt;ul&gt;&lt;li&gt;テンプレートID&lt;/li&gt;&lt;/ul&gt; |
|データフィールド|  &lt;ul&gt;&lt;li&gt;イベントに関連付けられた追加データ、例：アイテムID、アイテム量、市、州など。&lt;/li&gt;&lt;/ul&gt; |

### アクション - ユーザーの追加または更新

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|メール|  &lt;ul&gt;&lt;li&gt;プロフィールにユーザーIDが構成されている場合を除き、メールを構成する必要があります&lt;/li&gt;&lt;li&gt;ユーザーIDが構成されたプロフィールがすでに存在する場合、ユーザーIDからメールへのルックアップが行われます&lt;/li&gt;&lt;li&gt;詳細情報については、以下のベンダードキュメンテーションを参照してください：&lt;ul&gt;&lt;li&gt;[Iterable APIドキュメンテーション](https://api.iterable.com/api/docs#!/users/updateUser)&lt;/li&gt;&lt;/ul&gt; &lt;/li&gt;&lt;/ul&gt; |
|ユーザーID|  &lt;ul&gt;&lt;li&gt;オプションのユーザーID&lt;/li&gt;&lt;li&gt;これは通常、データベースが生成するIDです&lt;/li&gt;&lt;/ul&gt; |
|データフィールド|  &lt;ul&gt;&lt;li&gt;ユーザープロフィールに保存するデータフィールド&lt;/li&gt;&lt;/ul&gt; |

### アクション - ユーザーをリストに登録

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|リストID|  &lt;ul&gt;&lt;li&gt;ユーザーを登録するリストのID&lt;/li&gt;&lt;li&gt;詳細情報については、以下のベンダードキュメンテーションを参照してください：&lt;ul&gt;&lt;li&gt;[Iterable APIドキュメンテーション](https://api.iterable.com/api/docs#!/lists/subscribe)&lt;/li&gt;&lt;li&gt;[API概要とサンプルペイロード](https://support.iterable.com/hc/en-us/articles/204780579-API-Overview-and-Sample-Payloads#lists).&lt;/li&gt;&lt;/ul&gt; &lt;/li&gt;&lt;/ul&gt; |
|メール|  &lt;ul&gt;&lt;li&gt;ユーザーのメールアドレス&lt;/li&gt;&lt;/ul&gt; |
|ユーザーID|  &lt;ul&gt;&lt;li&gt;ユーザーの一意のユーザーID&lt;/li&gt;&lt;/ul&gt; |
|データフィールド|  &lt;ul&gt;&lt;li&gt;ユーザープロフィールに保存するデータフィールド&lt;/li&gt;&lt;/ul&gt; |

### アクション - ユーザーをリストから解除

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|リストID|  &lt;ul&gt;&lt;li&gt;ユーザーを解除するリストのID&lt;/li&gt;&lt;li&gt;詳細情報については、以下のベンダードキュメンテーションを参照してください：&lt;ul&gt;&lt;li&gt;[Iterable APIドキュメンテーション](https://api.iterable.com/api/docs#!/lists/unsubscribe)&lt;/li&gt;&lt;/ul&gt; &lt;/li&gt;&lt;/ul&gt; |
|メール|  &lt;ul&gt;&lt;li&gt;ユーザーのメールアドレス&lt;/li&gt;&lt;/ul&gt; |
|キャンペーンID|  &lt;ul&gt;&lt;li&gt;キャンペーンに解除を属性付けする&lt;/li&gt;&lt;/ul&gt; |
|チャネル解除|  &lt;ul&gt;&lt;li&gt;リストの関連チャネルからメールを解除する&lt;/li&gt;&lt;li&gt;このパラメータは基本的にグローバルな解除です&lt;/li&gt;&lt;li&gt;可能な値：`true`または`false`&lt;/li&gt;&lt;li&gt;デフォルト値は`false`です&lt;/li&gt;&lt;/ul&gt; |

### アクション - 特定のメールアドレスにメールを送信

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|キャンペーンID|  &lt;ul&gt;&lt;li&gt;トリガーするキャンペーンのID&lt;/li&gt;&lt;/ul&gt; |
|受信者メール|  &lt;ul&gt;&lt;li&gt;受信者のメールアドレス&lt;/li&gt;&lt;/ul&gt; |
|データフィールド|  &lt;ul&gt;&lt;li&gt;メールテンプレートにマージするフィールド&lt;/li&gt;&lt;/ul&gt; |
|送信時刻|  &lt;ul&gt;&lt;li&gt;メッセージを最大365日先までスケジュールします。&lt;/li&gt;&lt;li&gt;過去に構成されているか、空白の場合、メールはすぐに送信されます。&lt;/li&gt;&lt;li&gt;形式はUTCで`YYYY-MM-DD HH:MM:SS`です。&lt;/li&gt;&lt;/ul&gt; |
