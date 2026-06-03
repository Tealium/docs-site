---
title: Responsysマーケティングクラウドコネクタ構成ガイド
description: この記事では、Responsysマーケティングクラウドコネクタの構成方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/responsys-marketing-cloud-connector/
---

## コネクタのアクション

| アクション名 | AudienceStream | EventStream |
| --- | :---: | :---: |
|リスト受信者のマージ| ✓| ✓|
|プロフィール拡張受信者のマージ| ✓| ✓|
|テーブルレコードのマージ| ✓| ✓|
|カスタムイベントのトリガー| ✓| ✓|

### バッチ制限

このコネクタは、ベンダーへの大量データ転送をサポートするためにバッチリクエストを使用します。詳細については、[バッチアクション]()を参照してください。リクエストは、以下のいずれかの閾値が達成されるか、プロフィールが公開されるまでキューに入れられます：

* リクエストの最大数：100
* 最古のリクエストからの最大時間：60分
* リクエストの最大サイズ：1 MB

## 構成の構成

コネクタマーケットプレイスに移動し、新しいコネクタを追加します。コネクタの追加方法の一般的な指示については、[コネクタについて]()の記事を参照してください。

コネクタを追加した後、以下の構成を構成します：

* **APIユーザー名**
* **APIパスワード**
* **ログインエンドポイント**

## アクション構成 - パラメータとオプション

**次へ**をクリックするか、**アクション**タブに移動します。ここでコネクタアクションを構成します。

このセクションでは、各アクションのパラメータとオプションの構成方法について説明します。

### アクション - リスト受信者のマージ

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|リスト名|  &lt;ul&gt;&lt;li&gt;必須&lt;/li&gt;&lt;/ul&gt; |
|デフォルトの許可ステータス|  &lt;ul&gt;&lt;li&gt;オプション&lt;/li&gt;&lt;li&gt;値は **Opt In** または **Opt Out** です。&lt;/li&gt;&lt;/ul&gt; |
|マッチ列|  &lt;ul&gt;&lt;li&gt;オプション&lt;/li&gt;&lt;li&gt;受信者レコードをプロフィール拡張レコードと一致させるために使用される列名。&lt;/li&gt;&lt;/ul&gt; |
|マッチ演算子|  &lt;ul&gt;&lt;li&gt;オプション&lt;/li&gt;&lt;li&gt;マッチ列名を結合する演算子。&lt;/li&gt;&lt;/ul&gt; |
|更新戦略|  &lt;ul&gt;&lt;li&gt;オプション&lt;/li&gt;&lt;li&gt;既存のレコードがどのように更新されるかを制御します。  &lt;ul&gt;&lt;li&gt;**No Update** — 選択した場合、既存のレコードが一致した場合、更新は行われません（挿入のみ）。&lt;/li&gt;&lt;li&gt;**Replace All** — 選択した場合、既存のレコードが一致した場合、構成されたすべてのプロパティが更新されます。&lt;/li&gt;&lt;/ul&gt; &lt;/li&gt;&lt;/ul&gt; |
|HTML値|  &lt;ul&gt;&lt;li&gt;オプション&lt;/li&gt;&lt;li&gt;入力された優先メール形式データの値。&lt;/li&gt;&lt;li&gt;例：`H`はHTML形式のメールを優先することを表す場合があります。&lt;/li&gt;&lt;/ul&gt; |
|Opt In値|  &lt;ul&gt;&lt;li&gt;オプション&lt;/li&gt;&lt;li&gt;Opt-inステータスを表す入力されたOpt-inステータスデータの値。&lt;/li&gt;&lt;li&gt;例：`I`はOpt-inステータスを表す場合があります。&lt;/li&gt;&lt;/ul&gt; |
|Opt Out値|  &lt;ul&gt;&lt;li&gt;オプション&lt;/li&gt;&lt;li&gt;Opt-outステータスを表す入力されたOpt-outステータスデータの値。&lt;/li&gt;&lt;li&gt;例：`O`はOpt-outステータスを表す場合があります。&lt;/li&gt;&lt;/ul&gt; |
|チャネルが空の場合はレコードを拒否|  &lt;ul&gt;&lt;li&gt;オプション&lt;/li&gt;&lt;li&gt;チャネルアドレスフィールドがnullの場合にレコード拒否を引き起こすカンマで区切られたチャネルコードを含む文字列。&lt;/li&gt;&lt;li&gt;チャネルコードは次のとおりです：  &lt;ul&gt;&lt;li&gt;**E** – メール&lt;/li&gt;&lt;li&gt;**M** – モバイル&lt;/li&gt;&lt;li&gt;**P** – 郵便番号&lt;/li&gt;&lt;/ul&gt; &lt;/li&gt;&lt;/ul&gt; &lt;ul&gt;&lt;li&gt;例：&#34;`E,M`&#34;は、メールまたはモバイル番号の値がnullのレコードが拒否されることを示します。&lt;/li&gt;&lt;/ul&gt; |
|テキスト値|  &lt;ul&gt;&lt;li&gt;オプション&lt;/li&gt;&lt;li&gt;入力された優先メール形式データの値。&lt;/li&gt;&lt;li&gt;例：`T`はテキスト形式のメールを優先することを表す場合があります。&lt;/li&gt;&lt;/ul&gt; |

