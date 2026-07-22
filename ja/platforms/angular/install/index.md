---
title: インストール
description: Tealium SDKをAngularにインストールする方法を学びます。
url: https://docs.tealium.com/ja/platforms/angular/install/
---このサンプルは[Angular CLI Quickstart](https://angular.io/docs/ts/latest/cli-quickstart.html)に基づいています。

## 要件

*   Tealium iQタグ管理アカウント
*   Angularアプリケーション

## サンプルアプリ

Tealiumライブラリ、トラッキング方法、ベストプラクティスの実装について理解を深めるために、Tealium for Angularの[サンプルアプリ](https://github.com/Tealium/integration-angular)を探索してみてください。

## インストール

インストールには、アプリケーションに1つのファイルを追加するだけで済みます。このサービスは、アカウントのTealium `utag.js`ライブラリをロードし、トラッキング呼び出しを処理します。

Angular用のTealiumライブラリをインストールするには：

1. Angularアプリケーションでディレクトリ`./src/app/tealium`を作成します。

2. ファイル[utag.service.ts](https://github.com/Tealium/integration-angular/tree/master/example/src/app/tealium)をアプリケーションのパス`./src/app/tealium/`にコピーします。

3. サンプルアプリの[`app.compontent.ts`](https://github.com/Tealium/integration-angular/blob/master/example/src/app/app.component.ts)ファイルにある例に従って、アプリでTealiumサービスを定義し、呼び出します。

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

[`setConfig()`](https://docs.tealium.com/ja/platforms/angular/api/#setconfig)メソッドはTealiumを初期化し、`utag.js`ファイルへのパスを構築します。以下の例を参照してください：

```ruby
constructor(private tealium: TealiumUtagService) {
    this.tealium.setConfig({
        "account"     : "ACCOUNT",
        "profile"     : "PROFILE",
        "environment" : "ENVIRONMENT"});
}
```
インストールにより、アプリケーションに新しいクラス`TealiumUtagService`が追加され、これはコンポーネントにプロバイダとして登録することで利用可能になります。

## 例

以下は、Tealiumサービスをアプリケーションにインポートする完全な例です。[`app.component.ts`](https://github.com/Tealium/integration-angular/blob/master/example/src/app/app.component.ts)。

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
