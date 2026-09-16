---
title: Context API管理MCPサーバー
description: Context API管理MCPサーバーについて学びましょう。
url: https://docs.tealium.com/ja/server-side/context-api/managed-mcp-server/
---
## 概要
Context API管理MCPサーバーは、モデルコンテキストプロトコル（MCP）を使用して訪問プロファイルデータへの安全でリアルタイムなアクセスを可能にします。AIシステムはこのサーバーに接続して、即時のパーソナライゼーション、分析、および自動化のための顧客コンテキストを取得します。TealiumのMCPサービスは、現在Agent-to-Agent（A2A）プロトコルサポートを含む、管理されたネイティブAIプロトコルサポートの一部です。

## 要件

* **Context APIエンジン**: 少なくとも1つのアクティブな[Context APIエンジン](https://docs.tealium.com/about-context-api/#engines)が必要です。
* **APIキー**: 管理MCPサーバーへのアクセスには、この機能に専用のAPIキーが必要です。キーをリクエストするには、Tealiumサポートに連絡してください。

## 動作原理

管理MCPサーバーは、特定の指示とパラメーターを通じてトリガーできるツールを公開することで動作します。これらのツールを使用して、リアルタイムで訪問プロファイルデータをクエリし、パーソナライズされた応答と洞察を可能にします。

管理MCPサーバーと対話するには、Large Language Model（LLM）に明確で簡潔な指示を提供する必要があります。これらの指示には、以下を含める必要があります：

* **コンテキスト**: 対話の目的と、受け取りたい情報を説明します。
* **パラメーター**: ツールに必要なパラメーターを明確に記載します。例えば、`account`、`profile`、`engineId`、および訪問固有の識別子などです。

### 指示とプロンプト

このセクションでは、MCPサーバーとの対話時に効果的な指示とプロンプトを作成するための主要な概念を説明します。

1. **指示: 静的パラメーターの使用**  
   指示は、MCPツールに必要な静的パラメーターを定義します。例えば、`account`、`profile`、`engineId`などです。これらのパラメーターは特定の構成に対して一定であり、MCPツールがリクエストを処理する際にどのアカウント、プロファイル、エンジンを使用するかを知るために必要です。例えば：
   ```none
   TealiumのMCPツールを使用して質問に答えてください。
   次の必要なパラメーターを使用してください：
   * Tealiumアカウント: my_account
   * Tealiumプロファイル: my_profile
   * TealiumエンジンID: engine_001
   ```

2. **プロンプト: 動的パラメーターの使用**  
   プロンプトは、MCPツールに必要な動的パラメーターを指定します。これらのパラメーターは、問い合わせられる特定の訪問や使用ケースに応じて変わります。動的パラメーターをプロンプトに記載することで、MCPツールは現在のコンテキストに合わせたデータを取得できます。例えば：
   ```none
   匿名訪問{anon_visitor_id}はVIPオーディエンスの一部ですか？
   ```

3. **応答データ: 特定のプロパティの参照**  
   プロンプトには、期待される応答データの特定のプロパティへの参照が含まれるべきです。例えば、`audiences`、`attributes`、または`badges`などです。これにより、MCPツールは使用ケースに必要な関連データのみを返すようになり、明確性が向上し、不要な出力が減少します。例えば：
   ```none
   こちらが訪問のオーディエンスリストです：{response.audiences}
   ```  
   これにより、MCPツールは応答の`audiences`プロパティに焦点を当てるようになり、プロンプトの要件に合った出力が保証されます。詳細については、[Context API: Objects](https://docs.tealium.com/context-api-endpoint/#objects)を参照してください。

静的パラメーターを指示に組み込み、動的パラメーターをプロンプトに使用し、特定の応答プロパティを指定することで、MCPサーバーに対して正確で効果的なクエリを作成できます。

## ベストプラクティス

このソリューションから最良の結果を得るために、以下のことを強く推奨します：

**属性名の使用**（強く推奨）  
デフォルトでは、Context APIエンジンは数値の属性IDを返しますが、これにはLLMにとってのコンテキストが欠けています。最良の結果を得るために、エンジンが属性名を返すように構成してください。属性名は記述的であり、LLMが正確に解釈して応答するのに役立ちます。アカウントが広く認識されていない頭字語や略語を使用している場合、LLMはそれらを解釈するのが難しいかもしれません。属性名が記述的であり、人間とAIシステムの両方によって容易に理解されるように、見直しと更新を検討してください。


<blockquote>
属性名を使用することは、LLMベースのソリューションで管理MCPサーバーを活用する唯一の実現可能なアプローチです。詳細については、[Context API: Objects](https://docs.tealium.com/context-api-endpoint/#objects)を参照してください。
</blockquote>


**専用のContext APIエンジン**  
他の目的で作成された既存のContext APIエンジンを再利用しないでください。各管理MCPサーバーの使用ケースに対して別のエンジンを作成し、そのシナリオに必要な属性、バッジ、およびオーディエンスのみを構成してください。これにより：

* 関連するデータのみが公開され、正確なコンテキストが提供されます。
* 複雑さが減少し、メンテナンスが容易になります。
* 要件が変更された場合の監査と更新が簡単になります。

**特定の訪問データの使用**  
使用ケースに関連しない大量の訪問データをContext APIエンジンに公開しないでください。特定の使用ケースに不可欠な属性、バッジ、およびオーディエンスのみを含めてください。不要なデータを提供すると、LLMが圧倒されて応答の正確性が低下する可能性があります。関連するデータの焦点を絞ったセットは、明確性と応答品質を向上させます。

## 利用可能なツール

すべてのツールは次のパラメーターをサポートしています：

| パラメーター | 説明 |
| --------- | ----------- |
| `account` | (必須) Tealiumアカウントの名前です。 |
| `profile` | (必須) Tealiumアカウント内のプロファイルの名前です。 |
| `engineId` | (必須) Context APIエンドポイントのエンジンIDです。 |
| `Origin` | (必須) リクエストを開始した起源です。 |
| `Referer` | (必須) リクエストを開始した絶対または部分的なアドレスです。 |
| `suppressNotFound` | 訪問レコードが見つからない場合の応答タイプを決定します。<br>`false` (デフォルト): HTTPステータスコード`404 Not Found`を返します。<br>`true`: HTTPステータスコード`200 OK`を空の応答本体とともに返します。 |

Context API管理MCPサーバーには、次のツールが含まれています：

### `getPersonalizationContentByAnonymousId`

Tealiumの匿名IDを使用して訪問データを取得します。詳細については、[anonymous-user-visitor-id-attributes](https://docs.tealium.com/anonymous-user-visitor-id-attributes/)を参照してください。

| パラメーター | 説明 |
| --------- | ----------- |
| `visitorId` | (必須) 訪問に各訪問または各アプリ使用ごとに割り当てられる一意で匿名の値です。匿名IDは、同じブラウザーやアプリからの複数の訪問を追跡しますが、異なるブラウザーやデバイス間では追跡しません。 |

このツールを使用するには、プロンプトを特に匿名IDに言及するようにフォーマットしてください。例えば：

```none
匿名訪問{visitor_id}は何に興味がありますか？
```

### `getPersonalizationContentByVisitorId`

訪問ID属性を指定して訪問データを取得します。属性IDと属性検索値を指定します。詳細については、[anonymous-user-visitor-id-attributes](https://docs.tealium.com/anonymous-user-visitor-id-attributes/)を参照してください。

| パラメーター | 説明 |
| --------- | ----------- |
| `attributeId` | (必須) [訪問ID属性](https://docs.tealium.com/visitor-id-attribute/)を表す数値UIDです。 |
| `attributeValue` | (必須) 検索する属性の値です。 |

このツールを使用するには、プロンプトを特に属性IDと値に言及するようにフォーマットしてください。例えば：

```none
訪問属性ID{visitor_attribute_id}と値{visitor_attribute_value}に興味があるものは何ですか？
```
## OpenAIエージェントSDKソリューション

次のサンプルコードは、Python用OpenAIエージェントを使用してContext API管理MCPサーバーに接続し、訪問に関する質問をする方法を示しています。エージェントの指示には、リクエストに関連する静的パラメータが指定されています。プロンプトは、訪問の匿名IDが既知であると仮定しています。

詳細については、[OpenAI Agents SDK: Model context protocol (MCP)](https://openai.github.io/openai-agents-python/mcp/)を参照してください。



```python
import asyncio
import os

from agents import Agent, HostedMCPTool, Runner

async def main() -> None:
    agent = Agent(
        name="Assistant",
        instructions=f"""
                Tealium MCPツールを使用して質問に答えてください。
                Tealiumアカウント: my_account
                Tealiumプロファイル: my_profile
                TealiumエンジンID: engine_001
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
    匿名訪問{anon_visitor_id}はVIPオーディエンスの一部ですか？こちらが訪問のオーディエンスリストです: {response.audiences}
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
                Tealium MCPツールを使用して質問に答えてください。
                Tealiumアカウント: my_account
                Tealiumプロファイル: my_profile
                TealiumエンジンID: engine_001
                """,
            mcp_servers=[server],
            model_settings=ModelSettings(tool_choice="required"),
        )

        anon_visitor_id = '1234567'
        query = f'''
        匿名訪問{anon_visitor_id}はVIPオーディエンスの一部ですか？こちらが訪問のオーディエンスリストです: {response.audiences}
        '''
        result = await Runner.run(agent, query)
        print(result.final_output)

if __name__ == "__main__":
    asyncio.run(main())
```



## MCPサーバーをMCPインスペクターでテストする

MCPサーバーに接続するために、オープンソースのMCPインスペクターなどのツールの使用をお勧めします。

MCPインスペクターを使用して：

* サーバー接続を確認します。
* 利用可能なツールとそのパラメータを確認します。
* 認証または構成の問題をトラブルシューティングします。
* MCPベースの統合の開発を加速します。

詳細については、[Model Context Protocol > Getting started](https://modelcontextprotocol.io/docs/tools/inspector#getting-started)を参照してください。

MCPインスペクターを実行し、MCPサーバーをテストするには：

1. ターミナルを開き、次のコマンドを実行します：
    ```
    npx @modelcontextprotocol/inspector
    ```
    これにより、MCPインスペクターがインストールされ、ブラウザウィンドウでツールが開きます。
1. **Transport Type**に`Streamable HTTP`を構成します。
1. **URL**に`https://us-west-2.prod.developer.tealiumapis.com/v1/personalization/mcp`を構成します。リージョンは、Context APIエンジンのリージョンと一致する必要があります。
1. **Custom Headers**の下に、`X-Tealium-Api-Key`キーとMCPサーバーAPIキーを追加します。MCP APIキーはMCPサーバーアクセス専用のAPIキーであり、Tealiumサポートから要求する必要があります。

![](https://docs.tealium.com/images/server-side/moments-api/moments-mcp-server-inspector-config.png)

<blockquote>
このスクリーンショットは以前の製品名「Moments API」を示しています。製品UIが更新された際に更新されます。
</blockquote>


**Connect**をクリックすると、ステータスが**Connected**に更新され、「List Tools」ボタンが表示されます。

サーバーでツールを実行するには：

1. **List Tools**をクリックして利用可能なツールを確認します。
1. ツールをクリックしてその定義を確認します。
1. 必要なパラメータの値を入力します。
1. **Run Tool**をクリックします。
1. **Tool Result**の下に、`Success`メッセージとContext APIの結果が表示されます。