### アクション - プロフィール拡張受信者のマージ

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|リスト名|  &lt;ul&gt;&lt;li&gt;必須&lt;/li&gt;&lt;/ul&gt; |
|プロフィール拡張テーブル（PET）名|  &lt;ul&gt;&lt;li&gt;プロフィール拡張テーブル名。&lt;/li&gt;&lt;/ul&gt; |
|更新戦略|  &lt;ul&gt;&lt;li&gt;必須&lt;/li&gt;&lt;li&gt;既存のレコードがどのように更新されるかを制御します。  &lt;ul&gt;&lt;li&gt;**No Update** — 選択した場合、既存のレコードが一致した場合、更新は行われません（挿入のみ）。&lt;/li&gt;&lt;li&gt;**Replace All** — 選択した場合、既存のレコードが一致した場合、構成されたすべてのプロパティが更新されます。&lt;/li&gt;&lt;/ul&gt; &lt;/li&gt;&lt;/ul&gt; |
|マッチ列|  &lt;ul&gt;&lt;li&gt;受信者レコードをプロフィール拡張レコードと一致させるために使用される列名。&lt;/li&gt;&lt;li&gt;オプションは次のとおりです：  &lt;ul&gt;&lt;li&gt;受信者ID（RIID）&lt;/li&gt;&lt;li&gt;顧客ID&lt;/li&gt;&lt;li&gt;メールアドレス&lt;/li&gt;&lt;li&gt;モバイル番号&lt;/li&gt;&lt;li&gt;メール（MD5ハッシュ）&lt;/li&gt;&lt;li&gt;メール（SHA 256ハッシュ）&lt;/li&gt;&lt;/ul&gt; &lt;/li&gt;&lt;/ul&gt; |
|マップテンプレート名|  &lt;ul&gt;&lt;li&gt;オプション&lt;/li&gt;&lt;li&gt;Responsysで構成されたマッピングテンプレートを指定します。&lt;/li&gt;&lt;/ul&gt; |

### アクション - テーブルレコードのマージ

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|フォルダ名|  &lt;ul&gt;&lt;li&gt;必須&lt;/li&gt;&lt;/ul&gt; |
|テーブル名|  &lt;ul&gt;&lt;li&gt;必須&lt;/li&gt;&lt;/ul&gt; |
|更新戦略|  &lt;ul&gt;&lt;li&gt;必須&lt;/li&gt;&lt;li&gt;既存のレコードがどのように更新されるかを制御します。  &lt;ul&gt;&lt;li&gt;**No Update** — 選択した場合、既存のレコードが一致した場合、更新は行われません（挿入のみ）。&lt;/li&gt;&lt;li&gt;**Replace All** — 選択した場合、既存のレコードが一致した場合、構成されたすべてのプロパティが更新されます。&lt;/li&gt;&lt;/ul&gt; &lt;/li&gt;&lt;/ul&gt; |
|マッチ列|  &lt;ul&gt;&lt;li&gt;受信者レコードを補足テーブルレコードと一致させるために使用される列名。&lt;/li&gt;&lt;/ul&gt; |
|マップテンプレート名|  &lt;ul&gt;&lt;li&gt;オプション&lt;/li&gt;&lt;li&gt;Responsysで構成されたマッピングテンプレートを指定します。&lt;/li&gt;&lt;/ul&gt; |

### アクション - カスタムイベントのトリガー

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|イベント名|  &lt;ul&gt;&lt;li&gt;必須&lt;/li&gt;&lt;li&gt;カスタムイベント名&lt;/li&gt;&lt;/ul&gt; |
|フォルダ名|  &lt;ul&gt;&lt;li&gt;必須&lt;/li&gt;&lt;/ul&gt; |
|オブジェクト名|  &lt;ul&gt;&lt;li&gt;必須&lt;/li&gt;&lt;li&gt;プロフィールリスト名&lt;/li&gt;&lt;/ul&gt; |
|メール形式|  &lt;ul&gt;&lt;li&gt;必須&lt;/li&gt;&lt;li&gt;値は **Text** または **HTML** です。&lt;/li&gt;&lt;/ul&gt; |
|顧客ID|  &lt;ul&gt;&lt;li&gt;顧客ID&lt;/li&gt;&lt;/ul&gt; |
|メールアドレス|  &lt;ul&gt;&lt;li&gt;メールアドレス&lt;/li&gt;&lt;/ul&gt; |
|モバイル番号|  &lt;ul&gt;&lt;li&gt;モバイル番号&lt;/li&gt;&lt;/ul&gt; |
|モバイル番号|  &lt;ul&gt;&lt;li&gt;モバイル番号&lt;/li&gt;&lt;/ul&gt; |
|数値データマッピング|  &lt;ul&gt;&lt;li&gt;オプション&lt;/li&gt;&lt;/ul&gt; |
|日付データマッピング|  &lt;ul&gt;&lt;li&gt;オプション&lt;/li&gt;&lt;/ul&gt; |
|文字列データマッピング|  &lt;ul&gt;&lt;li&gt;オプション&lt;/li&gt;&lt;/ul&gt; |
|オプショナルデータ|  &lt;ul&gt;&lt;li&gt;オプション&lt;/li&gt;&lt;/ul&gt; |

## ベンダーのドキュメンテーション

* [Oracle Marketing Cloud - Responsys API](https://docs.oracle.com/cloud/latest/marketingcs_gs/responsys.html)
