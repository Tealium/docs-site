---
title: デバッグ
description: トラッキングコールのデバッグの基本を学びます。
url: https://docs.tealium.com/ja/platforms/javascript/debugging/
---
関数 `utag.view()` と `utag.link()` は、それぞれページビューとイベントをトラッキングするために使用されます。この記事では、これらの関数をデバッグして、いつ、どのように呼び出され、どのようなデータが処理されているかを確認する方法を示します。

## デバッグモード

デバッグモードを有効にするには、ブラウザの開発者コンソールを開き、次のコマンドを実行します：

```js
document.cookie=&#34;utagdb=true; path=/&#34;;
```

このクッキーはデバッグモードをオンにし、コンソールに有用な出力を生成します。

![](/images/platforms/javascript/console-output.png)

デバッグモードが有効になると、トラッキングコールが発生するときにコンソールにログステートメントが表示されます。これらのステートメントをコンソール出力で探します：

```none
trigger: view
trigger: link
```

次の例は、イベントがトラッキングされた後のコンソールの様子を示しています：

![](/images/platforms/javascript/debugging-console-utag-link.png)

`trigger:view` または `trigger:link` の後の行をクリックして、イベントデータオブジェクトの展開と折りたたみを行います。

## ブレークポイント

より深いデバッグのためには、`utag.js` にブレークポイントを構成して、トラッキングコールが発生したときにコードを一時停止すると便利です。ブレークポイントを使用して、トラッキングデータオブジェクトを調査したり、コールが発生した場所を確認するためにスタックトレースを調査します。

Chrome DevToolsを使用してブレークポイントを構成するには：

1. DevToolsを開き、**Sources** タブに移動して、ファイル `utag.js` を開きます。
1. `return this.track(` という行を見つけて、行番号をクリックしてブレークポイントを構成します：  
      ![](/images/platforms/javascript/debugging-utag-code.png)
4. メインウィンドウに戻り、トラッキングコールをトリガーするアクションを実行します。トラッキングコールが実行されると、コードはブレークポイントで一時停止します。
5. 右パネルで、**Watch** パネルを展開し、**&#43;** サインをクリックしてウォッチ式を追加します。`a` と入力して **Enter** をクリックし、この変数のウォッチ式を追加します。
6. パラメータ `a` に含まれるオブジェクトを展開して、トラッキングコールに渡されたデータを表示します。このデータは拡張機能、ロードルール、データマッピングで利用可能です。
7. 右パネルで、**Call Stack** パネルを展開して、トラッキングコールがどこから発生したかを確認します。

次に、`utag.link()` コールの場所を探す例を示します：

![](/images/platforms/javascript/utag-link-call-stack.png)

この例は、`utag.link()` コールをデバッグするために設置された `utag.js` のブレークポイントを示しています。項目 (2) をクリックすると、ソースコード内で行われた `utag.link()` コールが表示されます（左側）。 

これで、次の三つのことをデバッグすることができました：

*   ブレークポイントがヒットしたかどうか。もしヒットした場合、関数が正しくトリガーされるように構成されています。
*   ブレークポイントがヒットしたので、`utag.view()` または `utag.link()` が呼び出されたときにどのようなデータが送信されたかを確認することができました。
*   `utag.view()` または `utag.link()` の実際の構成を確認することができました。

特定のイベントがトリガーされたときに正しいデータが渡されていない場合、この情報は役立ちます。関数に渡されるデータが間違っている可能性があります。

詳細については、[Chrome DevTools: JavaScript debugging](https://developer.chrome.com/docs/devtools/javascript/reference/) を参照してください。

## コンソール出力

次の表は、コンソールに表示される重要なデバッグステートメントのいくつかを説明しています。あなたのサイトのデバッグ出力は、`utag.js`のバージョンや特定の構成によって若干異なる場合があります。

| デバッグステートメント | 説明 |
| ------------- | ----------- |
| `Pre-INIT` | **Pre Loader** にスコープされた拡張機能が実行されます。 |
| `PINIT` | **Before Load Rules** にスコープされた拡張機能が実行され、ロードルールが評価され、タグがロードされます。 |
| `utag.loader.RD` | ページからデータレイヤー変数が読み取られます（[data layer variable types]()を参照）。 |
| `utag.loader.INIT`| **After Load Rules** にスコープされた拡張機能が実行され、タグがロードされます。  |
| `All Tags EXTENSIONS`| **After Load Rules** にスコープされた拡張機能が実行されます。 |
| `utag.loader.INIT: waiting &lt;UID&gt;` | タグ (UID) が DOM Ready でロードされるように構成され、キューに追加されます。  |
| `READY:utag.cfg.readywait` | DOM Ready が発生し、`PINIT` が実行されます。 |
| `READY:utag.cfg.wq` | DOM Ready が発生し、キューに入れられたタグが処理されます。 |
| `WQ: #` | DOM Ready を待っているタグのキュー内の数です。 |
| `Attach to head` | タグスクリプトがソースコードに追加されます。|
| `utag.loader.LOAD &lt;UID&gt;` | タグ (UID) がページ上でロードされました。 |
| `Sending: &lt;UID&gt;` | タグ (UID) がベンダーへのコールをトリガーしています。 |
| `trigger:view` | `utag.view()` が呼び出されました。 |
| `trigger:link` | `utag.link()` が呼び出されました。 |
| `trigger:called before tags loaded` | タグがページ上でロードされる前にトラッキングコールが発生しました。トラッキングコールはキューに入れられ、タグがロードされた後に実行されます。|
| `utag.handler.INIT` | キューに入れられたタグがトリガーされます。 |