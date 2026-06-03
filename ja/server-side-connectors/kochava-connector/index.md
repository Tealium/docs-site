---
title: Kochavaコネクタ構成ガイド
description: この記事では、Kochavaコネクタの構成方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/kochava-connector/
---
## コネクタアクション

| アクション名 | AudienceStream | EventStream |
| --- | :---: | :---: |
|インストールイベントの送信| ✗| ✓|
|ポストインストールイベントの送信| ✗| ✓|

## 構成の構成

コネクタマーケットプレイスに移動し、新しいコネクタを追加します。コネクタの追加方法の一般的な指示については、[コネクタについて]()を参照してください。

## アクション構成 - パラメータとオプション

**続行**をクリックしてコネクタアクションを構成します。アクションの名前を入力し、ドロップダウンメニューからアクションタイプを選択します。

次のセクションでは、各アクションのパラメータとオプションの構成方法について説明します。

### アクション - インストールイベントの送信

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|Kochava App ID| アプリを表すユニークなアプリケーションIDです。&lt;br&gt; 詳細については、次の[APIドキュメンテーション](https://support.kochava.com/server-to-server-integration/install-notification-setup)を参照してください|
|App Version| アプリケーションバージョン番号の文字列表現。 |
|IP Address| インストール時のデバイスのIPアドレス。|
|Device Version| デバイスのメーカー、モデル、OSの文字列表現。構文は次のとおりです：`device-os_name-os_version` ここで、各値はハイフンで区切られます。&lt;br&gt; 詳細については、次の[APIドキュメンテーション](https://support.kochava.com/server-to-server-integration/install-notification-setup)を参照してください|
|Device User Agent| クライアントから提供されるデバイスのユーザーエージェントの文字列表現。これがURLエンコードされていることを確認してください。この文字列は、キャンペーンがフィンガープリント属性を必要とする場合に便利です。|
|IDFA| IDFA、IMEI、Android ID、MACアドレス、またはカスタムバリアントのいずれかを適切なフィールドに含める必要があります。|
|IDFV| IDFA、IMEI、Android ID、MACアドレス、またはカスタムバリアントのいずれかを適切なフィールドに含める必要があります。|
|IMEI| IDFA、IMEI、Android ID、MACアドレス、またはカスタムバリアントのいずれかを適切なフィールドに含める必要があります。|
|ADID| IDFA、IMEI、Android ID、MACアドレス、またはカスタムバリアントのいずれかを適切なフィールドに含める必要があります。|
|Android ID| IDFA、IMEI、Android ID、MACアドレス、またはカスタムバリアントのいずれかを適切なフィールドに含める必要があります。|
|iAd Org Name|
|iAd Conversion Date|
|iAd LineItem Name|
|iAd Campaign ID|
|iAd Attribution|
|iAd AdGroup Name|
|iAd Click Date|
|iAd Campaign Name|
|iAd LineItem ID|
|iAd Keyword|
|iAd AdGroup ID|

### アクション - ポストインストールイベントの送信

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|Kochava App ID| アプリを表すユニークなアプリケーションIDです。&lt;br&gt; 詳細については、次の[APIドキュメンテーション](https://support.kochava.com/server-to-server-integration/post-install-event-setup)を参照してください|
|App Version| アプリケーションバージョン番号の文字列表現。 |
|IP Address| インストール時のデバイスのIPアドレス。|
|Event Name| トラックするイベントの名前。|
|Event Data| トラックされるイベントに関連するデータポイント。|
|Device Version| デバイスのメーカー、モデル、OSの文字列表現。構文は次のとおりです：`device-os_name-os_version` ここで、各値はハイフンで区切られます。&lt;br&gt; 詳細については、次の[APIドキュメンテーション](https://support.kochava.com/server-to-server-integration/post-install-event-setup)を参照してください|
|Device User Agent| クライアントから提供されるデバイスのユーザーエージェントの文字列表現。これがURLエンコードされていることを確認してください。この文字列は、キャンペーンがフィンガープリント属性を必要とする場合に便利です。|
|IDFA| IDFA、IMEI、Android ID、MACアドレス、またはカスタムバリアントのいずれかを適切なフィールドに含める必要があります。|
|IDFV| IDFA、IMEI、Android ID、MACアドレス、またはカスタムバリアントのいずれかを適切なフィールドに含める必要があります。|
|IMEI| IDFA、IMEI、Android ID、MACアドレス、またはカスタムバリアントのいずれかを適切なフィールドに含める必要があります。|
|ADID| IDFA、IMEI、Android ID、MACアドレス、またはカスタムバリアントのいずれかを適切なフィールドに含める必要があります。|
|Android ID| IDFA、IMEI、Android ID、MACアドレス、またはカスタムバリアントのいずれかを適切なフィールドに含める必要があります。|
