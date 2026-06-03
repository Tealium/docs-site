---
title: Moceanコネクタ構成ガイド
description: この記事では、Moceanコネクタの構成方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/mocean-connector/
---
## コネクタのアクション

| アクション名 | AudienceStream | EventStream |
| --- | :---: | :---: |
|SMSを送信| ✓| ✗|

## 構成を構成する

コネクタマーケットプレイスに移動し、新しいコネクタを追加します。コネクタを追加する一般的な手順については、[コネクタ概要]()の記事を参照してください。

コネクタを追加した後、次の構成を構成します：

* **APIキー**：あなたのアカウントのAPIキー。詳細については、次を参照してください：[Mocean認証](https://moceanapi.com/docs/?shell#authentication&amp;quot;&amp;gt;https://moceanapi.com/docs/?shell#authentication)
* **APIシークレット**：あなたのアカウントのAPIシークレット。

## アクション構成 - パラメータとオプション

**次へ**をクリックするか、**アクション**タブに移動します。ここでコネクタのアクションを構成します。

このセクションでは、各アクションのパラメータとオプションの構成方法について説明します。

### アクション - SMSを送信

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|From|  &lt;ul&gt;&lt;li&gt;SMS送信者ID（SMS送信者名とも呼ばれます）は、メッセージがモバイルデバイスで受信されたときに、受信者に表示される情報です。&lt;/li&gt;&lt;li&gt;詳細については、次を参照してください：[Moceanのドキュメンテーション](https://moceanapi.com/docs/?shell#sms-api)&lt;/li&gt;&lt;/ul&gt; |
|To|  &lt;ul&gt;&lt;li&gt;受信者の電話番号。&lt;/li&gt;&lt;li&gt;複数の受信者に送信する場合は、各エントリをスペース（‘ ’）またはカンマ（`,`）で区切ります。&lt;/li&gt;&lt;li&gt;電話番号には国コードを含める必要があります。例えば、マレーシアの電話番号は`60123456789`となります。&lt;/li&gt;&lt;/ul&gt; |
|Text|  &lt;ul&gt;&lt;li&gt;メッセージの内容。&lt;/li&gt;&lt;li&gt;バイナリコンテンツを送信する場合、これは16進数の文字列になります。&lt;/li&gt;&lt;/ul&gt; |
|User Data Header|  &lt;ul&gt;&lt;li&gt;メッセージのユーザーデータヘッダ部分。例えば、`0605040B8423F0`。&lt;/li&gt;&lt;/ul&gt; |
|Coding|  &lt;ul&gt;&lt;li&gt;DCSフィールドの符号化スキームビットを構成します。&lt;/li&gt;&lt;li&gt;次の値を受け入れます：  &lt;ul&gt;&lt;li&gt;`1`は7ビット用&lt;/li&gt;&lt;li&gt;`2`は8ビット用&lt;/li&gt;&lt;li&gt;`3`はUCS2用&lt;/li&gt;&lt;/ul&gt; &lt;/li&gt;&lt;/ul&gt; &lt;ul&gt;&lt;li&gt;未構成の場合、値はデフォルトで7ビットになります。ただし、`mocean-udh`が定義されている場合は、符号化が8ビットに構成されます。&lt;/li&gt;&lt;li&gt;文字セットが構成されていない場合、または非GSM文字が検出されたときにUTF-8に構成されていない場合、符号化はUCS2に構成されます。&lt;/li&gt;&lt;/ul&gt; |
|Delivery Report|  &lt;ul&gt;&lt;li&gt;送信されたメッセージの状態を含む配信レポートを要求します。&lt;/li&gt;&lt;li&gt;配信レポートを有効にするには、この値を`1`に構成します。&lt;/li&gt;&lt;li&gt;このフィールドが指定されていない場合、デフォルト値は‘ ’となり、DLRは返されません。&lt;/li&gt;&lt;/ul&gt; |
|Delivery Report URL|  &lt;ul&gt;&lt;li&gt;配信レポートを受信するURL。&lt;/li&gt;&lt;li&gt;DLRが要求された場合は必須です。&lt;/li&gt;&lt;/ul&gt; |
|Schedule|  &lt;ul&gt;&lt;li&gt;このフィールドを使用すると、メッセージは指定された日時に送信されます（大量のSMSがスケジューリングのためにキューに入れられているため、ベストエフォートベースです）。&lt;/li&gt;&lt;li&gt;日時の形式は`YYYY-MM-DD hh:mm:ss`で、24時間形式です。例：`2007-02-11 23:30:00`&lt;/li&gt;&lt;li&gt;日付形式が間違っていると、ゲートウェイがリクエストを拒否します。スケジュールされたSMSリクエストを作成する際は、マレーシア時間（またはGMT &#43;8:00）を使用してください。 &lt;/li&gt;&lt;/ul&gt; |
|Charset|  &lt;ul&gt;&lt;li&gt;Textパラメータで使用される文字セットを示します。&lt;/li&gt;&lt;li&gt;サポートされている文字セットは次のとおりです：  &lt;ul&gt;&lt;li&gt;ISO 8859-1&lt;/li&gt;&lt;li&gt;ISO 8859-7&lt;/li&gt;&lt;li&gt;UTF-8&lt;/li&gt;&lt;li&gt;Windows-1252&lt;/li&gt;&lt;/ul&gt; &lt;/li&gt;&lt;/ul&gt; |
|Validity|  &lt;ul&gt;&lt;li&gt;メッセージの有効期間を定義します。&lt;/li&gt;&lt;li&gt;ユーザーは有効期間を秒単位で入力する必要があります。&lt;/li&gt;&lt;li&gt;例えば、ユーザーがメッセージを送信後5分で期限切れにしたい場合、有効期間の値を300（秒）に構成する必要があります。&lt;/li&gt;&lt;/ul&gt; |
