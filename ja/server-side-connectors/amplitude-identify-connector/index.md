---
title: Amplitude Identifyコネクタ構成ガイド
description: この記事では、Amplitude Identifyコネクタの構成方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/amplitude-identify-connector/
---
## API情報

このコネクタは以下のベンダーAPIを使用します：

* API名：Amplitude API
* APIバージョン：v2
* APIエンドポイント：`https://api2.amplitude.com/identify`
* ドキュメンテーション：[Amplitude Identify API](https://amplitude.com/docs/apis/analytics/identify)


## 構成

コネクタマーケットプレイスに移動し、新しいコネクタを追加します。コネクタの追加方法の一般的な指示については、[About Connectors](https://docs.tealium.com/about-connectors/)を参照してください。

コネクタを追加した後、以下の構成を行います：
* **APIキー**  
  * プロジェクトのAPIキー。APIキーはAmplitudeインスタンスの**構成 > プロジェクト**の下にあります。
* **エンドポイント**  
  * エンドポイントを選択するか、エンドポイントURLを入力します。
  * 標準サーバー：`https://api2.amplitude.com/identify`.
  * EU居住者サーバー：`https://api.eu.amplitude.com/identify`.
  * 提供されていない場合、デフォルトで標準サーバーエンドポイントを使用する必要があります。

## アクション

| アクション名 | AudienceStream | EventStream |
| --- | :---: | :---: |
| ユーザープロパティの更新 | ✓ | ✓ |

アクションの名前を入力し、ドロップダウンメニューからアクションタイプを選択します。

次のセクションでは、各アクションのパラメータとオプションの構成方法について説明します。

### ユーザープロパティの更新

#### パラメータ

| **パラメータ** | **説明** |
| --- | --- |
| `user_id` | 指定する`UUID`（ユニークなユーザー`ID`）。Amplitudeシステムにまだ存在しない`user_id`でリクエストを送信すると、その`user_id`に紐づけられたユーザーは、最初のイベントまで新規とはマークされません。 |
| `device_id` | デバイス固有の識別子、例えばiOSのベンダーの識別子（`IDFV`）。 |
| `app_version` | ユーザーが使用しているアプリのバージョン。 |
| `start_version` | ユーザーが最初に使用していたアプリのバージョン。 |
| `groups` | ユーザーグループを表すキーと値のペアの辞書。グループを構成することで、アカウントレベルのレポーティングを使用できます。最大`5`種類のユニークなグループタイプと`10`の合計グループを追跡できます。詳細については、[Amplitudeのアカウントレベルレポーティング](https://amplitude.com/docs/analytics/account-level-reporting)を参照してください。
<blockquote>
この機能は、アカウント追加オプションを購入したエンタープライズ顧客のみが利用可能です。
</blockquote>
 |
| `language` | ユーザーが構成した言語。 |
| `paying` | ユーザーが支払いを行っているかどうかを指定します。 |

#### 地理的なパラメータ


<blockquote>
以下のすべてのフィールドを一緒に更新する必要があります。これらのフィールドのいずれかを構成すると、同じ識別呼び出しで明示的に構成されていない他のフィールドは自動的にリセットされます。
</blockquote>


| **パラメータ** | **説明** |
| --- | --- |
| `country` | ユーザーがいる国。 |
| `region` | ユーザーがいる地理的な地域。 |
| `city` | ユーザーがいる都市。 |
| `DMA` | ユーザーの指定市場エリア。 |

#### デバイスパラメータ

以下のフィールドを一緒に更新する必要があります：
* `platform`
* `os_name`
* `os_version`
* `device_brand`
* `device_manufacturer`
* `device_model`
* `carrier`


<blockquote>
上記のフィールドのいずれかを構成すると、同じ識別呼び出しで明示的に構成されていない他のプロパティ値はすべてnullにリセットされます。それ以外の場合、プロパティ値は値が異なる文字列に変更されない限り、またはすべての値が`null`として渡されない限り、後続のイベントに持続します。Amplitudeは`device_brand`、`device_manufacturer`、`device_model`を使用して対応するデバイスタイプをマッピングしようとします。
</blockquote>


| **パラメータ** | **説明** |
| --- | --- |
| `platform` | データを送信しているプラットフォーム。 |
| `os_name` | ユーザーが使用しているモバイルオペレーティングシステムまたはブラウザ。 |
| `os_version` | ユーザーが使用しているモバイルオペレーティングシステムまたはブラウザのバージョン。 |
| `device_brand` | ユーザーが使用しているデバイスのブランド。 |
| `device_manufacturer` | ユーザーが使用しているデバイスの製造元。 |
| `device_model` | ユーザーが使用しているデバイスのモデル。 |
| `carrier` | ユーザーが契約しているキャリア。 |
| `user_properties` | ユーザーに関連付けられたデータを表すキーと値のペアの辞書。各異なる値はAmplitudeダッシュボード上のユーザーセグメントとして表示されます。オブジェクトの深さは`40`レイヤーを超えてはなりません。プロパティ値を配列に保存でき、日付値は文字列値に変換されます。 |
