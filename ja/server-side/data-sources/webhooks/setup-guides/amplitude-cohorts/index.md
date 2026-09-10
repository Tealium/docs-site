---
title: Amplitude コホートデータソース構成ガイド
description: Amplitude からコホートメンバーシップの更新を受け取るために Tealium で Amplitude コホートデータソースを構成する方法。
url: https://docs.tealium.com/ja/server-side/data-sources/webhooks/setup-guides/amplitude-cohorts/
---
Amplitude コホートデータソースは、Amplitude からあなたの Tealium プロファイルにコホートメンバーシップの更新を送信することを可能にします。コホートメンバーシップイベントはフラット化されたイベントとして到着し、ルール、エンリッチメント、およびオーディエンスで使用できます。

## 要件

Amplitude コホートデータソースは、Destinations カタログへのアクセスを持つ Amplitude アカウントを必要とします。

## 動作方法

Amplitude がコホートを同期するとき、Amplitude コホートデータソースエンドポイントにメンバーシップ更新を送信します。初期同期では完全なコホートメンバーシップが送信されます。その後の同期では、コホートに追加または削除されたユーザーのみのメンバーシップ変更が送信されます。

データは Amplitude から Tealium へのみ流れます。Tealium はデータを Amplitude に送り返しません。

受信 URL には一意のデータソースキーが含まれています。エンドポイントは認証ヘッダーを必要としません。

## Tealium でデータソースを構成する

Amplitude コホートデータソースを作成するには、[データソースについて](https://docs.tealium.com/about-data-sources/)を参照してください。

データソースを作成した後、**コード取得**画面に Amplitude を構成するために必要な値が表示されます：

* **アカウント名：** あなたの Tealium アカウント名。
* **プロファイル名：** あなたの Tealium プロファイル名。
* **データソースキー：** あなたのデータソースキー。
* **リージョン：** あなたの Tealium collect サブドメイン（例：`collect-eu-central-1.tealiumiq.com/`）。

プロファイルを保存して公開し、データソースをアクティブにします。

## Amplitude を構成する

Tealium でデータソースを構成した後、Amplitude のデスティネーションを構成します：

1. Amplitude で **データ > カタログ > デスティネーション** に移動します。
1. **Amplitude コホート (Tealium)** デスティネーションを開きます。
1. Tealium データソースからの **アカウント名**、**プロファイル名**、**データソースキー**、および **リージョン** の値を入力します。
1. デスティネーションを保存します。

## イベントと属性

Amplitude はコホートメンバーシップデータを JSON オブジェクトの配列として送信します。Tealium は各オブジェクトを単一レベルのイベントにフラット化します。

Amplitude は Tealium 属性以外のすべての属性に `amp_` を接頭辞として付けます。`tealium_visitor_id` と `tealium_event` フィールドには接頭辞が付けられません。

Tealium はまた、アンダースコアで区切られたキーを使用してネストされたオブジェクトをフラット化します。たとえば、`amp_user_props` の `email` プロパティは `amp_user_props_email` になります。

`amp_status` フィールドは、ユーザーがコホートに追加されたか削除されたかを示します。`true` の値はユーザーがコホートに追加されたことを意味し、`false` の値はユーザーが削除されたことを意味します。

Amplitude は次の形式でペイロードを送信します：

```json
[
  {
    "tealium_visitor_id": "abc123def456",
    "tealium_event": "amplitude_cohort_sync",
    "amp_cohort_id": "rg123456",
    "amp_cohort_name": "High Value Users",
    "amp_status": true,
    "amp_user_props": {
      "email": "user@example.com",
      "country": "US",
      "plan": "premium"
    }
  }
]
```

Tealium はペイロードを次のイベントにフラット化します：

```json
{
  "tealium_visitor_id": "abc123def456",
  "tealium_event": "amplitude_cohort_sync",
  "amp_cohort_id": "rg123456",
  "amp_cohort_name": "High Value Users",
  "amp_status": true,
  "amp_user_props_email": "user@example.com",
  "amp_user_props_country": "US",
  "amp_user_props_plan": "premium"
}
```

次の表は、主要なイベント属性を説明しています。

| 属性 | タイプ | 説明 |
|---|---|---|
| `tealium_event` | 文字列 | イベント名。値は `amplitude_cohort_sync` です。 |
| `tealium_visitor_id` | 文字列 | Amplitude から渡される訪問識別子。 |
| `amp_cohort_id` | 文字列 | Amplitude コホートの一意の識別子。 |
| `amp_cohort_name` | 文字列 | Amplitude コホートの名前。 |
| `amp_status` | ブール | コホートメンバーシップの変更を示します。`true` はユーザーがコホートに追加されたことを意味し、`false` はユーザーが削除されたことを意味します。 |
| `amp_user_props_*` | さまざま | フラット化されたユーザー属性。たとえば、`amp_user_props_email`。 |

## ベンダー文書

* [Amplitude: コホート同期統合を作成する](https://amplitude.com/docs/partners/create-a-cohort-sync-integration)
* [Amplitude: 行動コホートを受け取る](https://amplitude.com/docs/partners/receiving-behavioral-cohorts)