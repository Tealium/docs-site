---
title: トラブルシューティング
description: Tealium Configuration MCPでの一般的な問題、接続失敗、予期しないエージェントの動作、セッションエラーを解決します。
url: https://docs.tealium.com/ja/server-side/config-mcp/troubleshoot-config-mcp/
---
## MCPが私のTealiumプロファイルに接続できない

現在の会話でTealium Configuration MCPコネクタが有効であることを確認してください。コネクタを切断して再接続し、認証セッションが期限切れの場合は再度サインインしてください。

Tealium UIで以下を確認してください：

* サーバーサイドのユーザー構成の下でアカウントとプロファイルの選択が正しいこと。
* プロファイルへのプラットフォーム権限とMCPアクセスが必要であること。
* プロファイルには少なくとも1つの公開されたリビジョンがあること。

問題が続く場合は、組織のMCP構成を確認するために管理者に連絡してください。

## MCPが予期しないアクションを取る

エージェントが予期しない動作をする場合は、Claude Desktopまたはclaude.aiの組み込みフィードバックプロンプトを使用して診断レポートを生成してください：

1. メッセージコンポーザーで**+**アイコンをクリックします。
1. **Add from Tealium Configuration MCP**を選択します。
1. **Mcp-feedback**を選択し、プロンプトに従います。

![](https://docs.tealium.com/images/server-side/config-mcp-feedback-prompt.png)

エクスポートされたレポートを[Tealiumサポート](https://docs.tealium.com/support/)に共有して分析してもらいます。

## MCPがTealium UIでロードされないバージョンを作成する

そのバージョンを公開しないでください。すでに公開されている場合は、[バージョン管理](https://docs.tealium.com/ss-version-history/)を使用して以前の公開バージョンにロールバックします。[サポートに連絡](https://docs.tealium.com/support/)して、問題が発生したときのエージェントの動作についての詳細を提供してください。

## 要求されたエンティティまたはアクションが利用できない

[サポートされているオブジェクト](https://docs.tealium.com/about-config-mcp/#supported-objects)のリストを確認して、エンティティと操作がサポートされていることを確認してください。MCPサーバーがタスクを完了できない場合は、プロンプトを見直して、より明確な指示で言い換えてください。

## コミット後に変更が表示されない

コミットが正常に完了したことを確認してください。必要に応じて、`commit`と入力してコミットを強制します。その後、Tealium UIで**バージョン履歴**を開き、新しい保存されたバージョンを探します。コミットは公開を意味しません。新しいバージョンはTealium UIで別の公開アクションが必要です。

## トークンが不足している

Claudeプランをアップグレードしてください。特定のアクティビティやプロンプトが予想外に多くのトークンを消費する場合は、プロンプトとタスクの詳細を[Tealiumサポート](https://docs.tealium.com/support/)に連絡してください。これらの詳細を共有することで、Tealiumはさらに調査し最適化するのに役立ちます。