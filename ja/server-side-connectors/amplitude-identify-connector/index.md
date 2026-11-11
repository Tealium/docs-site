---
title: Amplitude Identify コネクタ構成ガイド
description: この記事では、Amplitude Identify コネクタの構成方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/amplitude-identify-connector/
---
## API 情報

このコネクタは、次のベンダー API を使用します。

* API 名: Amplitude API
* API バージョン: v2
* API エンドポイント: `https://api2.amplitude.com/identify`
* ドキュメント: [Amplitude Identify API](https://amplitude.com/docs/apis/analytics/identify)

## 構成

コネクタマーケットプレイスに移動し、新しいコネクタを追加します。詳細については、[about-connectors](https://docs.tealium.com/about-connectors/)を参照してください。

コネクタを追加したら、次の項目を構成します。
* **API キー**  
  * プロジェクトの API キー。API キーは、Amplitude インスタンスの **Settings > Projects** にあります。
* **エンドポイント**  
  * エンドポイントを選択するか、エンドポイント URL を入力します。
  * 標準サーバー: `https://api2.amplitude.com/identify`。
  * EU データレジデンシーサーバー: `https://api.eu.amplitude.com/identify`。
  * 指定しない場合は、標準サーバーのエンドポイントがデフォルトで使用されます。

コネクタを構成したら、**Done** をクリックします。

## アクション

| アクション名 | 訪問プロファイル | イベントデータ |
| --- | :---: | :---: |
| ユーザープロパティを更新 | ✓ | ✓ |

アクションの名前を入力し、ドロップダウンメニューからアクションタイプを選択します。

次のセクションでは、各アクションのパラメーターとオプションの構成方法について説明します。

### ユーザープロパティを更新

#### パラメーター

| **パラメーター** | **説明** |
| --- | --- |
| `user_id` | 指定する `UUID`（一意のユーザー `ID`）。Amplitude システムにまだ存在しない `user_id` を使用してリクエストを送信した場合、その `user_id` に関連付けられたユーザーは、最初のイベントが発生するまで新規ユーザーとして記録されません。 |
| `device_id` | iOS のベンダー ID（`IDFV`）など、デバイス固有の識別子。 |
| `app_version` | ユーザーが使用しているアプリのバージョン。 |
| `start_version` | ユーザーが最初に使用したアプリのバージョン。 |
| `groups` | ユーザーグループを表すキーと値のペアのディクショナリ。グループを構成すると、アカウントレベルのレポートを使用できます。最大 `5` 種類の一意のグループタイプと、合計 `10` 個のグループを追跡できます。詳細については、[Amplitude のアカウントレベルのレポート](https://amplitude.com/docs/analytics/account-level-reporting)を参照してください。
<blockquote>
この機能は、アカウントアドオンを購入した Enterprise のお客様のみ利用できます。
</blockquote>
 |
| `language` | ユーザーが構成している言語。 |
| `paying` | ユーザーが有料顧客であるかどうかを指定します。 |

#### 地理情報パラメーター


<blockquote>
次のフィールドはすべて同時に更新する必要があります。いずれかのフィールドを構成すると、同じ Identify 呼び出しで他のフィールドも明示的に構成されていない場合、それらのフィールドは自動的にリセットされます。
</blockquote>


| **パラメーター** | **説明** |
| --- | --- |
| `country` | ユーザーがいる国。 |
| `region` | ユーザーがいる地理的地域。 |
| `city` | ユーザーがいる都市。 |
| `DMA` | ユーザーの指定市場地域。 |

#### デバイスパラメーター

次のフィールドは同時に更新する必要があります。
* `platform`
* `os_name`
* `os_version`
* `device_brand`
* `device_manufacturer`
* `device_model`
* `carrier`


<blockquote>
上記のいずれかのフィールドを構成すると、同じ Identify 呼び出しで他のプロパティ値が明示的に構成されていない場合、それらの値はすべて null にリセットされます。それ以外の場合、プロパティ値は、別の文字列に変更されない限り、またはすべての値が `null` として渡されない限り、後続のイベントでも保持されます。Amplitude は、`device_brand`、`device_manufacturer`、`device_model` を使用して、対応するデバイスタイプへのマッピングを試みます。
</blockquote>


| **パラメーター** | **説明** |
| --- | --- |
| `platform` | データを送信しているプラットフォーム。 |
| `os_name` | ユーザーが使用しているモバイルオペレーティングシステムまたはブラウザー。 |
| `os_version` | ユーザーが使用しているモバイルオペレーティングシステムまたはブラウザーのバージョン。 |
| `device_brand` | ユーザーが使用しているデバイスのブランド。 |
| `device_manufacturer` | ユーザーが使用しているデバイスのメーカー。 |
| `device_model` | ユーザーが使用しているデバイスのモデル。 |
| `carrier` | ユーザーが利用している通信事業者。 |
| `user_properties` | ユーザーに関連付けられたデータを表すキーと値のペアのディクショナリ。個別の値はそれぞれ、Amplitude ダッシュボードにユーザーセグメントとして表示されます。オブジェクトの深さは `40` 階層を超えることはできません。プロパティ値は配列に格納でき、日付値は文字列値に変換されます。 |