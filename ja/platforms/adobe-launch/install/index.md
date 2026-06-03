---
title: Adobe Launch用Tealiumのインストール
description: Adobe Experience Platform LaunchのTealium Collect拡張機能について学びます。
url: https://docs.tealium.com/ja/platforms/adobe-launch/install/
---
## 必要条件

* [Tealium Customer Data Hubアカウント]()。

## Tealium Collect拡張機能

Adobe Experience Platform LaunchのTealium Collect拡張機能は、すべてのイベントと対応するデータをTealiumに送信します。この拡張機能は、ページごとに一度Tealium CollectのJavaScriptファイルを読み込むカスタムテンプレートです。

トリガーされた各イベントについて、Adobe Experience Platformタグは構成で指定されたデータレイヤーのエンリッチメントオブジェクトをキーと値のペアに自動的にフラット化し、データをTealium Collectエンドポイントに投稿します。ファーストパーティデータ収集を使用する場合は、カスタムエンドポイントを指定できます。

データレイヤー変数がどのようにフラット化されるかの詳細については、[データレイヤー](/ja/platforms/adobe-launch/data-layer/)を参照してください。

## インストール

Tealium Collect拡張機能をインストールするには、以下の手順を実行します：

1. Adobe Experience Platform Launch Marketplaceにアクセスします。
1. **拡張機能**メニューで**カタログ**をクリックし、**Tealium Collect**拡張機能を検索します。
1. **インストール**をクリックします。
1. 次の構成オプションを構成します：
      * **Tealiumアカウント**：（必須）あなたのTealiumアカウント名。
      * **Tealiumプロファイル**：（必須）あなたのTealiumプロファイル名。
      * **データソースキー**：（オプション）サーバーサイドTealium構成からのデータソースキー。
      * **CollectタグURL**：（オプション）デフォルトのTealium Collect URLを独自のファーストパーティデータホストファイルURLで上書きします。例：`https://collect.example.co.uk/collect.min.js`。
      * **エンドポイント**：（オプション）Tealium Collectエンドポイントをファーストパーティデータ収集エンドポイントで上書きします。例：`https://collect.example.co.uk/event`。
      * **データオブジェクト**：（オプション）データレイヤーエンリッチメントオブジェクトとして使用するJavaScript変数の名前。例えば、これをデータレイヤーエンリッチメントオブジェクトとして使用する場合は`digitalData`と入力します。拡張機能は、Direct Callイベントの`_satellite.track`呼び出しの第二パラメータを自動的に使用します。
      * **adobeDataLayerのイベントリスナーを追加**：（オプション）Track Eventアクションのみで使用：adobeDataLayerのイベントを自動的に追跡します。デフォルトおよびカスタムのAdobe Client Data Layerイベントの両方を追跡します。
1. **ライブラリに保存**をクリックします

## アクション

この拡張機能は、Tealium Collectにデータを送信するための2種類のアクションを提供します。それぞれは、サイトのデータレイヤー戦略に応じてAdobe Launchのルールに追加できます。

### Adobe Client Data Layer (ACDL)を使用したイベントの追跡

この拡張機能は、ACDLによってトリガーされたルールのための専用アクションをサポートしています。このアクションを選択すると、プッシュされたオブジェクト（`event.message`）が直接Tealium Collectに渡されます。

#### 動作方法

このアクションは、ACDLからイベントオブジェクトを読み取り、Tealium Collectに送信します。イベント名は、次の優先順位で解決されます：

1. `tealium_event`
2. `event`
3. Launchルール名
4. `type`
5. `eventName`

このアクションは、条件と除外を含む完全なルールレベルの制御を提供します。また、ACDLイベントモデルとのより緊密な整合性を保証します。

#### 使用するシナリオ

次のシナリオでこのアクションを使用します：

* サイトがAdobe Client Data Layer (ACDL)を使用している場合。
* Tealium Collectに送信されるプッシュをより詳細に制御したい場合。
* グローバルイベントリスナーの代わりにACDLトリガーを使用したい場合。

#### 使用例

ACDLデータプッシュに基づいてルールを構成し、ACDLアクションを通じてイベントを追跡します。

![](/images/platforms/adobe-launch/adobe-launch-acdl-rule.png)

### イベントの追跡

このアクションは、ルール条件が満たされたときにイベントデータをTealium Collectに送信します。Adobe Launchのイベントフレームワークを使用し、オプションでデータレイヤープッシュをリスンすることができます。

#### 動作方法

このアクションは、そのルールがトリガーされるたびに実行されます（例えば、ページロードやクリックイベント時）。**イベントリスナーを追加**オプションを構成すると、サイトのデータレイヤーからのイベントを自動的にリスンして転送します。
この拡張機能はページごとに一度Tealium Collectを読み込み、準備ができるまで追加のイベントをキューに入れます。このアプローチはACDLとは独立しており、カスタムまたは非ACDLデータレイヤーを使用するサイトに最適です。

#### 使用するシナリオ

次のシナリオでこのアクションを使用します：

* サイトがJavaScriptオブジェクトまたはカスタムデータレイヤーに直接データをプッシュする場合。
* Adobe Launchルールで完全に定義されたイベントを送信したい場合（例：DOM Ready、Link Click、または`_satellite.track`イベント）。
* ACDLイベントを個別にフィルタリングまたは管理する必要がない場合。

#### 使用例

Tealium Collect拡張機能をトリガーするルールを構成します。次の例では、ページビューイベントのために拡張機能を実行します。

![](/images/platforms/adobe-launch/adobe-launch-rules.png)

#### ダイレクトコール

`_satellite.track`からのダイレクトコールイベントは、**イベントの追跡**アクションを使用するとTealium Collectによって処理されます。データレイヤーの変数`tealium_event`に最初のパラメータが構成され、追加のデータレイヤー属性がTealium Collectエンドポイントに送信される第二パラメータが含まれます。

次の例は、イベント`contact_submit`のためのダイレクトコールです。キーバリューペアのデータレイヤーを使用することをお勧めしますが、ネストされた`adobeDataLayer`オブジェクトも渡すことができます。

```js
_satellite.track(&#34;contact_submit&#34;, { &#34;name&#34;: &#34;John Doe&#34; });
```

Tealium Collectでの結果のイベントは次のようになります：

```json
{
  &#34;tealium_event&#34; : &#34;contact_submit&#34;,
  &#34;name&#34; : &#34;John Doe&#34;
}
```

イベントパラメータに加えて、`_satellite.buildInfo`で見つかった値もダイレクトコールイベントトラッキングのためのデータレイヤーに含まれます：

```json
turbineVersion: &#34;14.0.0&#34;,
turbineBuildDate: &#34;2016-07-01T18:10:34Z&#34;,
buildDate: &#34;2016-03-30T16:27:10Z&#34;,
environment: &#34;development&#34;
```

## ソースコード

カスタム実装が必要な開発者の場合、[拡張機能のコード](https://github.com/Tealium/tealium-collect-adobe-launch-extension)をダウンロードして必要に応じて修正してください。