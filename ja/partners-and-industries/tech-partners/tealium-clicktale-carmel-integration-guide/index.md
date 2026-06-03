---
title: Tealium + Clicktale 統合ガイド
description: この記事では、iQタグ管理アカウントでClicktaleタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/partners-and-industries/tech-partners/tealium-clicktale-carmel-integration-guide/
---
TealiumタグマーケットプレイスからのClicktaleタグとiQタグ管理の統合は、クリックストリームデータに関連するセッションリプレイをシームレスに実行し、タグ付けされたWebページに関連するエンドカスタマーの摩擦を検出して最小限に抑えることを可能にします。

## 前提条件

* **Tealium**
    * iQタグ管理
    * AudienceStream
    * EventStream（オプション）
* **Clicktale**
    * データエクスポートへのアクセスがあるすべての顧客に利用可能なClicktaleリアルタイムシグナル

## 動作原理

Clicktaleは、ユニークな行動洞察を活用してユーザーエクスペリエンスを測定可能な利点に変えることをブランドに可能にします。Clicktaleについての詳細は、Contentsquare社のウェブサイト [contentsquare.com](https://contentsquare.com/) をご覧ください。

### 詐欺

* **過剰なペースト**  
同一訪問セッション内で異常かつ潜在的に詐欺的なペースト行動が識別された場合にトリガーされます。詐欺の可能性は**低**、**中**、**高**の3段階です。
* **過剰なリロード**  
同一訪問セッション内で異常かつ潜在的に詐欺的なリロード行動が識別された場合にトリガーされます。詐欺の可能性は**低**、**中**、**高**の3段階です。

### 広告ブロック

* **広告ブロッカーシグナル**  
特定のファイルがブロックされているかどうかを識別し、広告ブロッカーの存在を特定します。  
イベントストリームのイベント仕様やAudienceStreamの訪問属性からシグナルをオプションで使用できます。

## タグのヒント

* 注文IDが構成されたときに変換が発生します。
* Clicktale Replay LinkをTealiumに送信するには：
    1. リプレイリンクの生成を有効にするためにClicktale担当者に連絡してください。
    1. Send Replay Link構成を**True**に構成します。
* Contentsquareタグはページ上でロードされているTealiumアカウントとプロファイルを自動的に検出し、リプレイリンクをそこに送信します。リプレイリンクを別のアカウントやプロファイルに送信するには、デフォルト値を上書きして、`tealium_account` および `tealium_profile` の宛先にマッピングしたいアカウントとプロファイルを構成します。
* TealiumのAudiencesとBadgesをClicktaleに渡すには：
    1. このデータの受信を有効にするためにClicktale担当者に連絡してください。
    1. バッジをClicktaleに送信するには、マッピングツールボックスのBadgesタブに移動し、Clicktaleシステムで識別される名前を入力します。
    1. すべてのAudiencesをClicktaleに送信するには、Send UDH Audiencesトグルを**True**に切り替えます。

## タグの構成

まず、TealiumのタグマーケットプレイスにアクセスしてClicktale Carmelタグを追加します（[タグの追加方法についてはこちら]()を参照してください）。

タグを追加した後、データマッピングセクションで以下の構成を構成します。

## ロードルール

[Load Rules]()は、このタグのインスタンスをいつ、どこでロードするかを決定します。デフォルトのロードルールは「すべてのページでロード」です。特定のページでこのタグをロードするには、関連する条件を持つ新しいロードルールを作成します。

* 訪問のマウス動作を追跡したいページでこのタグをロードします。

## データマッピング

マッピングは、[data layer variable]()からベンダータグの対応する宛先変数にデータを送信するプロセスです。変数をタグ宛先にマッピングする方法については、[Data Mappings](/ja/iq-tag-management/data-mappings/manage/)を参照してください。

利用可能なカテゴリは以下の通りです：

### 標準

|変数| 説明|
|---| ---|
| `title` |  &lt;ul&gt;&lt;li&gt;(必須) タグインスタンスを識別します。&lt;/li&gt;&lt;li&gt;デフォルト名はClicktale Carmelです。&lt;/li&gt;&lt;li&gt;同じベンダーの複数のタグを使用する場合は、一意の名前を割り当ててください。&lt;/li&gt;&lt;/ul&gt; |
|`partition`|  &lt;ul&gt;&lt;li&gt;パーティション。&lt;/li&gt;&lt;li&gt;データが送信されるパーティション。&lt;/li&gt;&lt;li&gt;この変数にマッピングして、サーバーパーティション値を動的に構成します。&lt;/li&gt;&lt;/ul&gt; |
|`project_guid`|  &lt;ul&gt;&lt;li&gt;プロジェクトGUID。&lt;/li&gt;&lt;li&gt;この変数にマッピングして、プロジェクトガイドフィールドを構成します。&lt;/li&gt;&lt;/ul&gt; |
|`send_replay_link`|  &lt;ul&gt;&lt;li&gt;Clicktaleリプレイリンクを送信&lt;/li&gt;&lt;li&gt;値は**true**または**false**です。&lt;/li&gt;&lt;/ul&gt; |
|`send_udh_audiences`|  &lt;ul&gt;&lt;li&gt;UDHオーディエンスを送信。&lt;/li&gt;&lt;li&gt;値は**true**または**false**です。&lt;/li&gt;&lt;/ul&gt; |
|`tealium_account`|  &lt;ul&gt;&lt;li&gt;Tealiumアカウント。&lt;/li&gt;&lt;/ul&gt; |
|`tealium_profile`|  &lt;ul&gt;&lt;li&gt;Tealiumプロファイル。&lt;/li&gt;&lt;/ul&gt; |

### E-Commerce

|変数| 説明|
|---| ---|
|`order_id`|  &lt;ul&gt;&lt;li&gt;注文ID。&lt;/li&gt;&lt;li&gt;`_corder`を上書きします。&lt;/li&gt;&lt;li&gt;トランザクションに必須です。&lt;/li&gt;&lt;/ul&gt; |
|`order_total`|  &lt;ul&gt;&lt;li&gt;注文合計。&lt;/li&gt;&lt;li&gt;`_ctotal`を上書きします。&lt;/li&gt;&lt;li&gt;トランザクションに必須です。&lt;/li&gt;&lt;/ul&gt; |
|`order_shipping`|  &lt;ul&gt;&lt;li&gt;送料。&lt;/li&gt;&lt;li&gt;`_cship`を上書きします。&lt;/li&gt;&lt;/ul&gt; |
|`order_tax`|  &lt;ul&gt;&lt;li&gt;税金。&lt;/li&gt;&lt;li&gt;`_ctax`を上書きします。&lt;/li&gt;&lt;/ul&gt; |
|`product_id`|  &lt;ul&gt;&lt;li&gt;配列&lt;/li&gt;&lt;li&gt;製品IDのリスト。&lt;/li&gt;&lt;li&gt;`_cprod`を上書きします。&lt;/li&gt;&lt;/ul&gt; |
|`product_name`|  &lt;ul&gt;&lt;li&gt;配列&lt;/li&gt;&lt;li&gt;名前のリスト。&lt;/li&gt;&lt;li&gt;`_cprodname`を上書きします。&lt;/li&gt;&lt;li&gt;トランザクションに必須です。&lt;/li&gt;&lt;/ul&gt; |
|`product_sku`|  &lt;ul&gt;&lt;li&gt;配列&lt;/li&gt;&lt;li&gt;SKUのリスト。&lt;/li&gt;&lt;li&gt;`_csku`を上書きします。&lt;/li&gt;&lt;li&gt;トランザクションに必須です。&lt;/li&gt;&lt;/ul&gt; |
|`product_category`|  &lt;ul&gt;&lt;li&gt;配列&lt;/li&gt;&lt;li&gt;カテゴリのリスト。&lt;/li&gt;&lt;li&gt;`_ccat`を上書きします。&lt;/li&gt;&lt;/ul&gt; |
|`product_quantity`|  &lt;ul&gt;&lt;li&gt;配列&lt;/li&gt;&lt;li&gt;数量のリスト。&lt;/li&gt;&lt;li&gt;`_cquan`を上書きします。&lt;/li&gt;&lt;li&gt;トランザクションに必須です。&lt;/li&gt;&lt;/ul&gt; |
|`product_unit_price`|  &lt;ul&gt;&lt;li&gt;配列&lt;/li&gt;&lt;li&gt;価格のリスト。&lt;/li&gt;&lt;li&gt;`_cprice`を上書きします。&lt;/li&gt;&lt;li&gt;トランザクションに必須です。&lt;/li&gt;&lt;/ul&gt; |

### バッジ

|変数| 説明|
| --- | --- |
| `title` |  &lt;ul&gt;&lt;li&gt;バッジ識別子。&lt;/li&gt;&lt;li&gt;マッピングされたバッジをClicktaleに送信するには、Clicktaleで識別される名前を入力してください。&lt;/li&gt;&lt;li&gt;Tealiumは自動的に新しいオブジェクト`send_udh_data`の子プロパティとしてバッジタイトルを含めます。&lt;/li&gt;&lt;li&gt;あなたのバッジ名は`send_udh_data`にマッピングされたものとして表示されます。&lt;/li&gt;&lt;/ul&gt; |
