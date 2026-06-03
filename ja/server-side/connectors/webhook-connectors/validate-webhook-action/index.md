---
title: Webhookアクションの検証
description: この記事では、Webhookアクションを検証する方法について説明します。
url: https://docs.tealium.com/ja/server-side/connectors/webhook-connectors/validate-webhook-action/
---
新しいアクションを検証およびトラブルシューティングするために、以下の方法のいずれかを使用します：

* **ベンダーユーザーインターフェース**  
ベンダーが変更を監視できるWebユーザーインターフェースを提供している場合、アクションをターゲットベンダーエンドポイントに送信し、ターゲットエンドポイントでそれを確認します。
* **PutsReqバケット**  
サンプルのPutsReqバケットURLにテストリクエストを送信します。アクションフィールドを構成した後、以下のURLにアクセスして、PutsReqユーザーインターフェースを使用して受信したリクエストを調べます。  
`https://putsreq.com/&gt;YOURBUCKETNAME/inspect`
* **トレース**  
[トレースツールを実行する]() してアクションデータを調べます。このアクションのテンプレート機能を使用している場合は、テンプレート変数JSONとレンダリングされたテンプレート：&amp;lt;template name&amp;gt;を確認してください。  
個々のデータ項目がバッチに追加されると、トレースは最初にバッチ化されたアクションを表示し、その後、バッチが第三者に送信された後に再度表示します。  
トレースでバッチに追加された個々のデータ項目はバッチ化されません。
複数のバッチングアクションは、しばしば単一の送信アクションに対応します。2つの間にはかなりの遅延がある場合があります。

## サンプルアクション構成

1. [https://putsreq.com/](http://putsreq.com/) にアクセスし、**PutsReqを作成**をクリックしてテスト用のエンドポイントを作成します。
      ![](/images/server-side/putsreq-yourputsrequrl.jpg)
1. **PutsReq URL**をコピーします。
1. Webhookコネクタのアクション構成に移動します。
1. Methodまでスクロールダウンし、クリックして展開します。
1. ドロップダウンリストから**POST**を選択します。
1. URLまでスクロールダウンし、クリックして展開し、URLパラメータフィールドに**PutsReq URL**を貼り付けます。  
      ![](/images/server-side/putsreq-webhookconnectorsettings-method-and-url.jpg)
1. **保存**をクリックします。
1. 変更を保存して公開します。
1. [トレースを実行する]() して、期待通りにアクションがトリガーされたことを確認します。