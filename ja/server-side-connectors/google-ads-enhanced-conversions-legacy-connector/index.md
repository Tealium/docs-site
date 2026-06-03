---
title: Google Ads Enhanced Conversions - レガシーコネクタ構成ガイド
description: この記事では、Google Ads Enhanced Conversions - レガシーコネクタの構成方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/google-ads-enhanced-conversions-legacy-connector/
---
## コネクタのアクション

| アクション名 | AudienceStream | EventStream |
| --- | :---: | :---: |
|コンバージョンの送信| ✓| ✓|

このコネクタは現在非推奨となっており、アプリの増分性研究を実行している場合のみ使用してください。現在のコネクタについては、[Google Ads Enhanced Conversions for Web connector](/ja/server-side-connectors/google-ads-enhanced-conversions-for-web-connector/)を参照してください。

## API情報

このコネクタは以下のベンダーAPIを使用します：

* API名：Google Enhanced Conversion API
* APIバージョン：v1
* APIエンドポイント：`https://www.google.com/ads/event/api/`

## 構成の構成

コネクタマーケットプレイスに移動し、新しいコネクタを追加します。コネクタの追加方法の一般的な指示については、[About Connectors](/ja/server-side/connectors/manage/)の記事を参照してください。

コネクタを追加した後、以下の構成を構成します：

## アクション構成 — パラメータとオプション

**次へ**をクリックするか、**アクション**タブに移動します。ここでコネクタアクションを構成します。

このセクションでは、各アクションのパラメータとオプションの構成方法について説明します。

