---
title: Sailthruコネクタ構成ガイド
description: この記事では、Sailthruコネクタの構成方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/sailthru-connector/
---
## コネクタアクション

| アクション名 | AudienceStream | EventStream |
| --- | :---: | :---: |
|リストにユーザーを追加| ✓| ✗|
|リストからユーザーを削除| ✓| ✗|
|リストにユーザーを追加（バッチジョブ）| ✓| ✗|
|リストからユーザーを削除（バッチジョブ）| ✓| ✗|
|トランザクションメールを送信| ✓| ✗|

## 構成の構成

コネクタマーケットプレイスに移動し、新しいコネクタを追加します。コネクタの追加方法の一般的な指示については、[コネクタ概要]()の記事を参照してください。

コネクタを追加した後、次の構成を構成します：

* **APIキー**
  * Sailthruアカウント機能にアクセスするためのAPIキー。

* **共有シークレット**
  * Sailthruアカウントの共有シークレット。

## アクション構成 - パラメータとオプション

**次へ**をクリックするか、**アクション**タブに移動します。ここでコネクタアクションを構成します。

このセクションでは、各アクションのパラメータとオプションの構成方法について説明します。

### アクション - リストにユーザーを追加

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|Sailthruリスト|  &lt;ul&gt;&lt;li&gt;ユーザーを追加するプライマリまたはセカンダリリスト。&lt;/li&gt;&lt;/ul&gt; |
|ユーザーFacebook ID|  &lt;ul&gt;&lt;li&gt;ユーザーFacebook IDにマッピング&lt;/li&gt;&lt;/ul&gt; |
|Sailthru Horizonクッキー|  &lt;ul&gt;&lt;li&gt;Sailthru Horizonクッキーにマッピング&lt;/li&gt;&lt;/ul&gt; |
|ユーザーSMS|  &lt;ul&gt;&lt;li&gt;ユーザーSMSにマッピング&lt;/li&gt;&lt;/ul&gt; |
|ユーザー指定識別子|  &lt;ul&gt;&lt;li&gt;ユーザー指定識別子にマッピング&lt;/li&gt;&lt;/ul&gt; |
|ユーザーEmail|  &lt;ul&gt;&lt;li&gt;ユーザーEmailにマッピング&lt;/li&gt;&lt;/ul&gt; |
|ユーザーTwitter名|  &lt;ul&gt;&lt;li&gt;ユーザーX名にマッピング&lt;/li&gt;&lt;/ul&gt; |
|Sailthru識別子|  &lt;ul&gt;&lt;li&gt;Sailthru識別子にマッピング&lt;/li&gt;&lt;/ul&gt; |

### アクション - リストからユーザーを削除

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|Sailthruリスト|  &lt;ul&gt;&lt;li&gt;ユーザーを削除するプライマリまたはセカンダリリスト。&lt;/li&gt;&lt;/ul&gt; |
|ユーザーFacebook ID|  &lt;ul&gt;&lt;li&gt;ユーザーFacebook IDにマッピング&lt;/li&gt;&lt;/ul&gt; |
|Sailthru Horizonクッキー|  &lt;ul&gt;&lt;li&gt;Sailthru Horizonクッキーにマッピング&lt;/li&gt;&lt;/ul&gt; |
|ユーザーSMS|  &lt;ul&gt;&lt;li&gt;ユーザーSMSにマッピング&lt;/li&gt;&lt;/ul&gt; |
|ユーザー指定識別子|  &lt;ul&gt;&lt;li&gt;ユーザー指定識別子にマッピング&lt;/li&gt;&lt;/ul&gt; |
|ユーザーEmail|  &lt;ul&gt;&lt;li&gt;ユーザーEmailにマッピング&lt;/li&gt;&lt;/ul&gt; |
|ユーザーTwitter名|  &lt;ul&gt;&lt;li&gt;ユーザーX名にマッピング&lt;/li&gt;&lt;/ul&gt; |
|Sailthru識別子|  &lt;ul&gt;&lt;li&gt;Sailthru識別子にマッピング&lt;/li&gt;&lt;/ul&gt; |

### アクション - リストにユーザーを追加（バッチジョブ）

##### バッチ制限

このアクションは、ベンダーへの大量のデータ転送をサポートするためにバッチリクエストを使用します。詳細については、[バッチアクション]()を参照してください。リクエストは、以下のいずれかの閾値が達成されるか、プロファイルが公開されるまでキューに入れられます：

* リクエストの最大数：10000
* 最古のリクエストからの最大時間：10分
* リクエストの最大サイズ：10MB

#### パラメータ

