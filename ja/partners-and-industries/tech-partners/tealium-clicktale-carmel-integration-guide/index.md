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

<blockquote>
イベントストリームのイベント仕様やAudienceStreamの訪問属性からシグナルをオプションで使用できます。
</blockquote>


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

まず、TealiumのタグマーケットプレイスにアクセスしてClicktale Carmelタグを追加します（[タグの追加方法についてはこちら](https://docs.tealium.com/manage-tags/)を参照してください）。

タグを追加した後、データマッピングセクションで以下の構成を構成します。

## ロードルール

[Load Rules](https://docs.tealium.com/about-load-rules/)は、このタグのインスタンスをいつ、どこでロードするかを決定します。デフォルトのロードルールは「すべてのページでロード」です。特定のページでこのタグをロードするには、関連する条件を持つ新しいロードルールを作成します。

* 訪問のマウス動作を追跡したいページでこのタグをロードします。

## データマッピング

マッピングは、[data layer variable](https://docs.tealium.com/data-layer-variables/)からベンダータグの対応する宛先変数にデータを送信するプロセスです。変数をタグ宛先にマッピングする方法については、[Data Mappings](https://docs.tealium.com/ja/iq-tag-management/data-mappings/manage/)を参照してください。

利用可能なカテゴリは以下の通りです：

### 標準

|変数| 説明|
|---| ---|
| `title` |  <ul><li>(必須) タグインスタンスを識別します。</li><li>デフォルト名はClicktale Carmelです。</li><li>同じベンダーの複数のタグを使用する場合は、一意の名前を割り当ててください。</li></ul> |
|`partition`|  <ul><li>パーティション。</li><li>データが送信されるパーティション。</li><li>この変数にマッピングして、サーバーパーティション値を動的に構成します。</li></ul> |
|`project_guid`|  <ul><li>プロジェクトGUID。</li><li>この変数にマッピングして、プロジェクトガイドフィールドを構成します。</li></ul> |
|`send_replay_link`|  <ul><li>Clicktaleリプレイリンクを送信</li><li>値は**true**または**false**です。</li></ul> |
|`send_udh_audiences`|  <ul><li>UDHオーディエンスを送信。</li><li>値は**true**または**false**です。</li></ul> |
|`tealium_account`|  <ul><li>Tealiumアカウント。</li></ul> |
|`tealium_profile`|  <ul><li>Tealiumプロファイル。</li></ul> |

### E-Commerce

|変数| 説明|
|---| ---|
|`order_id`|  <ul><li>注文ID。</li><li>`_corder`を上書きします。</li><li>トランザクションに必須です。</li></ul> |
|`order_total`|  <ul><li>注文合計。</li><li>`_ctotal`を上書きします。</li><li>トランザクションに必須です。</li></ul> |
|`order_shipping`|  <ul><li>送料。</li><li>`_cship`を上書きします。</li></ul> |
|`order_tax`|  <ul><li>税金。</li><li>`_ctax`を上書きします。</li></ul> |
|`product_id`|  <ul><li>配列</li><li>製品IDのリスト。</li><li>`_cprod`を上書きします。</li></ul> |
|`product_name`|  <ul><li>配列</li><li>名前のリスト。</li><li>`_cprodname`を上書きします。</li><li>トランザクションに必須です。</li></ul> |
|`product_sku`|  <ul><li>配列</li><li>SKUのリスト。</li><li>`_csku`を上書きします。</li><li>トランザクションに必須です。</li></ul> |
|`product_category`|  <ul><li>配列</li><li>カテゴリのリスト。</li><li>`_ccat`を上書きします。</li></ul> |
|`product_quantity`|  <ul><li>配列</li><li>数量のリスト。</li><li>`_cquan`を上書きします。</li><li>トランザクションに必須です。</li></ul> |
|`product_unit_price`|  <ul><li>配列</li><li>価格のリスト。</li><li>`_cprice`を上書きします。</li><li>トランザクションに必須です。</li></ul> |

### バッジ

|変数| 説明|
| --- | --- |
| `title` |  <ul><li>バッジ識別子。</li><li>マッピングされたバッジをClicktaleに送信するには、Clicktaleで識別される名前を入力してください。</li><li>Tealiumは自動的に新しいオブジェクト`send_udh_data`の子プロパティとしてバッジタイトルを含めます。</li><li>あなたのバッジ名は`send_udh_data`にマッピングされたものとして表示されます。</li></ul> |
