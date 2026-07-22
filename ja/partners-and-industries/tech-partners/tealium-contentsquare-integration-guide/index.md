---
title: Tealium + Contentsquare 統合ガイド
description: この記事では、Tealium iQタグ管理アカウントでContentsquare UXアナリティクスタグを構成し、TealiumのオーディエンスとビジターバッジをContentsquareに送信することで、TealiumとContentsquareを最大限に活用する方法について説明します。
url: https://docs.tealium.com/ja/partners-and-industries/tech-partners/tealium-contentsquare-integration-guide/
---
iQタグ管理とTealiumタグマーケットプレイスからのContentsquareタグの統合が機能すると、顧客はクリックストリームデータに関連付けられたセッションリプレイを実行し、タグ付けされたWebページに関連するエンドカスタマーの摩擦を検出して最小限に抑えることができます。

## 前提条件

* **Tealium**
    * iQタグ管理
    * AudienceStream
    * EventStream（オプション）
* **Contentsquare**
    * Contentsquareビジネスエディション以上

## 動作原理

Contentsquareは、ブランドがユニークな行動洞察に基づいて行動を起こし、ユーザーエクスペリエンスを測定可能な利点に変えることを可能にします。Contentsquareは、地理や業界を越えたデジタル行動のグローバルデータセットに基づいてベンチマークと予測スコアリングを提供し、収益の増加、ロイヤルティの向上、イノベーションの促進に役立てることができます。

詳細は [contentsquare.com](https://contentsquare.com/) をご覧ください。


<blockquote>
以前は、Contentsquareタグの構成で利用可能だった詐欺と広告ブロックのトリガーは、現在タグに組み込まれ、デフォルトで有効になっています。
</blockquote>


### 詐欺

* **過度のペースト**
同一訪問セッション内で異常かつ潜在的に詐欺的なペースト行動が識別された場合にトリガーされます。詐欺の可能性は**低**、**中**、**高**の3段階です。
* **過度のリロード**
同一訪問セッション内で異常かつ潜在的に詐欺的なリロード行動が識別された場合にトリガーされます。詐欺の可能性は**低**、**中**、**高**の3段階です。

### 広告ブロック

* **広告ブロッカーシグナル**
特定のファイルがブロックされているかどうかを識別し、広告ブロッカーの存在を示します。

<blockquote>
EventStreamのイベント仕様やAudienceStreamの訪問属性からのシグナルをオプションで使用することができます。
</blockquote>


## タグのヒント

* 注文IDが構成されたときにコンバージョンが発生します。
* Contentsquareリプレイリンクをサーバーサイド属性として利用可能にするには：
    * Contentsquareの担当者に連絡して、リプレイリンクの生成を有効にしてもらいます。
    * **Send Replay Link**を**True**に構成します。

* Contentsquareタグはページ上でロードされているTealiumアカウントとプロファイルを自動的に検出し、そこにリプレイリンクを送信します。リプレイリンクを異なるアカウントやプロファイルに送信するには、デフォルト値を上書きして、`tealium_account`と`tealium_profile`の目的地に送りたいアカウントとプロファイルをマッピングします。
* TealiumオーディエンスとバッジをContentsquareに渡すには：
    * Contentsquareの担当者に連絡して、このデータの受信を有効にしてもらいます。
    * バッジをContentsquareに送るには、マッピングツールボックスの**バッジ**タブに移動し、Contentsquareシステムで識別される名前を入力します。
    * すべてのオーディエンスをContentsquareに送るには、**Send All Audiences**を**True**に構成します。

## タグの構成

まず、Tealiumタグマーケットプレイスにアクセスして、Contentsquare UXユーザーアナリティクスタグを追加します（[タグの追加方法についてはこちら](https://docs.tealium.com/manage-tags/)を参照）。

参照：[Contentsquare UXユーザーアナリティクスタグ構成ガイド](https://docs.tealium.com/contentsquare-ux-analytics-tag/)

タグを追加した後、**データマッピング**セクションに移動して、追加のマッピングを構成します。

## ロードルール

[ロードルール](https://docs.tealium.com/about-load-rules/)は、このタグのインスタンスをいつ、どこでロードするかを決定します。デフォルトのロードルールは「すべてのページでロード」です。

特定のページでこのタグをロードするには、関連する条件で新しいロードルールを作成し、訪問のマウス動作を追跡したいページでContentsquareタグをロードします。

## 拡張機能

データレイヤーで`tealium_datasource`を構成する必要があります。これによりContentsquareはサーバーサイドでデータを送信できます。

1. **サーバーサイド &gt; データソース**に移動します。
1. HTTP APIデータソースを追加します。
1. 名前を「Contentsquareサーバーサイドイベント」と構成します。

完了したら、データソースキーをメモしてください。iQタグ管理では、この値を`tealium_datasource`変数に割り当てるために拡張機能を使用します。

Tealium Universal Tag (utag.js)のバージョン4.41以前を使用している場合は、以下の変数も構成する必要があります：

* `tealium_account`
* `tealium_profile`
* `tealium_visitor_id`

これらの変数は、バージョン4.42以降では自動的に構成されます。

## データマッピング

マッピングは、[データレイヤー変数](https://docs.tealium.com/data-layer-variables/)からベンダータグの対応する宛先変数にデータを送信するプロセスです。変数をタグの宛先にマッピングする方法については、[データマッピング](https://docs.tealium.com/ja/iq-tag-management/data-mappings/manage/)を参照してください。

利用可能なカテゴリは以下の通りです：

### 標準

|変数| 説明|
|---| ---|
| `title` |  <ul><li>(必須) タグインスタンスを識別します。</li><li>デフォルト名はContentsquare UXアナリティクスです。</li><li>同じベンダーの複数のタグを使用する場合は、一意の名前を割り当てます。</li></ul> |
| `id_project` |  <ul><li>プロジェクト固有のプロジェクトタグIDです。</li><li>この変数にマッピングしてプロジェクトガイドフィールドを構成します。</li></ul> |
| `base_url` |  <ul><li>ベースURL</li></ul> |
| `send_replay_link` |  <ul><li>Contentsquareリプレイリンクを送信します</li><li>値は**true**または**false**です。</li><li>`contensquare_replay_link`とも呼ばれます。注意：この変数とセッションリプレイ機能は現在Contentsquareタグで開発中で、2020年上半期にリリース予定です。</li></ul> |
| `send_udh_audiences` |  <ul><li>カスタマーデータハブ（CDH）のオーディエンスを送信します。</li><li>値は**true**または**false**です。</li></ul> |
| `tealium_account` |  <ul><li>Tealiumアカウント。</li></ul> |
| `tealium_profile` |  <ul><li>Tealiumプロファイル。</li></ul> |

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
|---| ---|
| `title` |  <ul><li>バッジ識別子。</li><li>マッピングされたバッジをContentsquareに送るには、Contentsquareで識別される名前を入力します。</li><li>Tealiumは自動的に新しいオブジェクト`send_udh_data`の子プロパティとしてバッジタイトルを含めます。</li><li>あなたのバッジ名は`send_udh_data`にマッピングされたものとして表示されます。</li></ul> |
