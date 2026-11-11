---
title: Context API マネージド MCP サーバー
description: Context API マネージド MCP サーバーについて説明します。
url: https://docs.tealium.com/ja/server-side/context-api/managed-mcp-server/
---
## 概要
Context API マネージド MCP サーバーを使用すると、Model Context Protocol（MCP）を通じて訪問プロファイルデータに安全かつリアルタイムにアクセスできます。AI システムはこのサーバーに接続して顧客コンテキストを取得し、即時のパーソナライゼーション、分析、自動化に利用します。Tealium MCP サービスは、Tealium が管理するネイティブ AI プロトコルサポートの一部であり、現在は Agent-to-Agent（A2A）プロトコルもサポートしています。

## 要件

* **Context API エンジン**：少なくとも 1 つの有効な [Context API エンジン](https://docs.tealium.com/about-context-api/#engines)が必要です。
* **API キー**：マネージド MCP サーバーにアクセスするには、この機能専用の API キーが必要です。キーをリクエストするには、Tealium サポートにお問い合わせください。

## 仕組み

マネージド MCP サーバーは、特定の指示とパラメータを使用してトリガーできるツールを公開することで動作します。これらのツールを使用すると、訪問プロファイルデータをリアルタイムで照会し、パーソナライズされた応答やインサイトを得ることができます。

マネージド MCP サーバーとやり取りするには、大規模言語モデル（LLM）に明確かつ簡潔な指示を与える必要があります。指示には、以下を含めてください。

* **コンテキスト**：やり取りの目的と、受け取ることを期待する情報について説明します。
* **パラメータ**：`account`、`profile`、`engineId`、訪問固有の識別子など、ツールに必要なパラメータを明確に指定します。

### 指示とプロンプト

このセクションでは、MCP サーバーとやり取りする際に効果的な指示とプロンプトを作成するための主要な概念について説明します。

1. **指示：静的パラメータを使用する**  
   指示では、`account`、`profile`、`engineId` など、MCP ツールに必要な静的パラメータを定義します。これらのパラメータは、特定の構成では変化せず、リクエストの処理時に使用するアカウント、プロファイル、エンジンを MCP ツールが認識できるようにします。例：  
   ```none
   Use the Tealium MCP tools to answer the questions.
   Use the following required parameters:
   * Tealium Account: my_account
   * Tealium Profile: my_profile
   * Tealium Engine ID: engine_001
   ```

2. **プロンプト：動的パラメータを使用する**  
   プロンプトでは、各ツールで必要となる訪問固有の値など、MCP ツールに必要な動的パラメータを指定します。これらのパラメータは、照会対象の訪問やユースケースに応じて変化します。プロンプト内で動的パラメータを参照することにより、MCP ツールは現在のコンテキストに合わせたデータを取得できます。例：  
   ```none
   Is the anonymous visitor {anon_visitor_id} part of the VIP Audience?
   ```

3. **応答データ：特定のプロパティを参照する**  
   プロンプトには、`audiences`、`attributes`、`badges` など、期待する応答データの特定のプロパティへの参照を含めてください。これにより、MCP ツールはユースケースに必要な関連データのみを返すため、明確さが向上し、不要な出力が削減されます。例：  
   ```none
   Here is the visitor's list of audiences: {response.audiences}
   ```  
   これにより、MCP ツールは応答内の `audiences` プロパティに注目し、出力をプロンプトの要件に合わせることができます。詳細については、[Context API：オブジェクト](https://docs.tealium.com/context-api-endpoint/#objects)を参照してください。  

指示内の静的パラメータ、プロンプト内の動的パラメータ、特定の応答プロパティを組み合わせることで、MCP サーバー向けの正確で効果的なクエリを作成できます。

## ベストプラクティス

このソリューションから最良の結果を得るため、以下を強く推奨します。

**属性名を使用する**（強く推奨）  
デフォルトでは、Context API エンジンは数値の属性 ID を返しますが、これらには LLM が理解するためのコンテキストがありません。最良の結果を得るには、属性名を返すようにエンジンを構成してください。属性名は説明的であり、LLM が正確に解釈して応答するのに役立ちます。広く認識されていない頭字語や略語をアカウントで使用している場合、LLM がそれらを解釈するのは困難なことがあります。人間と AI システムの両方が容易に理解できる説明的な属性名になっていることを確認し、必要に応じて更新することを検討してください。


<blockquote>
LLM ベースのソリューションでマネージド MCP サーバーを活用するには、属性名の使用が唯一の実用的な方法です。詳細については、[Context API：オブジェクト](https://docs.tealium.com/context-api-endpoint/#objects)を参照してください。
</blockquote>


**専用の Context API エンジン**  
他の目的で作成された既存の Context API エンジンを再利用しないでください。マネージド MCP サーバーのユースケースごとに、そのシナリオで必要となる属性、バッジ、オーディエンスのみを構成した個別のエンジンを作成してください。これにより、以下が実現します。

* 関連するデータのみが公開され、正確なコンテキストが提供されます。
* 複雑さが軽減され、メンテナンスが容易になります。
* 要件の変更に伴う監査と更新が簡素化されます。

**特定の訪問データを使用する**  
ユースケースに関係のない大量の訪問データを Context API エンジンで公開しないでください。特定のユースケースに不可欠な属性、バッジ、オーディエンスのみを含めてください。不要なデータを提供すると LLM の処理に負荷がかかり、応答の精度が低下する可能性があります。関連データに絞ることで、明確さと応答品質が向上します。

## 利用可能なツール

すべてのツールで、以下のパラメータがサポートされています。

| パラメータ | 説明 |
| --------- | ----------- |
| `account` | （必須）Tealium アカウントの名前。 |
| `profile` | （必須）Tealium アカウント内のプロファイル名。 |
| `engineId` | （必須）Context API エンドポイントのエンジン ID。 |
| `Origin` | （必須）リクエストの送信元。 |
| `Referer` | （必須）リクエストを開始した絶対アドレスまたは部分アドレス。 |
| `suppressNotFound` | 訪問レコードが見つからない場合に返される応答タイプを決定します。<br>`false`（デフォルト）：HTTP ステータスコード `404 Not Found` を返します。<br>`true`：空の応答本文とともに HTTP ステータスコード `200 OK` を返します。 |


Context API マネージド MCP サーバーには、以下のツールが含まれています。

### `getPersonalizationContentByAnonymousId`

Tealium 匿名 ID を使用して訪問データを取得します。詳細については、[anonymous-user-visitor-id-attributes](https://docs.tealium.com/anonymous-user-visitor-id-attributes/)を参照してください。

| パラメータ | 説明 |
| --------- | ----------- |
| `visitorId` | （必須）サイトへの訪問時またはアプリの使用時に、訪問に割り当てられる一意の匿名値。同じブラウザーまたはアプリからの複数回の訪問にわたって訪問を追跡しますが、異なるブラウザーやデバイス間では追跡しません。 |

このツールを使用するには、匿名 ID を明示するようにプロンプトを記述します。例：

```none
What is anonymous visitor {visitor_id} interested in?
```

### `getPersonalizationContentByVisitorId`

属性 ID と属性の検索値を指定し、訪問 ID 属性を使用して訪問データを取得します。詳細については、[anonymous-user-visitor-id-attributes](https://docs.tealium.com/anonymous-user-visitor-id-attributes/)を参照してください。

| パラメータ | 説明 |
| --------- | ----------- |
| `attributeId` | （必須）[訪問 ID 属性](https://docs.tealium.com/visitor-id-attribute/)を表す数値 UID。 |
| `attributeValue` | （必須）検索する属性の値。 |

このツールを使用するには、検索する属性 ID と値を明示するようにプロンプトを記述します。例：

```none
What is visitor attribute id {visitor_attribute_id} with value {visitor_attribute_value} interested in?
```
## OpenAI Agent SDK ソリューション

次のサンプルコードは、Python 用 OpenAI Agent を使用して Context API のマネージド MCP サーバーに接続し、訪問について質問する方法を示しています。エージェントの指示では、リクエストに関連する静的パラメータを指定しています。このプロンプトでは、訪問の匿名 ID が既知であることを前提としています。

詳細については、[OpenAI Agents SDK：Model Context Protocol（MCP）](https://openai.github.io/openai-agents-python/mcp/)を参照してください。



```python
import asyncio
import os

from agents import Agent, HostedMCPTool, Runner

async def main() -> None:
    agent = Agent(
        name="Assistant",
        instructions=f"""
                Use the Tealium MCP tools to answer the questions.
                Tealium Account: my_account
                Tealium Profile: my_profile
                Tealium Engine Id: engine_001
                """,
        tools=[
            HostedMCPTool(
                tool_config={
                    "type": "mcp",
                    "server_label": "tealium_personalization_mcp",
                    "server_url": "https://us-west-2.prod.developer.tealiumapis.com/v1/personalization/mcp",
                    "require_approval": "never",
                    "headers": {
                        "X-Tealium-Api-Key": os.getenv('TEALIUM_API_KEY'),
                        "Origin": "https://example.com",
                        "Referer": "https://example.com"
                    }
                }
            )
        ],
    )

    anon_visitor_id = '1234567'
    query = f'''
    Is the anonymous visitor {anon_visitor_id} part of the VIP Audience? Here is the visitor's list of audiences: {response.audiences}
    '''
    result = await Runner.run(agent, query)
    print(result.final_output)

if __name__ == "__main__":
    asyncio.run(main())
```



```python
import asyncio
import os

from agents import Agent, Runner
from agents.mcp import MCPServerStreamableHttp
from agents.model_settings import ModelSettings

async def main() -> None:
    api_key = os.environ["TEALIUM_API_KEY"]

    async with MCPServerStreamableHttp(
            name="Tealium MCP Streamable HTTP Server",
            params={
                "url": "https://us-west-2.prod.developer.tealiumapis.com/v1/personalization/mcp",
                "headers": {
                    "X-Tealium-Api-Key": api_key,
                    "Origin": "https://example.com",
                    "Referer": "https://example.com"
                },
                "timeout": 10,
            },
            max_retry_attempts=3
    ) as server:
        agent = Agent(
            name="Assistant",
            instructions=f"""
                Use the Tealium MCP tools to answer the questions.
                Tealium Account: my_account
                Tealium Profile: my_profile
                Tealium Engine ID: engine_001
                """,
            mcp_servers=[server],
            model_settings=ModelSettings(tool_choice="required"),
        )

        anon_visitor_id = '1234567'
        query = f'''
        Is the anonymous visitor {anon_visitor_id} part of the VIP Audience? Here is the visitor's list of audiences: {response.audiences}
        '''
        result = await Runner.run(agent, query)
        print(result.final_output)

if __name__ == "__main__":
    asyncio.run(main())
```



## MCP Inspector を使用した MCP サーバーのテスト

MCP サーバーへの接続には、オープンソースの MCP Inspector などのツールを使用することをお勧めします。

MCP Inspector を使用すると、次のことができます。

* サーバーへの接続を確認する。
* 使用可能なツールとそのパラメータを確認する。
* 認証または構成に関する問題をトラブルシューティングする。
* MCP ベースの連携開発を迅速化する。

詳細については、[Model Context Protocol > はじめに](https://modelcontextprotocol.io/docs/tools/inspector#getting-started)を参照してください。

MCP Inspector を実行して MCP サーバーをテストするには、次の手順を実行します。

1. ターミナルを開き、次のコマンドを実行します。  
    ```
    npx @modelcontextprotocol/inspector
    ```
    これにより MCP Inspector がインストールされ、ブラウザーウィンドウでツールが開きます。
1. **Transport Type** を `Streamable HTTP` に構成します。
1. **URL** を `https://us-west-2.prod.developer.tealiumapis.com/v1/personalization/mcp` に構成します。リージョンは、Context API エンジンのリージョンと一致している必要があります。
1. **Custom Headers** で、`X-Tealium-Api-Key` キーと MCP サーバーの API キーを追加します。MCP API キーは MCP サーバーへのアクセス専用の API キーであり、Tealium サポートに申請する必要があります。

![](https://docs.tealium.com/images/server-side/moments-api/moments-mcp-server-inspector-config.png)

<blockquote>
このスクリーンショットには、以前の製品名である「Context API」が表示されています。製品 UI の更新時に、このスクリーンショットも更新されます。
</blockquote>


**Connect** をクリックすると、ステータスが **Connected** に更新され、**List Tools** ボタンが表示されます。

サーバー上のツールを実行するには、次の手順を実行します。

1. **List Tools** をクリックして、使用可能なツールを確認します。
1. ツールをクリックして、その定義を表示します。
1. 必須パラメータの値を入力します。
1. **Run Tool** をクリックします。
1. **Tool Result** に、`Success` メッセージと Context API の結果が表示されます。