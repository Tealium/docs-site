---
title: モバイル
description: お使いのモバイルSDKとTealium for Mobileを統合する方法について説明します。
url: https://docs.tealium.com/ja/partners-and-industries/partner-with-us/mobile/
---


貴社がモバイルベンダーで、アプリの使用状況や訪問の行動のトラッキングを行うSDKをお使いの場合や、貴社のSDKをアプリに簡単に追加できるようにタグ管理を使用する場合と同じ便利さをユーザーに提供したい場合は、このガイドをお読みください。Tealium for Mobileと統合して、開発者が既存のTealium実装を活用してネイティブのSDKを簡単にアクティブ化できる方法をご確認ください。

## Tealium for Mobileとは

Tealium for Mobileは、アプリ内のベンダー統合を管理したり、モバイルカスタマーデータをTealium Customer Data Hubに送信することができる総合型ソリューションです。Tealiumユーザーは、ネイティブアプリによるタグ管理の利点と、Tealium EventStreamおよびTealium AudienceStreamによるサーバー側データ管理の威力を同時に利用できます。

[Tealium for Mobileの詳細については、こちらを参照してください](https://docs.tealium.com/ja/platforms/getting-started/)。

## リモートコマンド

リモートコマンドは、サードパーティのSDKを読み込むためのネイティブソリューションを提供する統合機能です。Tag Managementを使用してトラッキングオプションを構成する便利さはそのままで、アプリの再送信も必要ありません。

モバイル実装を利用するTealiumユーザーは、機能を統合するためのリモートコマンドを追加するだけで、SDKの機能を追加できます。リモートコマンドモジュールは、Tealiumのメインライブラリによってトラッキングされるカスタマーデータおよびイベントを、対応するSDKのメソッドに渡します。

これにより、ほとんど同じようなデータのトラッキングを行う複数のSDKを管理する面倒がなくなり、SDKの実装が容易になります。

[リモートコマンドの詳細については、こちらを参照してください](https://docs.tealium.com/ja/platforms/remote-commands/)。

## FAQ

**リモートコマンド統合には、どのような制限がありますか？**

モバイル開発では、Tealiumで提供されていないSDK機能の実装が必要になることがあります。以下は、直接実装する必要がある機能の例です。

* アプリ内パーソナライゼーション
* プッシュ通知
* アンインストールトラッキング

**リモートコマンドモジュールは、選択的に初期化できますか？**

はい、Tag Managementのタグ配信ルールを使用して、ベンダーSDKを初期化するタイミングを制御できます。

## パートナーになる

貴社のテクノロジーを統合する方法については、[お問い合わせください](https://community.tealiumiq.com/t5/Become-a-Technology-Partner/bd-p/become-a-technology-partner) 。
