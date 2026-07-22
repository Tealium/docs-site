---
title: トレース: トレースでテスト
description: このステップでは、トレースを使用して、すべての前の構成が期待通りに動作していることを確認します。トレースIDを取得し、それをアプリケーションに追加するか（またはTealiumツールを使用するか）、簡単なテストを行い、その後、トレースインターフェースのログを調査します。
url: https://docs.tealium.com/ja/server-side/getting-started/audiencestream-cdp/test-trace/
---
## 必要条件

トレースでウェブページをテストする場合、以下が必要です：

* [Tealium Toolsブラウザ拡張](https://docs.tealium.com/tealium-tools-browser-extension/)

## トレースの開始

以下の手順でトレースをテストします：

1. **ツール > トレース**に移動し、新規トレースの下の**開始**をクリックします。
1. 提供されたトレースIDをコピーし、**続行**をクリックします。
1. 次の方法のいずれかを使用してトレースIDを有効にします：  

  * **Tealium Tools** 
  
      1. テストページへの新しいブラウザウィンドウを開きます。 
      1. Tealium Toolsブラウザ拡張をクリックします
      1. **AudienceStream Trace**をクリックします。
      1. ステップ2からのトレースIDを入力し、**Start Trace**をクリックします。<br> ![](https://docs.tealium.com/images/server-side/es-getting-started-trace-tealium-tool.jpg) 

  * **Data Layer Attribute** 
  
      1. `tealium_trace_id`をコードインストールのデータレイヤーに追加し、それをトレースIDの値に構成します。
      1. HTTP APIでは、これはクエリストリングパラメータを追加することを意味します：`&tealium_trace_id=012345`
      1. 例えばSwiftアプリでは、以下のようになります：<br> `tealium?.volatileData()?.add(data: ["tealium_trace_id": "012345"])`

1. テストケースのワークフローを進めます。  
これは、ページを更新したり、いくつかのページをナビゲートしたり、購入を行ったり、ネイティブアプリのいくつかの画面を表示したりすることを意味します。この場合、500ドル以上の購入を完了すると、作成したオーディエンスがトリガーされます。
1. ログの詳細を調査するためにトレースインターフェースに戻ります。

## トレースログ

トレースログは、イベントが受信されると自動的に更新されます。UIは、イベントデータの詳細、エンリッチされた訪問属性、参加または離脱したオーディエンス、およびトリガーされたコネクタアクションを表示します。エラーがあった場合、問題の詳細とともにそれらも提供されます。

この例では、550ドルの購入が完了し、トレースで以下が確認されました：

* ✓ - 訪問属性の更新  
    ![](https://docs.tealium.com/images/tutorials/as-getting-started-trace-enriched-visitor.jpg)
* ✓ - VIPオーディエンスの参加  
    ![](https://docs.tealium.com/images/tutorials/as-getting-started-audiences-joined.jpg)
* ✓ - Google Sheetsコネクタのトリガー  
    ![](https://docs.tealium.com/images/tutorials/as-getting-started-sheets-inserted-row.jpg)
* ✓ - Google Sheets行の挿入  
    ![](https://docs.tealium.com/images/server-side/as-getting-started-sheets-inserted-row.jpg)

![](https://docs.tealium.com/images/server-side/beast-thumbsup-whistle-small.png)

期待したトレースログが表示されなかった場合は、以下のことを確認してください：

* テストで正しいトレースIDを使用しましたか？
* 訪問属性、オーディエンス、コネクタアクションを追加した後にアカウントを保存し、公開しましたか？
* 属性のエンリッチされたルールは正確ですか？
* オーディエンスフィルターは正しいですか？

このシンプルなガイドの最後まで来ました。次のステップでは、保存と公開のプロセスを簡単にカバーし、その後、追加の読み物のための役立つリンクを提供します。