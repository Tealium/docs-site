---
title: The Trade Desk Cookie Matching Serviceタグ構成ガイド
description: この記事では、Tealium iQタグ管理アカウントでThe Trade Desk Cookie Matching Serviceタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/the-trade-desk-cookie-matching-service-tag/
---
 このタグを`utag`バージョン4.50以降で使用する場合、`utag.js`の[`always_set_v_id`構成]()を`true`に構成する必要があります。この構成により、訪問IDがクッキー同期に利用可能になります。詳細は、[utag 4.50リリースノート]()と[utag 4.50&#43;へのアップグレード時のtealium_visitor_idに関する考慮事項](https://support.tealiumiq.com/en/support/solutions/articles/36000535887-considerations-for-tealium-visitor-id-when-upgrading-to-utag-4-50-)を参照してください。

## 必要条件

* iQタグ管理
* AudienceStream

## 動作方法

The Trade Desk Cookie Matching Serviceタグは、新しい変数`ttd_uuid`を構成します。これはセッションクッキーとして、また標準的なデータレイヤー変数として保存されます。このタグはデフォルトでセッションごとに一度だけトリガーされます。

The Trade Desk Cookie Matching Serviceタグは、Trade Deskのサーバーと通信して現在のユーザーの識別子をリクエストします。この値がタグに返されると、その値はAudienceStreamに渡され、同期されたユーザーIDを含む訪問属性を生成するために使用されます。この属性は、&#34;Trade Desk ID (TDID)&#34;へのマッピングとしてThe Trade Deskコネクタアクションで使用できます。

## データレイヤー変数

タグを追加する前に、以下のデータレイヤー変数を作成します：

* `ttd_uuid`: UDO変数
* `utag_main_ttd_uuid`: ファーストパーティクッキー

これらの変数は、クッキーマッチングタグによって自動的に生成されます。

![](/images/client-side-tags/the-trade-desk-cookie.png)

## タグ構成

タグマーケットプレイスに移動し、Trade Desk Cookie Matching Serviceタグを追加します（[タグの追加方法]()について詳しくはこちらをご覧ください）。

タグを追加した後、以下の構成を行います：

* **Tealiumアカウント**: The Trade DeskユーザーIDを別のアカウントに送信する場合を除き、空白のままにします。
* **Tealiumプロファイル**: The Trade DeskユーザーIDを別のプロファイルに送信する場合を除き、空白のままにします。

### ロードルール

[ロードルール]()は、サイト上のどこで、いつこのタグのインスタンスをロードするかを決定します。

このタグは、クッキーマッチがまだ行われていない場合にのみ実行する必要があります。これは、ロードルール条件としてクッキー変数`utag_main_ttd_uuid`を使用して判断できます：

`utag_main_ttd_uuid`が定義されていない

タグには、クッキーが定義されていない場合にのみ発火する組み込みのロジックがありますが、ロードルールを使用することで、現在のセッションで既に実行されている場合にはページ上でタグがロードされないことを保証します。

## データマッピング

マッピングは、[データレイヤー変数]()からベンダータグの対応する宛先変数にデータを送信するプロセスです。変数をタグの宛先にマップする方法については、[データマッピング]()を参照してください。

|**宛先名**| **タイプ** | **説明**|
|---| ---| ---|
|`tealium_account`| 文字列 | ユーザーIDを同期するTealiumアカウント。デフォルトは現在のアカウントです。 |
|`tealium_profile`| 文字列 | ユーザーIDを同期するTealiumプロファイル。デフォルトは現在のプロファイルです。 |
|`gdpr`| ブール値 | 現在のユーザーが欧州連合（EU）に居住しており、したがってGDPRの対象であることを示す値を渡します。&lt;ul&gt;&lt;li&gt;ユーザーがGDPRの対象でない場合は`0`（デフォルト）、GDPRの対象である場合は`1`に構成します。&lt;br&gt; この値を`0`に構成し、訪問がEUに位置している場合、Cookie Sync Serviceは空の配列を返します。&lt;/li&gt;&lt;/ul&gt; |
|`gdpr_consent_string`| 文字列 | Base64 URLエンコードされたGDPR同意文字列。|
| `domain` | 文字列 | クッキー同期が開始するドメイン。&lt;br&gt; 注意: このドメインをThe Trade Deskの構成で**許可リスト**に追加する必要があります。 |
|`order_id`| 文字列 | `_corder` e-commerce拡張値を上書きします。|

## AudienceStream構成

変更を保存し、Prodに公開した後、新しい変数はAudienceStreamで利用可能になります。`ttd_uuid`変数はイベント属性として表示されますが、The Trade Deskコネクタアクションで使用できるように、訪問属性として作成する必要があります。

`ttd_uuid`値を保存する訪問属性を追加するには：

1. **Transform &gt; Visitor / Visit Attributes**に移動します。
1. **属性を追加**をクリックし、**訪問**スコープ、次に**文字列**データタイプを選択します。
1. 名前に`Trade Desk User ID`を入力します。
1. **エンリッチメントを追加**をクリックし、**文字列を構成**を選択します。
1. **Set String to**ドロップダウンメニューから`ttd_uuid`を選択します。
1. **完了**をクリックします。

これで、Trade Desk User IDが入力された訪問のオーディエンスを作成できます。これらのオーディエンスは、The Trade Deskとのコネクタアクションで使用されます。この属性をThe Trade Deskコネクタアクションの&#34;Trade Desk ID (TDID)&#34;パラメータにマップします。
