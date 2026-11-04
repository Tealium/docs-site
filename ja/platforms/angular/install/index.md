---
title: インストール
description: Angular向けTealium SDKのインストール方法について説明します。
url: https://docs.tealium.com/ja/platforms/angular/install/
---このサンプルは、[Angular CLIクイックスタート](https://angular.io/docs/ts/latest/cli-quickstart.html)に基づいています。

## 要件

*   タグ管理アカウント
*   Angularアプリケーション

## サンプルアプリ

Tealiumライブラリ、トラッキングメソッド、実装のベストプラクティスについて理解を深めるには、Tealium for Angularの[サンプルアプリ](https://github.com/Tealium/integration-angular)を参照してください。


## インストール

インストールでは、アプリケーションにファイルを1つ追加するだけです。このサービスは、アカウント用のTealium `utag.js` ライブラリの読み込みと、トラッキング呼び出しの処理を行います。

Angular向けTealiumライブラリをインストールするには、次の手順を実行します。

1. Angularアプリケーション内にディレクトリ `./src/app/tealium` を作成します。

2. ファイル[utag.service.ts](https://github.com/Tealium/integration-angular/tree/master/example/src/app/tealium)を、アプリケーションのパス `./src/app/tealium/` にコピーします。

3. サンプルアプリの [`app.compontent.ts`](https://github.com/Tealium/integration-angular/blob/master/example/src/app/app.component.ts) ファイルにある例に従って、アプリ内でTealiumサービスを定義し、呼び出します。

      ```ruby
      import { Component, OnInit } from '@angular/core';
      import { TealiumUtagService } from './tealium/utag.service';

      @Component({
            selector: 'app-root',
            providers: [TealiumUtagService],
            templateUrl: './app.component.html',
            styleUrls: ['./app.component.css']
      })
      ```

## 初期化

次の例に示すように、[`setConfig()`](https://docs.tealium.com/ja/platforms/angular/api/#setconfig) メソッドはTealiumを初期化し、`utag.js` ファイルへのパスを構築します。

```ruby
constructor(private tealium: TealiumUtagService) {
    this.tealium.setConfig({
        "account"     : "ACCOUNT",
        "profile"     : "PROFILE",
        "environment" : "ENVIRONMENT"});
}
```

インストールにより、`TealiumUtagService` という新しいクラスがアプリケーションに追加されます。このクラスは、コンポーネントにプロバイダーとして登録することで使用できます。


## 例

次に、Tealiumサービスをアプリケーションにインポートする完全な例を示します（[`app.component.ts`](https://github.com/Tealium/integration-angular/blob/master/example/src/app/app.component.ts)）。

```ruby
import { Component, OnInit } from '@angular/core';
import { TealiumUtagService } from './tealium/utag.service';

@Component({
  selector: 'app-root',
  providers: [TealiumUtagService],
  templateUrl: './app.component.html',
  styleUrls: ['./app.component.css']})

export class AppComponent implements OnInit {

  title = 'Testing App';

  constructor(private tealium: TealiumUtagService) {
    this.tealium.setConfig({ account: '##TEALIUM_ACCOUNT##', profile: '##TEALIUM_PROFILE##', environment: 'prod' });
  }

  ngOnInit(): void {
    // The tealium.view function will call the tealium.track function with 'view' as first param
    // Most tags support the 'view' event and many analytics tags also support the 'link' event
    this.tealium.view({event_name: 'init'});
    //this.tealium.track('view', {'event_name' : 'init'});
  }
}
```