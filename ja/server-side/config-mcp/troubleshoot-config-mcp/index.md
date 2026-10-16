---
title: トラブルシューティング
description: Tealium Configuration MCPの一般的な問題、接続失敗、予期しないエージェントの動作、セッションエラーを解決します。
url: https://docs.tealium.com/ja/server-side/config-mcp/troubleshoot-config-mcp/
---
## Tealium Configuration MCPが私のTealiumプロファイルに接続できない

現在の会話でTealium Configuration MCPコネクタが有効であることを確認してください。コネクタを切断して再接続し、認証セッションが期限切れになっている場合は再度サインインしてください。

Tealium UIで以下を確認してください：

* サーバーサイドのユーザー構成の下でアカウントとプロファイルの選択が正しいこと。
* MCPサーバーアクセス（プラットフォーム権限）を持つユーザーグループを通じて、またはリーダー、エディター、パブリッシャープロファイルレベルのアクセス（レガシー権限）を通じてプロファイルへの必要なTealium Configuration MCPアクセスを持っていること。
* プロファイルには少なくとも1つの公開されたリビジョンがあること。

問題が続く場合は、組織のTealium Configuration MCP構成を確認するために管理者に連絡してください。

## Tealium Configuration MCPが予期しないアクションを取る

エージェントが予期しない動作をする場合は、Claude Desktopまたはclaude.aiの組み込みフィードバックプロンプトを使用して診断レポートを生成してください：

1. メッセージコンポーザーで**+**アイコンをクリックします。
1. **Tealium Configuration MCPから追加**を選択します。
1. **Mcp-feedback**を選択し、プロンプトに従います。

![](https://docs.tealium.com/images/server-side/config-mcp-feedback-prompt.png)

エクスポートされたレポートを[Tealiumサポート](https://docs.tealium.com/support/)に共有して分析してもらってください。

## Tealium Configuration MCPがTealium UIでロードされないバージョンを作成する

そのバージョンを公開しないでください。バージョンがすでに公開されている場合は、[バージョン管理](https://docs.tealium.com/ss-version-history/)を使用して以前の公開バージョンにロールバックします。[サポートに連絡](https://docs.tealium.com/support/)して、問題が発生したときのエージェントの動作についての詳細を提供してください。

## Tealium Configuration MCPが既存のオーディエンスを変更できない

Tealium Configuration MCPは、変更できない一部のオーディエンスを読み取ることができます。この制限は、オーディエンスが現在のオーディエンスUIで編集および公開されていない場合に発生することがあります。**Activate > Audiences**でオーディエンスを開き、変更せずに保存して公開してください。公開すると、オーディエンスは自動的に現在の構成形式にアップグレードされます。公開後、新しいMCPセッションを開始してください。次のツールコール時に、Tealium Configuration MCPは新しい公開バージョンが利用可能であることを通知しますが、現在のセッションドラフトは依然として古いオーディエンスバージョンを保持しています。このアップグレードは永続的であり、元に戻すことはできません。

セグメントを使用するオーディエンスは、Tealium Configuration MCPの構成変更に対応していません。これらのオーディエンスはTealium UIで編集する必要があります。

## 要求されたエンティティまたはアクションが利用不可能

[サポートされているオブジェクト](https://docs.tealium.com/about-config-mcp/#supported-objects)のリストを確認して、エンティティと操作がサポートされていることを確認してください。Tealium Configuration MCPがタスクを完了できない場合は、プロンプトを見直して、より明確な指示で言い換えてください。

## コミット後に変更が表示されない

コミットが正常に完了したことを確認してください。必要に応じて、`commit`と入力してコミットを強制してください。その後、Tealium UIの**バージョン履歴**を開いて新しい保存バージョンを探してください。コミットは公開を意味しません。新バージョンはTealium UIで別の公開アクションを必要とします。

## トークンが不足している

Claudeプランをアップグレードしてください。特定の活動やプロンプトが予想以上に多くのトークンを消費しているように思われる場合は、プロンプトとタスクに関する詳細を[Tealiumサポート](https://docs.tealium.com/support/)に連絡してください。これらの詳細を共有することで、Tealiumはさらに調査および最適化を行うことができます。

## 長い会話でモデルの精度が低下する

長い会話でモデルが幻覚を起こしたり精度が低下したりする場合は、モデルに会話を要約させ、その要約を初期コンテキストとして使用して新しいチャットを開始してください。