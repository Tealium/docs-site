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
      import { Component, OnInit } from &#39;@angular/core&#39;;
      import { TealiumUtagService } from &#39;./tealium/utag.service&#39;;

      @Component({
            selector: &#39;app-root&#39;,
            providers: [TealiumUtagService],
            templateUrl: &#39;./app.component.html&#39;,
            styleUrls: [&#39;./app.component.css&#39;]
      })
      ```

## 初期化

[`setConfig()`](/ja/platforms/angular/api/#setconfig)メソッドはTealiumを初期化し、`utag.js`ファイルへのパスを構築します。以下の例を参照してください：

```ruby
constructor(private tealium: TealiumUtagService) {
    this.tealium.setConfig({
        &#34;account&#34;     : &#34;ACCOUNT&#34;,
        &#34;profile&#34;     : &#34;PROFILE&#34;,
        &#34;environment&#34; : &#34;ENVIRONMENT&#34;});
}
```
インストールにより、アプリケーションに新しいクラス`TealiumUtagService`が追加され、これはコンポーネントにプロバイダとして登録することで利用可能になります。

## 例

以下は、Tealiumサービスをアプリケーションにインポートする完全な例です。[`app.component.ts`](https://github.com/Tealium/integration-angular/blob/master/example/src/app/app.component.ts)。

```ruby
import { Component, OnInit } from &#39;@angular/core&#39;;
import { TealiumUtagService } from &#39;./tealium/utag.service&#39;;

@Component({
  selector: &#39;app-root&#39;,
  providers: [TealiumUtagService],
  templateUrl: &#39;./app.component.html&#39;,
  styleUrls: [&#39;./app.component.css&#39;]})

export class AppComponent implements OnInit {

  title = &#39;Testing App&#39;;

  constructor(private tealium: TealiumUtagService) {
    this.tealium.setConfig({ account: &#39;##TEALIUM_ACCOUNT##&#39;, profile: &#39;##TEALIUM_PROFILE##&#39;, environment: &#39;prod&#39; });
  }

  ngOnInit(): void {
    // The tealium.view function will call the tealium.track function with &#39;view&#39; as first param
    // Most tags support the &#39;view&#39; event and many analytics tags also support the &#39;link&#39; event
    this.tealium.view({event_name: &#39;init&#39;});
    //this.tealium.track(&#39;view&#39;, {&#39;event_name&#39; : &#39;init&#39;});
  }
}
```
