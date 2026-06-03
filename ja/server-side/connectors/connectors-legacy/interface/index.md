---
title: コネクターインターフェース（レガシー）
description: コネクターインターフェースは、AudienceStream Customer Data Platform (CDP) および EventStream API Hub のユーザーがサーバーサイドのコネクターやアクションを構築および維持する際に直感的なワークフローを表示します。
url: https://docs.tealium.com/ja/server-side/connectors/connectors-legacy/interface/
---
これはコネクターインターフェースのレガシーバージョンであり、間もなく非推奨となります。新しいインターフェースについては、を参照してください。

コネクターのランディングページから、新しいコネクターを構成したり、既存のコネクターのアクションを表示・編集したり、成功とエラーのカウントに関するリアルタイムレポートを表示することができます。

以下のリストは、コネクターインターフェースから利用可能な機能の概要を提供します：

## ランディングページ

コネクターにアクセスすると、初期のデフォルトビューは現在のサーバーサイドコネクターの拡張スナップショットです。  
![](/images/server-side/connector-workflow-sample-update.png)

## 検索

**Spotlight Search** 機能を使用すると、探しているコネクターの名前を入力し始めると、入力される各文字に応じてリストが一致するものを表示します。検索結果から、そのコネクターの利用可能なオプションに直接進むことができ、詳細にドリルダウンすることができます。

![](/images/server-side/connectors-workflow-spotlight-search-update.png)

## 概要

コネクターを追加する際、最初のページではコネクターに関する情報、必要なもの、サポートされるアクション、関連する内部および外部リソースがまとめられています。

![](/images/server-side/connectors-v2-clicksend-config.jpg)

## ワークフロー
コネクターインターフェースのワークフローは、新しいサーバーサイドコネクターを追加するための簡単なステップをユーザーに案内し、各技術にすでに割り当てられているアクションオプションを表示します。

![](/images/server-side/about-connectors-select-data-source.gif)

## コネクターの構成
単一のコネクターに対して異なる構成を構成することができます。たとえば、開発者、サンドボックス、および本番アカウントはそれぞれ独自の構成を持つことができます。  
![](/images/server-side/about-connectors-set-by-configuration.gif)

## 同意カテゴリの表示
マーケットプレースの各EventStreamコネクターには、利用可能なアクションごとに1つ以上の同意カテゴリが割り当てられています。特定のコネクターアクションの同意カテゴリをすばやく表示するには、コネクターアクションの隣にある情報アイコンをクリックします。

![](/images/server-side/eventstream-connector-consent-categories.gif)

## 不完全なアクションの表示
コネクターのアクションを構成する際、各必須アクションの右側にある状態インジケーターは、`COMPLETED`または`INCOMPLETE`を表示して、次に進む前に完全性をすばやく確認することができます。オプションのアクションはこの状態を表示しません。

![](/images/server-side/about-connectors-actions-complete-or-incomplete.gif)

## アクションのオン/オフ切り替え
コネクターの個々のアクションをオンまたはオフに切り替えることができます。また、コネクター全体をオンまたはオフに切り替えることもできます。

![](/images/server-side/about-connectors-toggle-entire-connector-or-individual-actions.gif)

## 新しいアクションの再割り当て
すでに構築されているサーバーサイドコネクターに、アクションを作成して再割り当てすることができます。

## エンリッチメントされたレポーティング
AudienceStreamおよびEventStreamのサーバーサイドコネクターレポーティングは、リアルタイムでの成功とエラーの総数を示します。エラー情報をCSVファイルにダウンロードして詳細に調査することもできます。

## 以前のコネクターバージョンにロールバック
以前に公開されたコネクターのバージョンにロールバックすることができます。

![](/images/server-side/connectors-v2-roll-back-version.jpg)
