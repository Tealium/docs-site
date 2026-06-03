---
title: Podscribe S2S コネクタ構成ガイド
description: この記事では、Podscribe S2S コネクタの構成方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/podscribe-s2s-connector/
---
## API 情報

このコネクタは以下のベンダー API を使用します：

* API 名：Podscribe API
* API エンドポイント：`https://verifi.podscribe.com/tag`
* ドキュメント：[Podscribe API](https://help.podscribe.com/sending-podscribe-conversion-events-/g4g8w3hppouCfkXZdcx6FV/sending-events-server-to-server-s2s-in-batch-or-as-an-img-tag/67UdckfSLHXAPtUAfWDyud)

## 構成

コネクタマーケットプレイスにアクセスし、新しいコネクタを追加します。コネクタの追加方法についての一般的な説明は、[コネクタについて]()を参照してください。

コネクタを追加した後、以下の構成を構成します：
* **API キー**：リクエストを認証するために使用される Podscribe S2S API キー。
* **広告主 ID**：プラットフォームによって割り当てられたユニークな広告主 ID。

## アクション

| アクション名 | AudienceStream | EventStream |
| --- | :---: | :---: |
| イベント送信 | ✓ | ✓ |

アクション名を入力し、ドロップダウンメニューからアクションタイプを選択します。

次のセクションでは、各アクションのパラメータとオプションの構成方法について説明します。

### イベント送信

#### パラメータ

| **パラメータ** | **説明** |
| --- | --- |
| アクション | イベントのタイプ（例：ユーザーアクションやコンバージョン）。&lt;br&gt;view&lt;br&gt;signup&lt;br&gt;lead&lt;br&gt;purchase&lt;br&gt;install&lt;br&gt;offline_purchase |

#### イベントデータ

| **パラメータ** | **説明** |
| --- | --- |
| `event_url` | イベントが発生した URL。 |
| `landing_url` | セッションのランディングページ URL。 |
| `referrer_url` | ユーザーを参照したページの URL。 |
| `campaign_id` | Podscribe キャンペーン ID。 |
| `timestamp` | イベントの UTC タイムスタンプ。 |

#### ユーザーデータ

| **パラメータ** | **説明** |
| --- | --- |
| `ip` | ユーザーの IP アドレス。可能であれば IPv6 を使用。 |
| `ipv4` | IPv6 が利用不可能な場合に使用される IPv4 アドレス。 |
| `user_agent` | ブラウザまたはアプリのユーザーエージェント文字列。 |
| `cookie` | ブラウザのクッキーまたはセッション識別子。 |
| `hashed_email` | ユーザーの SHA256 ハッシュ化されたメールアドレス。ハッシュ化する前にトリムおよび小文字化。 |
| `device_id` | 内部のユーザーまたはデバイス識別子。 |
| `idfa` | Apple 広告 ID (IDFA)。 |
| `gaid` | Google 広告 ID (GAID)。 |
| `is_new_customer` | ユーザーが初めての顧客かどうか。 |
| `is_subscription` | イベントがサブスクリプションに関連しているかどうかを示します。 |

#### メタデータ

| **パラメータ** | **説明** |
| --- | --- |
| `value` | 購入またはコンバージョンの価値。 |
| `currency` | 取引の通貨コード。 |
| `order_number` | ユニークな注文または取引 ID。 |
| `discount_code` | 使用された割引またはプロモーションコード。 |
| `product` | 関与する製品の名前または ID。 |
| `category` | 製品カテゴリを示します。 |
| `channel` | チャネルソースを示します。 |
| 自動マッピングを無効にする | コネクタの自動マッピングを無効にします。|