---
title: Oracle BlueKai モバイルコネクタ構成ガイド
description: この記事では、Oracle BlueKai モバイルコネクタの構成方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/oracle-bluekai-mobile-connector/
---
## コネクタアクション

| **アクション名** | **AudienceStream** | **EventStream** |
|:----------------|:-------------------|:----------------|
| ピクセルを送信      | ✓                  | ✓               |

## 構成を構成する

コネクタマーケットプレイスに移動し、新しいコネクタを追加します。コネクタを追加する一般的な手順については、[コネクタ概要]()の記事を参照してください。

コネクタを追加した後、次の構成を構成します：

* **サイトID**：BlueKaiコンテナから提供され、BlueKaiプラットフォームでデスクトップサイトとモバイルサイトを関連付けます。

## アクション構成 - パラメータとオプション

**次へ**をクリックするか、**アクション**タブに移動します。ここでコネクタアクションを構成します。

このセクションでは、各アクションのパラメータとオプションの構成方法について説明します。

### アクション - ピクセルを送信

#### パラメータ

| **パラメータ**   | **説明**                                                                                                                                                                                                                                                                 |
|:----------------|:--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| ユーザーエージェント      | &lt;ul&gt;&lt;li&gt;提供された場合、`User-Agent`ヘッダーで値が使用されます&lt;/li&gt;&lt;li&gt;指定されていない場合、デフォルトは`Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/69.0.3497.100 Safari/537.36`になります&lt;/li&gt;&lt;/ul&gt;                                        |
| ユーザーIDタイプ    | &lt;ul&gt;&lt;li&gt;ユーザー識別子のタイプ&lt;/li&gt;&lt;li&gt;BlueKaiウェブサイトの[IDスワッピング](https://docs.oracle.com/en/cloud/saas/data-cloud/dsmkt/integrating-oracle-bluekai-platform.html#GUID-A8856438-EF6A-4BCE-A2E4-B4CE725B0E61)ガイドラインを参照してください&lt;/li&gt;&lt;/ul&gt;                                    |
| ユーザーID値   | &lt;ul&gt;&lt;li&gt;ユーザー識別子の値&lt;/li&gt;&lt;/ul&gt;                                                                                                                                                                                                                                      |
| IDハッシュ      | &lt;ul&gt;&lt;li&gt;ユーザーIDをハッシュ化するためにチェックします&lt;/li&gt;&lt;li&gt;メールアドレスと電話番号はハッシュ化する必要があります&lt;/li&gt;&lt;/ul&gt;                                                                                                                                                                                       |
| ハッシュタイプ       | &lt;ul&gt;&lt;li&gt;ハッシュ化アルゴリズムを選択します&lt;/li&gt;&lt;li&gt;メールアドレスと電話番号はMD5またはSHA256でハッシュ化する必要があります&lt;/li&gt;&lt;li&gt;ANDROIDIDはMD5またはSHA1でハッシュ化する必要があります&lt;/li&gt;&lt;li&gt;ADIDとIDFAはMD5またはSHA1でハッシュ化するか、全くハッシュ化しないかを選択します&lt;/li&gt;&lt;/ul&gt; |
| Phints          | &lt;ul&gt;&lt;li&gt;キーと値のペアとしてphintsを提供します&lt;/li&gt;&lt;li&gt;左側の値が右側のキーに割り当てられます&lt;/li&gt;&lt;/ul&gt;                                                                                                                                                        |
| 追加データ | &lt;ul&gt;&lt;li&gt;キーと値のペアとして追加データを提供します&lt;/li&gt;&lt;li&gt;このデータに対して追加の処理は行われません&lt;/li&gt;&lt;/ul&gt;                                                                                                                                                        |
