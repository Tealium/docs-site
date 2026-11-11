---
title: Podscribe S2Sコネクタ構成ガイド
description: Podscribe S2Sコネクタを構成し、アトリビューションのためにサーバーサイドのコンバージョンイベントをPodscribeへ送信します。
url: https://docs.tealium.com/ja/server-side-connectors/podscribe-s2s-connector/
---
## API情報

このコネクタは、以下のベンダーAPIを使用します。

* API名：Podscribe API
* APIエンドポイント：`https://verifi.podscribe.com/tag`
* ドキュメント：[Podscribe API](https://help.podscribe.com/sending-podscribe-conversion-events-/g4g8w3hppouCfkXZdcx6FV/sending-events-server-to-server-s2s-in-batch-or-as-an-img-tag/67UdckfSLHXAPtUAfWDyud)

## 構成

コネクタマーケットプレイスに移動し、新しいコネクタを追加します。詳細については、[about-connectors](https://docs.tealium.com/about-connectors/)を参照してください。

コネクタを追加した後、以下を構成します。

* **APIキー**：（必須）リクエストの認証に使用するPodscribe S2S APIキー。
* **広告主ID**：（必須）プラットフォームによって割り当てられた一意の広告主ID。
* **ユーザーID**：（必須）すべてのイベントリクエストで送信されるユーザー識別子。

コネクタを構成したら、**完了**をクリックします。

## アクション

| アクション名 | 訪問プロファイル | イベントデータ |
| --- | :---: | :---: |
| イベントを送信 | ✓ | ✓ |

アクションの名前を入力し、ドロップダウンメニューからアクションタイプを選択します。

### イベントを送信

#### パラメーター

| **パラメーター** | **説明** |
| --- | --- |
| アクション | イベントのタイプ（ユーザーアクションやコンバージョンなど）。<br>`view`<br>`signup`<br>`lead`<br>`purchase`<br>`install`<br>`offline_purchase` |

#### イベントデータ

| **パラメーター** | **説明** |
| --- | --- |
| `event_url` | イベントが発生したURL。 |
| `landing_url` | セッションのランディングページURL。 |
| `referrer` | ユーザーの参照元ページのURL。 |
| `campaign_id` | PodscribeのキャンペーンID。 |
| `timestamp` | イベントのUTCタイムスタンプ。 |

#### ユーザーデータ

| **パラメーター** | **説明** |
| --- | --- |
| `ip` | ユーザーのIPv6アドレス。IPv4より優先されます。`ip`が空で`ipv4`に値が構成されている場合、コネクタは両方のフィールドに`ipv4`の値を送信します。 |
| `ipv4` | ユーザーのIPv4アドレス。 |
| `user_agent` | ブラウザーまたはアプリのユーザーエージェント文字列。 |
| `cookie` | ブラウザーCookieまたはセッション識別子。 |
| `hashed_email` | ユーザーのSHA256ハッシュ化されたメールアドレス。ハッシュ化する前に、前後の空白を削除して小文字に変換してください。 |
| `device_id` | 内部ユーザーまたはデバイスの識別子。 |
| `idfa` | Apple広告ID（IDFA）。 |
| `gaid` | Google広告ID（GAID）。 |
| `is_new_customer` | ユーザーが初回購入者かどうか。 |
| `is_subscription` | イベントにサブスクリプションが含まれるかどうかを示します。 |

#### メタデータ

| **パラメーター** | **説明** |
| --- | --- |
| `value` | 購入額またはコンバージョン値。 |
| `currency` | 取引の通貨コード。 |
| `order_number` | 一意の注文IDまたは取引ID。 |
| `discount_code` | 使用された割引コードまたはプロモーションコード。 |
| `product` | 対象となる商品の名前またはID。 |
| `category` | イベントの商品またはコンテンツのカテゴリー。 |
| `channel` | イベントのトラフィックチャネルソース。 |
| **Eコマースの自動マッピングを無効化** | Eコマースフィールド（`value`、`currency`、`order_number`、`discount_code`、`product`、`category`）の自動マッピングを抑制します。明示的な直接マッピングは引き続き適用されます。この構成にかかわらず、`view`イベントではEコマースフィールドが自動的にマッピングされることはありません。 |
| **識別子の自動マッピングを無効化** | 識別子およびコンテキストフィールド（`ip`、`ipv4`、`user_agent`、`event_url`、`referrer`、`timestamp`、`cookie`）の自動マッピングを抑制します。明示的な直接マッピングは引き続き適用されます。 |