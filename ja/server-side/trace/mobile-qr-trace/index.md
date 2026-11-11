---
title: Tealium Tools モバイル QR トレース
description: モバイルトレースツールは、デバイスでスキャンできる QR コードを提供することでトレース機能をエンリッチメントし、Tealium Mobile SDK から送信されるイベントをすばやく確認できるようにします。
url: https://docs.tealium.com/ja/server-side/trace/mobile-qr-trace/
---## 仕組み

ツールで **Start Trace** をクリックすると、Customer Data Hub のセッションごとに一度、以降新しいトレースを開始するたびに、メインブラウザーウィンドウへ QR コードが自動的に挿入されます。

QR コードは、各プラットフォーム（[Android](https://docs.tealium.com/platforms/android-kotlin/) または [iOS](https://docs.tealium.com/platforms/ios-swift/)）用に生成されます。対応するモバイルデバイスのカメラで適切な QR コードをスキャンした後、QR コードから取得したリンクをクリックすると、アプリが起動し、トレースパラメータが Tealium SDK に渡されます。Tealium SDK はトレース ID をほかのパラメータとともに受信し、現在のセッションのデータレイヤーに挿入します。

それ以降のすべてのイベントは、セッションを終了するかトレースから離脱するまで、トレースセッションに記録されます。

次の図は、その仕組みを示しています。![](https://docs.tealium.com/images/server-side/screen-shot-2020-09-11-at-3.23.40-pm.png)

## インストール

このツールを使用するには、まず Tealium Tools 拡張機能を使用して Chrome ブラウザーに追加する必要があります。この拡張機能のインストールについては、[Tealium Tools ブラウザー拡張機能](https://docs.tealium.com/tealium-tools-browser-extension/)を参照してください。

**Add by URL** テキストフィールドに、次の URL を貼り付けます：`https://solutions.tealium.net/hosted/tealiumTools/mobile-trace/tool.json`

インストールが完了したら、Tealium Tools 拡張機能から Mobile Trace Tool アイコンを起動します。

## URL スキーム

Mobile Trace Tool を使用するには、Android および iOS アプリが処理する URL を確認し、URL スキームを構成します。

QR コードトレース機能は URL からアプリを起動し、特定のクエリパラメータを待ち受けます。URL からアプリを直接起動するには、特定のドメインを処理するようにアプリが登録されている必要があります。

通常、ほとんどのアプリはすでに特定の URL を処理するように構成されています。たとえば、Web サイトのドメインが `https://mycompany.com` の場合、アプリはこのドメインのハンドラーとして自身を登録します。ユーザーのデバイスにアプリがインストールされている場合、ブラウザー内ではなくアプリでリンクを開くよう促すメッセージがユーザーに表示されます。


<blockquote>
一部のアプリは、`http` や `https` の代わりに、`mycompanyapp://` などのカスタム URL スキームを登録しています。これらも Mobile Trace Tool で使用できます。
</blockquote>


アプリを起動する URL スキームを確認したら、Mobile Trace Tool の入力フィールドに入力します。このツールでは、必要に応じて Android と iOS に異なるスキームを指定できますが、通常は両方のプラットフォームで同じスキームを使用します。

![](https://docs.tealium.com/images/server-side/screen-shot-2020-09-11-at-3.41.58-pm.png)

各 URL スキームの横にある **Save** をクリックすると、構成がブラウザーの localStorage に保存されます。必要に応じて URL スキームを編集するには、青い鉛筆アイコンをクリックします。

## トレース

以下では、Mobile Trace Tool を使用してトレースを開始および離脱する方法について説明します。

### トレースの開始

トレースを開始する前に、サーバーサイドの Customer Data Hub を表示していることを確認します。Mobile Trace Tool で **Start Trace** をクリックすると、新しいトレースが開始され、Mobile Trace の QR コードがトレースウィンドウに追加されます。

![](https://docs.tealium.com/images/server-side/screen-shot-2020-09-11-at-3.46.20-pm.png)

Tealium Tools UI から一度トレースを開始した後は、Tealium Tools UI を閉じることができます。そのセッションの残りの期間では、Tealium Tools UI を使用する必要はありません。

以降のトレースは Customer Data Hub から直接開始でき、新しいトレースを開始するたびに QR コードが自動的に更新されます。デバイスのカメラで QR コードをスキャンし、リンクをクリックしてアプリを起動すると、トレースが自動的に開始されます。トレースに参加した後にアプリによって生成された Tealium イベントは、すべてトレースセッションに記録されます。

![](https://docs.tealium.com/images/server-side/screen-shot-2020-09-11-at-3.48.06-pm.png)

### トレースからの離脱

トレースセッションを終了せずに離脱した場合、そのトレースセッションの履歴を失うことなく、別のデバイスから同じトレースに再参加できます。

トレースから離脱するには、次の手順を実行します。

1. トレース UI で **Leave Trace** チェックボックスを選択します
1. デバイスのカメラでもう一度 QR コードをスキャンします
1. リンクをクリックして、そのデバイスをトレースセッションから離脱させます

### 訪問の終了（Customer Data Platform（CDP））

Customer Data Platform（CDP）で「End of Visit」アクションをテストするには、訪問のセッションを直ちに終了させるシグナルが必要です。それ以外の場合は、セッションが通常どおり期限切れになるまで待つ必要があります。

Mobile Trace Tool でセッションを直ちに終了するには、**Kill Visitor Session** チェックボックスを選択します。これにより、SDK が `kill_visitor_session` イベントを送信するためのパラメータが QR コードに追加されます。

![](https://docs.tealium.com/images/server-side/screen-shot-2020-09-11-at-3.50.27-pm.png)