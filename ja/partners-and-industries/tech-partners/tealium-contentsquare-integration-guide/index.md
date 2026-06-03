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

以前は、Contentsquareタグの構成で利用可能だった詐欺と広告ブロックのトリガーは、現在タグに組み込まれ、デフォルトで有効になっています。

### 詐欺

* **過度のペースト**
同一訪問セッション内で異常かつ潜在的に詐欺的なペースト行動が識別された場合にトリガーされます。詐欺の可能性は**低**、**中**、**高**の3段階です。
* **過度のリロード**
同一訪問セッション内で異常かつ潜在的に詐欺的なリロード行動が識別された場合にトリガーされます。詐欺の可能性は**低**、**中**、**高**の3段階です。

### 広告ブロック

* **広告ブロッカーシグナル**
特定のファイルがブロックされているかどうかを識別し、広告ブロッカーの存在を示します。
EventStreamのイベント仕様やAudienceStreamの訪問属性からのシグナルをオプションで使用することができます。

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

まず、Tealiumタグマーケットプレイスにアクセスして、Contentsquare UXユーザーアナリティクスタグを追加します（[タグの追加方法についてはこちら]()を参照）。

参照：[Contentsquare UXユーザーアナリティクスタグ構成ガイド]()

タグを追加した後、**データマッピング**セクションに移動して、追加のマッピングを構成します。

## ロードルール

[ロードルール]()は、このタグのインスタンスをいつ、どこでロードするかを決定します。デフォルトのロードルールは「すべてのページでロード」です。

特定のページでこのタグをロードするには、関連する条件で新しいロードルールを作成し、訪問のマウス動作を追跡したいページでContentsquareタグをロードします。

## 拡張機能

データレイヤーで`tealium_datasource`を構成する必要があります。これによりContentsquareはサーバーサイドでデータを送信できます。

1. **サーバーサイド &amp;gt; データソース**に移動します。
1. HTTP APIデータソースを追加します。
1. 名前を「Contentsquareサーバーサイドイベント」と構成します。

完了したら、データソースキーをメモしてください。iQタグ管理では、この値を`tealium_datasource`変数に割り当てるために拡張機能を使用します。

Tealium Universal Tag (utag.js)のバージョン4.41以前を使用している場合は、以下の変数も構成する必要があります：

* `tealium_account`
* `tealium_profile`
* `tealium_visitor_id`

これらの変数は、バージョン4.42以降では自動的に構成されます。

## データマッピング

マッピングは、[データレイヤー変数]()からベンダータグの対応する宛先変数にデータを送信するプロセスです。変数をタグの宛先にマッピングする方法については、[データマッピング](/ja/iq-tag-management/data-mappings/manage/)を参照してください。

利用可能なカテゴリは以下の通りです：

### 標準

|変数| 説明|
|---| ---|
| `title` |  &lt;ul&gt;&lt;li&gt;(必須) タグインスタンスを識別します。&lt;/li&gt;&lt;li&gt;デフォルト名はContentsquare UXアナリティクスです。&lt;/li&gt;&lt;li&gt;同じベンダーの複数のタグを使用する場合は、一意の名前を割り当てます。&lt;/li&gt;&lt;/ul&gt; |
| `id_project` |  &lt;ul&gt;&lt;li&gt;プロジェクト固有のプロジェクトタグIDです。&lt;/li&gt;&lt;li&gt;この変数にマッピングしてプロジェクトガイドフィールドを構成します。&lt;/li&gt;&lt;/ul&gt; |
| `base_url` |  &lt;ul&gt;&lt;li&gt;ベースURL&lt;/li&gt;&lt;/ul&gt; |
| `send_replay_link` |  &lt;ul&gt;&lt;li&gt;Contentsquareリプレイリンクを送信します&lt;/li&gt;&lt;li&gt;値は**true**または**false**です。&lt;/li&gt;&lt;li&gt;`contensquare_replay_link`とも呼ばれます。注意：この変数とセッションリプレイ機能は現在Contentsquareタグで開発中で、2020年上半期にリリース予定です。&lt;/li&gt;&lt;/ul&gt; |
| `send_udh_audiences` |  &lt;ul&gt;&lt;li&gt;カスタマーデータハブ（CDH）のオーディエンスを送信します。&lt;/li&gt;&lt;li&gt;値は**true**または**false**です。&lt;/li&gt;&lt;/ul&gt; |
| `tealium_account` |  &lt;ul&gt;&lt;li&gt;Tealiumアカウント。&lt;/li&gt;&lt;/ul&gt; |
| `tealium_profile` |  &lt;ul&gt;&lt;li&gt;Tealiumプロファイル。&lt;/li&gt;&lt;/ul&gt; |

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
|---| ---|
| `title` |  &lt;ul&gt;&lt;li&gt;バッジ識別子。&lt;/li&gt;&lt;li&gt;マッピングされたバッジをContentsquareに送るには、Contentsquareで識別される名前を入力します。&lt;/li&gt;&lt;li&gt;Tealiumは自動的に新しいオブジェクト`send_udh_data`の子プロパティとしてバッジタイトルを含めます。&lt;/li&gt;&lt;li&gt;あなたのバッジ名は`send_udh_data`にマッピングされたものとして表示されます。&lt;/li&gt;&lt;/ul&gt; |