### アクション - コンバージョンの送信

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|コンバージョン追跡ID|  &lt;ul&gt;&lt;li&gt;必須&lt;/li&gt;&lt;li&gt;`AW-123456789`からの数値で、広告主アカウントを一意に識別します。マップされた値から`AW-`を省略します。&lt;/li&gt;&lt;/ul&gt; |
|コンバージョンラベル|  &lt;ul&gt;&lt;li&gt;エンコードされたコンバージョン追跡IDとコンバージョンタイプ。&lt;/li&gt;&lt;/ul&gt; |
|コンバージョンタイプ|  &lt;ul&gt;&lt;li&gt;コンバージョンのタイプ。&lt;/li&gt;&lt;li&gt;広告主としてラベルにアクセスできない場合にのみ使用されます。&lt;/li&gt;&lt;/ul&gt; |
|コンバージョン値|  &lt;ul&gt;&lt;li&gt;広告主にとってのコンバージョンの金額。&lt;/li&gt;&lt;li&gt;デフォルト値は`$1 (USD)`&lt;/li&gt;&lt;/ul&gt; |
|通貨コード|  &lt;ul&gt;&lt;li&gt;コンバージョン値に関連する通貨。&lt;/li&gt;&lt;li&gt;これはISO 4217の3文字の通貨コードです。&lt;/li&gt;&lt;li&gt;デフォルト値は`USD`。&lt;/li&gt;&lt;li&gt;例：`USD`、`EUR`&lt;/li&gt;&lt;/ul&gt; |
|コンバージョン時間|  &lt;ul&gt;&lt;li&gt;エポックからのUnix時間、マイクロ秒単位。&lt;/li&gt;&lt;li&gt;デフォルト値は`now`。&lt;/li&gt;&lt;/ul&gt; |
|トランザクションID|  &lt;ul&gt;&lt;li&gt;必須&lt;/li&gt;&lt;li&gt;広告主として生成された、コンバージョンイベントを一意に識別するID。&lt;/li&gt;&lt;/ul&gt; |
|Google Click ID|  &lt;ul&gt;&lt;li&gt;利用可能な場合、ユーザーコンバージョンにつながるGoogle Click ID（`gclid`）。&lt;/li&gt;&lt;/ul&gt; |
|ユーザーエージェント|  &lt;ul&gt;&lt;li&gt;広告主がデータを保持している場合、コンバージョンしたユーザーのユーザーエージェント。&lt;/li&gt;&lt;/ul&gt; |
|メール|  &lt;ul&gt;&lt;li&gt;コンバージョン時点のユーザーメール。&lt;/li&gt;&lt;li&gt;複数のメール、電話番号、住所を追加するために配列タイプの属性を使用します。&lt;/li&gt;&lt;li&gt;以下のいずれかを提供する必要があります：  &lt;ul&gt;&lt;li&gt;ユーザーメール&lt;/li&gt;&lt;li&gt;ユーザーのフルネームと住所&lt;/li&gt;&lt;/ul&gt; &lt;/li&gt;&lt;/ul&gt; |
|電話番号|  &lt;ul&gt;&lt;li&gt;電話はメールまたはフルネームと住所と一緒に提供することができます。&lt;/li&gt;&lt;li&gt;複数のメール、電話番号、住所を追加するために配列タイプの属性を使用します。&lt;/li&gt;&lt;li&gt;コンバージョン時点のユーザーの電話番号。&lt;/li&gt;&lt;li&gt;[E.164 standard](https://en.wikipedia.org/wiki/E.164)形式：`&#43;prefix, country code, subscribe number`&lt;/li&gt;&lt;li&gt;例：`&#43;14150000000`&lt;/li&gt;&lt;/ul&gt; |
|住所：名前|  &lt;ul&gt;&lt;li&gt;ユーザーの名前。&lt;/li&gt;&lt;li&gt;住所の場合、すべてのデータフィールド（名前、姓、通りの住所、市、地域、郵便番号、国）を提供する必要があります。&lt;/li&gt;&lt;li&gt;複数のメール、電話番号、住所を追加するために配列タイプの属性を使用します。&lt;/li&gt;&lt;/ul&gt; |
|住所：姓|  &lt;ul&gt;&lt;li&gt;ユーザーの姓。&lt;/li&gt;&lt;li&gt;住所の場合、すべてのデータフィールド（名前、姓、通りの住所、市、地域、郵便番号、国）を提供する必要があります。&lt;/li&gt;&lt;li&gt;複数のメール、電話番号、住所を追加するために配列タイプの属性を使用します。&lt;/li&gt;&lt;/ul&gt; |
|住所：通り|  &lt;ul&gt;&lt;li&gt;ユーザーの通りの住所。&lt;/li&gt;&lt;li&gt;住所の場合、すべてのデータフィールド（名前、姓、通りの住所、市、地域、郵便番号、国）を提供する必要があります。&lt;/li&gt;&lt;li&gt;複数のメール、電話番号、住所を追加するために配列タイプの属性を使用します。&lt;/li&gt;&lt;/ul&gt; |
|住所：市|  &lt;ul&gt;&lt;li&gt;ユーザーの市名。&lt;/li&gt;&lt;li&gt;住所の場合、すべてのデータフィールド（名前、姓、通りの住所、市、地域、郵便番号、国）を提供する必要があります。&lt;/li&gt;&lt;li&gt;複数のメール、電話番号、住所を追加するために配列タイプの属性を使用します。&lt;/li&gt;&lt;/ul&gt; |
|住所：地域|  &lt;ul&gt;&lt;li&gt;ユーザーの県、州、または地域。&lt;/li&gt;&lt;li&gt;住所の場合、すべてのデータフィールド（名前、姓、通りの住所、市、地域、郵便番号、国）を提供する必要があります。&lt;/li&gt;&lt;li&gt;複数のメール、電話番号、住所を追加するために配列タイプの属性を使用します。&lt;/li&gt;&lt;/ul&gt; |
|住所：郵便番号|  &lt;ul&gt;&lt;li&gt;ユーザーの郵便番号。&lt;/li&gt;&lt;li&gt;住所の場合、すべてのデータフィールド（名前、姓、通りの住所、市、地域、郵便番号、国）を提供する必要があります。&lt;/li&gt;&lt;li&gt;複数のメール、電話番号、住所を追加するために配列タイプの属性を使用します。&lt;/li&gt;&lt;/ul&gt; |
|住所：国|  &lt;ul&gt;&lt;li&gt;[ISO 3166-1 alpha-3](https://en.wikipedia.org/wiki/ISO_3166-1_alpha-3)形式のユーザーの3文字の国コード。&lt;/li&gt;&lt;li&gt;住所の場合、すべてのデータフィールド（名前、姓、通りの住所、市、地域、郵便番号、国）を提供する必要があります。&lt;/li&gt;&lt;li&gt;複数のメール、電話番号、住所を追加するために配列タイプの属性を使用します。&lt;/li&gt;&lt;/ul&gt; |
|顧客データのハッシュ化|  &lt;ul&gt;&lt;li&gt;オプション&lt;/li&gt;&lt;li&gt;マップされた顧客データ（メール、電話、名前、姓、通りの住所）がすでにwebsafe-base 64 eoncoded SHA-256ハッシュを使用してハッシュ化されているかどうかを確認します。注：これはSHA-256文字列をbase64エンコードするのとは異なります。既存のSHA-256文字列をバイナリに変換してからbase64エンコードします。&lt;/li&gt;&lt;/ul&gt; |
|増分性研究のためのアプリコンバージョン|  &lt;ul&gt;&lt;li&gt;オプション&lt;/li&gt;&lt;li&gt;このアクションが増分性研究のためのコンバージョンイベントに関連しているかどうかを確認します。&lt;/li&gt;&lt;/ul&gt; |
|増分性研究のためのコンバージョンデータ|  &lt;ul&gt;&lt;li&gt;オプション&lt;/li&gt;&lt;li&gt;このコンバージョンイベントの増分性研究に使用するための雑多なデータフィールドを1つ以上マップします。&lt;/li&gt;&lt;/ul&gt; |

## 一般的なエラーとトラブルシューティング

以下は一般的なエラーコードと解決策の一部です：

* **INVALID_CONVERSION_DATA**：コンバージョンのデータが無効です。可能なアクションの失敗は以下の通りです：
  * **urlまたはjsonペイロードに有効なconversion_typeまたはlabelが提供されていません**：labelが提供されていない場合、`conversion_type`が必要です。これらのうちの1つがマップされた属性に値があることを確認してください。
  * **urlまたはjsonペイロードに提供されたconversion_timeが古すぎます。**：マップされたタイムスタンプが正しい形式であることを確認してください。例：**2022-08-01 00:06:06&#43;00:01**。または、マッピングを削除し、コネクタにデフォルトの現在のタイムスタンプを送信させます。

* **INVALID_USER_CUSTOMER_AUTHORIZATION**：コネクタ構成の顧客IDに`AW-`が含まれていないことを確認します。認証されたユーザーは、コンバージョンアクションを所有するアカウントに対して少なくとも読み取り専用のアクセス権を持っている必要があります。
* **無効なパラメータ - アクションに無効なパラメータ値があるか、必要なパラメータが欠けています / メールまたはフルネーム＆アドレスのいずれかを提供する必要があります**：Enhanced Conversionsに必要なPIIは以下のセットのいずれかです：   
a) 顧客のメール  
b) 顧客の名前、姓、通りの住所、市、州、国、郵便番号  
イベントデータに必要なフィールド値が存在することを確認してください。
