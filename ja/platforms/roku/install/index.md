---
title: インストール
description: Tealium for Rokuのインストールについて説明します。
url: https://docs.tealium.com/ja/platforms/roku/install/
---このガイドでは、ユーザーのアクティビティをトラッキングするために、TealiumをRokuアプリに追加する方法を説明します。はじめに、このプラットフォームの紹介動画をご覧ください。



## 要件

* [Tealium Customer Data Hubアカウント](https://community.tealiumiq.com/t5/Customer-Data-Hub/Introduction-to-Customer-Data-Hub/ta-p/17571)
* [Roku SDK](https://sdkdocs.roku.com/display/sdkdoc/Release&#43;Notes) 7.2以降
* アクティブな[Roku開発者アカウント](https://developer.roku.com/developer)
* Rokuデバイス

[RokuプラグインをインストールしたEclipse](https://blog.roku.com/developer/2016/11/17/eclipse-plugin-update/)で開発することをお勧めします。

## サンプルアプリ

当社のライブラリ、トラッキングメソッド、ベストプラクティスの実装に精通していただけるよう、[Rokuサンプルアプリ](https://github.com/Tealium/tealium-roku/tree/master/sample_app)をダウンロードすることをお勧めします。

サンプルアプリのコードは[`main.brs`](https://github.com/Tealium/tealium-roku/blob/master/sample_app/source/application/main.brs)ファイルから入手できます。コールバック関数のトラッキングと定義を行うボタンを追加する例をこのアプリで確認できます。

## インストール

コードのインストールとセットアップの概要については、以下の動画をご確認ください。



Roku向けTealiumライブラリをインストールするには：

1. GitHubから[Tealium for Roku](https://github.com/tealium/tealium-roku)をダウンロードしてインストールします。このコードはサンプルアプリとして構成されています。Tealiumのコードファイルは`sample_app/source/tealium`にあります。
今後のリリースに向けたアップデートをしやすくするため、ライブラリを（ダウンロードではなく）クローンすることを推奨しています。

2. 以下のファイルをプロジェクトのソースフォルダにインポートする必要があります。
  * `tealium.brs`
  * `tealiumCollect.brs`
  * `tealiumLog.brs`

3. Eclipseを使用している場合は、Tealiumコンポーネントにアクセスするためにプロジェクトをリフレッシュします。


## 初期化

次の例に示すように、Tealiumオブジェクトは[`TealiumBuilder()`](/ja/platforms/roku/api/#tealiumbuilder)コンストラクタによって初期化されます。

```javascript
builder = TealiumBuilder(&#34;ACCOUNT&#34;, &#34;PROFILE&#34;, LOG_LEVEL)
builder.SetEnvironment(&#34;ENVIRONMENT&#34;)
builder.SetDatasource(&#34;DATASOURCE&#34;)
teal = builder.Build()
```

本番環境にリリースする際は、適切なログレベルを構成してください。

