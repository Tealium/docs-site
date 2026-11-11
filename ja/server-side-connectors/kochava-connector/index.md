---
title: Kochavaコネクタ構成ガイド
description: この記事では、Kochavaコネクタの構成方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/kochava-connector/
---
## コネクタのアクション

| アクション名 | ビジタープロファイル | イベントデータ |
| --- | :---: | :---: |
|インストールイベントを送信| ✗| ✓|
|インストール後イベントを送信| ✗| ✓|

## 構成の構成

コネクタマーケットプレイスに移動し、新しいコネクタを追加します。詳細については、[about-connectors](https://docs.tealium.com/about-connectors/)を参照してください。

## アクション構成 — パラメータとオプション

**続行**をクリックして、コネクタのアクションを構成します。アクション名を入力し、ドロップダウンメニューからアクションタイプを選択します。

次のセクションでは、各アクションのパラメータとオプションを構成する方法について説明します。

### アクション — インストールイベントを送信

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|Kochava App ID|アプリを表すために使用される一意のアプリケーションIDです。<br>詳細については、次の[APIドキュメント](https://support.kochava.com/server-to-server-integration/install-notification-setup)を参照してください。|
|App Version|アプリケーションのバージョン番号を表す文字列です。|
|IP Address|インストール時のデバイスのIPアドレスです。|
|Device Version|デバイスのメーカー、モデル、OSを表す文字列です。構文は `device-os_name-os_version` で、各値をハイフンで区切ります。<br>詳細については、次の[APIドキュメント](https://support.kochava.com/server-to-server-integration/install-notification-setup)を参照してください。|
|Device User Agent|クライアントから提供されたデバイスのユーザーエージェントを表す文字列です。必ずURLエンコードしてください。この文字列は、キャンペーンでフィンガープリントアトリビューションが必要な場合に役立ちます。|
|IDFA|IDFA、IMEI、Android ID、MACアドレス、またはカスタムバリアントのうち、1つ以上のデバイスIDを該当するフィールドに指定する必要があります。|
|IDFV|IDFA、IMEI、Android ID、MACアドレス、またはカスタムバリアントのうち、1つ以上のデバイスIDを該当するフィールドに指定する必要があります。|
|IMEI|IDFA、IMEI、Android ID、MACアドレス、またはカスタムバリアントのうち、1つ以上のデバイスIDを該当するフィールドに指定する必要があります。|
|ADID|IDFA、IMEI、Android ID、MACアドレス、またはカスタムバリアントのうち、1つ以上のデバイスIDを該当するフィールドに指定する必要があります。|
|Android ID|IDFA、IMEI、Android ID、MACアドレス、またはカスタムバリアントのうち、1つ以上のデバイスIDを該当するフィールドに指定する必要があります。|
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

### アクション — インストール後イベントを送信

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|Kochava App ID|アプリを表すために使用される一意のアプリケーションIDです。<br>詳細については、次の[APIドキュメント](https://support.kochava.com/server-to-server-integration/post-install-event-setup)を参照してください。|
|App Version|アプリケーションのバージョン番号を表す文字列です。|
|IP Address|インストール時のデバイスのIPアドレスです。|
|Event Name|追跡するイベントの名前です。|
|Event Data|追跡対象のイベントに関連するデータポイントです。|
|Device Version|デバイスのメーカー、モデル、OSを表す文字列です。構文は `device-os_name-os_version` で、各値をハイフンで区切ります。<br>詳細については、次の[APIドキュメント](https://support.kochava.com/server-to-server-integration/post-install-event-setup)を参照してください。|
|Device User Agent|クライアントから提供されたデバイスのユーザーエージェントを表す文字列です。必ずURLエンコードしてください。この文字列は、キャンペーンでフィンガープリントアトリビューションが必要な場合に役立ちます。|
|IDFA|IDFA、IMEI、Android ID、MACアドレス、またはカスタムバリアントのうち、1つ以上のデバイスIDを該当するフィールドに指定する必要があります。|
|IDFV|IDFA、IMEI、Android ID、MACアドレス、またはカスタムバリアントのうち、1つ以上のデバイスIDを該当するフィールドに指定する必要があります。|
|IMEI|IDFA、IMEI、Android ID、MACアドレス、またはカスタムバリアントのうち、1つ以上のデバイスIDを該当するフィールドに指定する必要があります。|
|ADID|IDFA、IMEI、Android ID、MACアドレス、またはカスタムバリアントのうち、1つ以上のデバイスIDを該当するフィールドに指定する必要があります。|
|Android ID|IDFA、IMEI、Android ID、MACアドレス、またはカスタムバリアントのうち、1つ以上のデバイスIDを該当するフィールドに指定する必要があります。|