| **パラメータ**             | **説明**                                                                     |
| ------------------------- | ----------------------------------------------------------------------------------- |
| Sailthruリスト             | &lt;ul&gt;&lt;li&gt;ユーザーを追加するリストを1つ以上選択します。&lt;/li&gt;&lt;/ul&gt;                          |
| ユーザーFacebook ID          | &lt;ul&gt;&lt;li&gt;ユーザーFacebook IDにマッピング&lt;/li&gt;&lt;/ul&gt;                                           |
| Sailthru Horizonクッキー   | &lt;ul&gt;&lt;li&gt;Sailthru Horizonクッキーにマッピング&lt;/li&gt;&lt;/ul&gt;                                    |
| ユーザーSMS                  | &lt;ul&gt;&lt;li&gt;ユーザーSMSにマッピング&lt;/li&gt;&lt;/ul&gt;                                                   |
| ユーザー指定識別子 | &lt;ul&gt;&lt;li&gt;ユーザー指定識別子にマッピング&lt;/li&gt;&lt;/ul&gt;                                  |
| ユーザーEmail                | &lt;ul&gt;&lt;li&gt;ユーザーEmailにマッピング&lt;/li&gt;&lt;/ul&gt;                                                 |
| ユーザーTwitter名         | &lt;ul&gt;&lt;li&gt;ユーザーX名にマッピング&lt;/li&gt;&lt;/ul&gt;                                          |
| Sailthru識別子       | &lt;ul&gt;&lt;li&gt;Sailthru識別子にマッピング&lt;/li&gt;&lt;/ul&gt;                                        |
| ユーザーカスタム変数     | &lt;ul&gt;&lt;li&gt;ユーザーにカスタム変数を構成します。&lt;/li&gt;&lt;/ul&gt;                                 |
| Opt Out                   | &lt;ul&gt;&lt;li&gt;次のいずれかでなければなりません：`all`, `basic`, `blast`または`none`&lt;/li&gt;&lt;/ul&gt; |
| サインアップ日               | &lt;ul&gt;&lt;li&gt;ユーザーのサインアップ日。&lt;/li&gt;&lt;/ul&gt;                                                 |

### アクション - リストからユーザーを削除（バッチジョブ）

##### バッチ制限

このアクションは、ベンダーへの大量のデータ転送をサポートするためにバッチリクエストを使用します。詳細については、[バッチアクション]()を参照してください。リクエストは、以下のいずれかの閾値が達成されるか、プロファイルが公開されるまでキューに入れられます：

* リクエストの最大数：10000
* 最古のリクエストからの最大時間：10分
* リクエストの最大サイズ：10MB

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|Sailthruリスト|  &lt;ul&gt;&lt;li&gt;ユーザーを削除するリストを1つ以上選択します。&lt;/li&gt;&lt;/ul&gt; |
|ユーザーFacebook ID|  &lt;ul&gt;&lt;li&gt;ユーザーFacebook IDにマッピング&lt;/li&gt;&lt;/ul&gt; |
|Sailthru Horizonクッキー|  &lt;ul&gt;&lt;li&gt;Sailthru Horizonクッキーにマッピング&lt;/li&gt;&lt;/ul&gt; |
|ユーザーSMS|  &lt;ul&gt;&lt;li&gt;ユーザーSMSにマッピング&lt;/li&gt;&lt;/ul&gt; |
|ユーザー指定識別子|  &lt;ul&gt;&lt;li&gt;ユーザー指定識別子にマッピング&lt;/li&gt;&lt;/ul&gt; |
|ユーザーEmail|  &lt;ul&gt;&lt;li&gt;ユーザーEmailにマッピング&lt;/li&gt;&lt;/ul&gt; |
|ユーザーTwitter名|  &lt;ul&gt;&lt;li&gt;ユーザーX名にマッピング&lt;/li&gt;&lt;/ul&gt; |
|Sailthru識別子|  &lt;ul&gt;&lt;li&gt;Sailthru識別子にマッピング&lt;/li&gt;&lt;/ul&gt; |
|ユーザーカスタム変数|  &lt;ul&gt;&lt;li&gt;ユーザーにカスタム変数を構成します。&lt;/li&gt;&lt;/ul&gt; |
|Opt Out|  &lt;ul&gt;&lt;li&gt;次のいずれかでなければなりません：`all`, `basic`, `blast`または`none`&lt;/li&gt;&lt;/ul&gt; |
|サインアップ日|  &lt;ul&gt;&lt;li&gt;ユーザーのサインアップ日。&lt;/li&gt;&lt;/ul&gt; |

### アクション - トランザクションメールを送信

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|To|  &lt;ul&gt;&lt;li&gt;このメールを受け取るユーザーのメールアドレス&lt;/li&gt;&lt;/ul&gt; |
|メールテンプレート|  &lt;ul&gt;&lt;li&gt;ユーザーに送信するメール&lt;/li&gt;&lt;/ul&gt; |
|メール変数置換|  &lt;ul&gt;&lt;li&gt;提供されたメールテンプレートの変数をTealiumデータで置換します。&lt;/li&gt;&lt;li&gt;これにより、ユーザーに保存されている変数が上書きされます。&lt;/li&gt;&lt;li&gt;逆に、割り当てられていない変数はユーザーに保存されているものがデフォルトとなります。&lt;/li&gt;&lt;/ul&gt; |
|メールリスト置換|  &lt;ul&gt;&lt;li&gt;データレイヤーで配列タイプが必要です。&lt;/li&gt;&lt;li&gt;データは正しくフォーマットされて渡されます。&lt;/li&gt;&lt;li&gt;提供されたメールテンプレートのリスト変数をTealiumデータで置換します。&lt;/li&gt;&lt;li&gt;これにより、ユーザーに保存されている変数が上書きされます。&lt;/li&gt;&lt;li&gt;逆に、割り当てられていない変数はユーザーに保存されているものがデフォルトとなります。&lt;/li&gt;&lt;/ul&gt; |