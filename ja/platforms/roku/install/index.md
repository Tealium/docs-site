---
title: インストール
description: Tealium for Rokuのインストールについて説明します。
url: https://docs.tealium.com/ja/platforms/roku/install/
---このガイドでは、ユーザーのアクティビティをトラッキングするために、TealiumをRokuアプリに追加する方法を説明します。はじめに、このプラットフォームの紹介動画をご覧ください。



## 要件

* [Tealium Customer Data Hubアカウント](https://community.tealiumiq.com/t5/Customer-Data-Hub/Introduction-to-Customer-Data-Hub/ta-p/17571)
* [Roku SDK](https://sdkdocs.roku.com/display/sdkdoc/Release+Notes) 7.2以降
* アクティブな[Roku開発者アカウント](https://developer.roku.com/developer)
* Rokuデバイス


<blockquote>
[RokuプラグインをインストールしたEclipse](https://blog.roku.com/developer/2016/11/17/eclipse-plugin-update/)で開発することをお勧めします。
</blockquote>


## サンプルアプリ

当社のライブラリ、トラッキングメソッド、ベストプラクティスの実装に精通していただけるよう、[Rokuサンプルアプリ](https://github.com/Tealium/tealium-roku/tree/master/sample_app)をダウンロードすることをお勧めします。

サンプルアプリのコードは[`main.brs`](https://github.com/Tealium/tealium-roku/blob/master/sample_app/source/application/main.brs)ファイルから入手できます。コールバック関数のトラッキングと定義を行うボタンを追加する例をこのアプリで確認できます。

## インストール

コードのインストールとセットアップの概要については、以下の動画をご確認ください。



Roku向けTealiumライブラリをインストールするには：

1. GitHubから[Tealium for Roku](https://github.com/tealium/tealium-roku)をダウンロードしてインストールします。このコードはサンプルアプリとして構成されています。Tealiumのコードファイルは`sample_app/source/tealium`にあります。

<blockquote>
今後のリリースに向けたアップデートをしやすくするため、ライブラリを（ダウンロードではなく）クローンすることを推奨しています。
</blockquote>


2. 以下のファイルをプロジェクトのソースフォルダにインポートする必要があります。
  * `tealium.brs`
  * `tealiumCollect.brs`
  * `tealiumLog.brs`

3. Eclipseを使用している場合は、Tealiumコンポーネントにアクセスするためにプロジェクトをリフレッシュします。


## 初期化

次の例に示すように、Tealiumオブジェクトは[`TealiumBuilder()`](https://docs.tealium.com/ja/platforms/roku/api/#tealiumbuilder)コンストラクタによって初期化されます。

```javascript
builder = TealiumBuilder("ACCOUNT", "PROFILE", LOG_LEVEL)
builder.SetEnvironment("ENVIRONMENT")
builder.SetDatasource("DATASOURCE")
teal = builder.Build()
```


<blockquote>
本番環境にリリースする際は、適切なログレベルを構成してください。
</blockquote>


