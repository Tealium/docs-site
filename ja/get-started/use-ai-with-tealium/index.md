---
title: Tealium で AI を使用する
description: Tealium が AI エージェントに顧客コンテキストを提供し、AI モデルでデータをエンリッチし、AI サービスにデータを送信する方法と、AI を使用して Tealium を構成する方法について説明します。
url: https://docs.tealium.com/ja/get-started/use-ai-with-tealium/
---
AI エージェントとモデルは、最新の顧客データを利用することで、より適切な意思決定を行えます。Tealium は、選択した AI システムにそのデータを提供し、AI の出力を訪問プロファイルに追加します。また、チームによる Tealium の構成を支援する AI アシスタントも備えています。

## AI エージェントに顧客コンテキストを提供する

AI エージェントには、対応する顧客に関する最新のコンテキストが必要です。Context API MCP サーバーは、AI エージェントがツールを呼び出すための標準的な方法である Model Context Protocol（MCP）を通じて、そのコンテキストをエージェントに提供します。エージェントは、オーディエンス、バッジ、属性など、アプリがリクエストするものと同じ訪問プロファイルデータを受け取ります。

たとえば、AI サポートエージェントは、会話の開始時に訪問の最近のアクティビティとオーディエンスメンバーシップを読み込みます。


![](https://docs.tealium.com/images/icons/icon-moments-api.svg)

#### Context API MCP サーバー

MCP を通じて、AI エージェントが訪問プロファイルデータにリアルタイムでアクセスできるようにします。


## AI でデータをエンリッチする

AI エンリッチメントは、Tealium データパイプラインの一部として、イベントデータまたは訪問データに大規模言語モデル（LLM）による処理を実行します。たとえば、AI エンリッチメントでは、製品レビューの感情を分類したり、最近の閲覧履歴から訪問の購入意向を推測したりできます。出力は新しいイベントとして Tealium に返されるため、オーディエンスとコネクタはその結果に基づいて処理を実行できます。


![](https://docs.tealium.com/images/icons/icon-star.svg)

#### AI エンリッチメント

顧客データを LLM に送信し、その出力を Tealium に返します。


## AI サービスにデータを送信する

AI コネクタは、プロンプトに基づく推論を行うために、イベントデータと訪問データを Amazon Bedrock、Google Vertex AI、OpenAI などの AI プラットフォームに送信します。モデルの応答はイベントとして Tealium に返され、エンリッチメントによって結果が訪問プロファイルに書き込まれます。


![](https://docs.tealium.com/images/icons/icon-connector.svg)

#### AI コネクタ

AI コネクタが顧客データを AI プラットフォームに送信する仕組みについて説明します。


## AI で Tealium を構成する

Tealium インターフェイスの AI 機能は、構成の構築と保守に役立ちます。

* **AI Assistant**：Tealium の構成と使用方法に関する質問に回答します。
* **AI audience recommendations**：属性と訪問データに基づいてオーディエンスを提案します。
* **Functions writer**：関数コード、トリガールール、テストペイロードを生成します。
* **Note generation**：構成項目の説明を作成します。
* **SQL writer**：クラウドデータソース向けのクエリを生成します。

Tealium Studio は、コンポーネントがどのように構成されているか、どのコンポーネントが相互に依存しているかなど、サーバーサイド構成に関する質問に対応する AI チャットインターフェイスです。

Configuration MCP サーバーは、Claude などの外部 AI クライアントをサーバーサイドプロファイルに接続し、自然言語で構成を調査、変更できるようにします。


![](https://docs.tealium.com/images/icons/icon-star.svg)

#### AI 機能

Tealium インターフェイスの AI 機能と、その有効化方法について説明します。



![](https://docs.tealium.com/images/icons/icon-audience.svg)

#### AI オーディエンスレコメンデーション

AI が生成した新しいオーディエンスの提案を取得します。



![](https://docs.tealium.com/images/icons/icon-code.svg)

#### Functions writer

AI を使用して関数コードを生成し、デバッグします。



![](https://docs.tealium.com/images/icons/icon-cube.svg)

#### Tealium Studio

サーバーサイド構成について、自然言語で質問します。



![](https://docs.tealium.com/images/icons/icon-gear.svg)

#### Configuration MCP サーバー

AI クライアントからサーバーサイド構成を調査、変更します。



![](https://docs.tealium.com/images/icons/icon-book-solid.svg)

#### AI エージェント向けドキュメント

Tealium のドキュメントを AI エージェントや LLM とともに使用します。
