---
title: Moments API 管理MCPサーバー
description: Moments API 管理MCPサーバーについて学びましょう。
url: https://docs.tealium.com/ja/server-side/moments-api/managed-mcp-server/
---
## 概要
Moments API 管理MCPサーバーは、モデルコンテキストプロトコル（MCP）を使用して訪問プロファイルデータへの安全でリアルタイムなアクセスを可能にします。AIシステムはこのサーバーに接続して、即時のパーソナライゼーション、分析、および自動化のための顧客コンテキストを取得します。Tealium MCPサービスは、現在Agent-to-Agent（A2A）プロトコルサポートを含む、管理されたネイティブAIプロトコルサポートの一部です。

## 要件

* **Moments APIエンジン**: 少なくとも1つのアクティブな[Moments APIエンジン]()が必要です。
* **APIキー**: 管理MCPサーバーへのアクセスには、この機能に専用のAPIキーが必要です。キーをリクエストするには、Tealiumサポートに連絡してください。

## 動作原理

管理MCPサーバーは、特定の指示とパラメーターを通じてトリガーできるツールを公開することで動作します。これらのツールを使用して、リアルタイムで訪問プロファイルデータをクエリし、パーソナライズされた応答と洞察を可能にします。

管理MCPサーバーと対話するには、Large Language Model（LLM）に明確で簡潔な指示を提供する必要があります。これらの指示には、以下を含める必要があります：

* **コンテキスト**: 対話の目的と、受け取りたい情報を説明します。
* **パラメーター**: ツールに必要なパラメーターを明確に記載します。例えば、`account`、`profile`、`engineId`、および訪問固有の識別子などです。

### 指示とプロンプト

このセクションでは、MCPサーバーとの対話時に効果的な指示とプロンプトを作成するための主要な概念を説明します。

1. **指示: 静的パラメーターの使用**  
   指示は、MCPツールに必要な静的パラメーターを定義します。例えば、`account`、`profile`、`engineId`などです。これらのパラメーターは、特定の構成に対して一定であり、MCPツールがリクエストを処理する際にどのアカウント、プロファイル、エンジンを使用するかを知るために必要です。例えば：
   ```none
   Tealium MCPツールを使用して質問に答えてください。
   次の必要なパラメーターを使用してください：
   * Tealiumアカウント: my_account
   * Tealiumプロファイル: my_profile
   * TealiumエンジンID: engine_001
   ```

2. **プロンプト: 動的パラメーターの使用**  
   プロンプトは、MCPツールに必要な動的パラメーターを指定します。これらのパラメーターは、問い合わせられる特定の訪問や使用ケースに応じて変化します。動的パラメーターをプロンプトに記載することで、MCPツールは現在のコンテキストに合わせたデータを取得できます。例えば：
   ```none
   匿名訪問{anon_visitor_id}はVIPオーディエンスの一部ですか？
   ```

3. **応答データ: 特定のプロパティの参照**  
   プロンプトには、期待される応答データの特定のプロパティへの参照が含まれるべきです。例えば、`audiences`、`attributes`、または`badges`などです。これにより、MCPツールは使用ケースに必要な関連データのみを返すようになり、明確性が向上し、不要な出力が減少します。例えば：
   ```none
   こちらは訪問のオーディエンスリストです：{response.audiences}
   ```  
   これにより、MCPツールは応答の`audiences`プロパティに焦点を当てるように導かれ、プロンプトの要件に合った出力が保証されます。詳細については、[Moments API: Objects]()を参照してください。

指示に静的パラメーターを組み合わせ、プロンプトに動的パラメーターと特定の応答プロパティを使用することで、MCPサーバーに対して正確で効果的なクエリを作成できます。

## ベストプラクティス

このソリューションから最良の結果を得るために、以下を強く推奨します：

**属性名の使用**（強く推奨）  
デフォルトでは、Moments APIエンジンは数値の属性IDを返しますが、これはLLMにとってコンテキストが不足しています。最良の結果を得るために、エンジンが属性名を返すように構成してください。属性名は記述的であり、LLMが正確に解釈して応答するのに役立ちます。アカウントが広く認識されていない頭字語や略語を使用している場合、LLMはそれらを解釈するのが難しいかもしれません。属性名が記述的であり、人間とAIシステムの両方によって容易に理解できるように、属性名の見直しと更新を検討してください。

属性名を使用することは、LLMベースのソリューションで管理MCPサーバーを活用する唯一の実現可能なアプローチです。詳細については、[Moments API: Objects]()を参照してください。

**専用のMoments APIエンジン**  
他の目的で作成された既存のMoments APIエンジンを再利用しないでください。各管理MCPサーバーの使用ケースに対して別々のエンジンを作成し、そのシナリオに必要な属性、バッジ、およびオーディエンスのみを構成してください。これにより：

* 関連するデータのみが公開され、正確なコンテキストが提供されます。
* 複雑さが減少し、メンテナンスが容易になります。
* 要件が変更された場合の監査と更新が簡単になります。

**特定の訪問データの使用**  
使用ケースに関連しない大量の訪問データをMoments APIエンジンに公開しないでください。特定の使用ケースに不可欠な属性、バッジ、およびオーディエンスのみを含めてください。不要なデータを提供すると、LLMが圧倒され、応答の正確性が低下する可能性があります。関連するデータの焦点を絞ったセットは、明確性と応答品質を向上させます。

## 利用可能なツール

すべてのツールは次のパラメーターをサポートしています：

| パラメーター | 説明 |
| --------- | ----------- |
| `account` | (必須) Tealiumアカウントの名前です。 |
| `profile` | (必須) Tealiumアカウント内のプロファイルの名前です。 |
| `engineId` | (必須) Moments APIエンドポイントのエンジンIDです。 |
| `Origin` | (必須) リクエストを開始した起源です。 |
| `Referer` | (必須) リクエストを開始した絶対または部分的なアドレスです。 |
| `suppressNotFound` | 訪問レコードが見つからない場合の応答タイプを決定します。&lt;br&gt;`false` (デフォルト): HTTPステータスコード `404 Not Found` を返します。&lt;br&gt;`true`: HTTPステータスコード `200 OK` を返し、レスポンスボディが空です。 |

Moments API 管理MCPサーバーには、次のツールが含まれています：

### `getPersonalizationContentByAnonymousId`

Tealiumの匿名IDを使用して訪問データを取得します。詳細については、を参照してください。

| パラメーター | 説明 |
| --------- | ----------- |
| `visitorId` | (必須) 訪問に各訪問または各アプリ使用ごとに割り当てられる一意で匿名の値です。匿名IDは、同じブラウザーやアプリからの複数の訪問を追跡しますが、異なるブラウザーやデバイス間では追跡しません。 |

このツールを使用するには、プロンプトを特に匿名IDに言及するようにフォーマットしてください。例えば：

```none
匿名訪問{visitor_id}は何に興味がありますか？
```

### `getPersonalizationContentByVisitorId`

訪問ID属性を指定して訪問データを取得します。属性IDと属性検索値を指定します。詳細については、を参照してください。

| パラメーター | 説明 |
| --------- | ----------- |
| `attributeId` | (必須) [訪問ID属性]()を表す数値UIDです。 |
| `attributeValue` | (必須) 検索する属性の値です。 |

このツールを使用するには、プロンプトを特に属性IDと値を検索するようにフォーマットしてください。例えば：

```none
訪問属性ID {visitor_attribute_id} と値 {visitor_attribute_value} は何に興味がありますか？
```
## OpenAIエージェントSDKソリューション

以下のサンプルコードは、Python用OpenAIエージェントを使用してMoments API管理MCPサーバーに接続し、訪問に関する質問をする方法を示しています。エージェントの指示には、リクエストに関連する静的パラメータが指定されています。プロンプトでは、訪問の匿名IDが既知であると仮定しています。

詳細については、[OpenAI Agents SDK: モデルコンテキストプロトコル（MCP）](https://openai.github.io/openai-agents-python/mcp/)を参照してください。



```python
import asyncio
import os

from agents import Agent, HostedMCPTool, Runner

async def main() -&gt; None:
    agent = Agent(
        name=&#34;Assistant&#34;,
        instructions=f&#34;&#34;&#34;
                Tealium MCPツールを使用して質問に答えてください。
                Tealiumアカウント: my_account
                Tealiumプロファイル: my_profile
                TealiumエンジンID: engine_001
                &#34;&#34;&#34;,
        tools=[
            HostedMCPTool(
                tool_config={
                    &#34;type&#34;: &#34;mcp&#34;,
                    &#34;server_label&#34;: &#34;tealium_personalization_mcp&#34;,
                    &#34;server_url&#34;: &#34;https://us-west-2.prod.developer.tealiumapis.com/v1/personalization/mcp&#34;,
                    &#34;require_approval&#34;: &#34;never&#34;,
                    &#34;headers&#34;: {
                        &#34;X-Tealium-Api-Key&#34;: os.getenv(&#39;TEALIUM_API_KEY&#39;),
                        &#34;Origin&#34;: &#34;https://example.com&#34;,
                        &#34;Referer&#34;: &#34;https://example.com&#34;
                    }
                }
            )
        ],
    )

    anon_visitor_id = &#39;1234567&#39;
    query = f&#39;&#39;&#39;
    匿名訪問{anon_visitor_id}はVIPオーディエンスの一部ですか？こちらが訪問のオーディエンスリストです: {response.audiences}
    &#39;&#39;&#39;
    result = await Runner.run(agent, query)
    print(result.final_output)

if __name__ == &#34;__main__&#34;:
    asyncio.run(main())
```



```python
import asyncio
import os

from agents import Agent, Runner
from agents.mcp import MCPServerStreamableHttp
from agents.model_settings import ModelSettings

async def main() -&gt; None:
    api_key = os.environ[&#34;TEALIUM_API_KEY&#34;]

    async with MCPServerStreamableHttp(
            name=&#34;Tealium MCP Streamable HTTP Server&#34;,
            params={
                &#34;url&#34;: &#34;https://us-west-2.prod.developer.tealiumapis.com/v1/personalization/mcp&#34;,
                &#34;headers&#34;: {
                    &#34;X-Tealium-Api-Key&#34;: api_key,
                    &#34;Origin&#34;: &#34;https://example.com&#34;,
                    &#34;Referer&#34;: &#34;https://example.com&#34;
                },
                &#34;timeout&#34;: 10,
            },
            max_retry_attempts=3
    ) as server:
        agent = Agent(
            name=&#34;Assistant&#34;,
            instructions=f&#34;&#34;&#34;
                Tealium MCPツールを使用して質問に答えてください。
                Tealiumアカウント: my_account
                Tealiumプロファイル: my_profile
                TealiumエンジンID: engine_001
                &#34;&#34;&#34;,
            mcp_servers=[server],
            model_settings=ModelSettings(tool_choice=&#34;required&#34;),
        )

        anon_visitor_id = &#39;1234567&#39;
        query = f&#39;&#39;&#39;
        匿名訪問{anon_visitor_id}はVIPオーディエンスの一部ですか？こちらが訪問のオーディエンスリストです: {response.audiences}
        &#39;&#39;&#39;
        result = await Runner.run(agent, query)
        print(result.final_output)

if __name__ == &#34;__main__&#34;:
    asyncio.run(main())
```



## MCPサーバーをMCPインスペクターでテストする

MCPサーバーに接続するために、オープンソースのMCPインスペクターなどのツールを使用することをお勧めします。

MCPインスペクターを使用して：

* サーバー接続を確認します。
* 利用可能なツールとそのパラメータを確認します。
* 認証または構成の問題をトラブルシューティングします。
* MCPベースの統合の開発を加速します。

詳細については、[モデルコンテキストプロトコル &gt; 入門](https://modelcontextprotocol.io/docs/tools/inspector#getting-started)を参照してください。

MCPインスペクターを実行し、MCPサーバーをテストするには：

1. ターミナルを開き、次のコマンドを実行します：
    ```
    npx @modelcontextprotocol/inspector
    ```
    これにより、MCPインスペクターがインストールされ、ブラウザウィンドウでツールが開きます。
1. **Transport Type**に`Streamable HTTP`を構成します。
1. **URL**に`https://us-west-2.prod.developer.tealiumapis.com/v1/personalization/mcp`を構成します。リージョンはMoments APIエンジンのリージョンと一致する必要があります。
1. **Custom Headers**の下に、`X-Tealium-Api-Key`キーとMCPサーバーAPIキーを追加します。MCP APIキーはMCPサーバーアクセス専用のAPIキーであり、Tealiumサポートから要求する必要があります。

![](/images/server-side/moments-api/moments-mcp-server-inspector-config.png)

**Connect**をクリックすると、ステータスが**Connected**に更新され、**List Tools**ボタンが表示されます。

サーバーでツールを実行するには：

1. **List Tools**をクリックして利用可能なツールを確認します。
1. ツールをクリックしてその定義を確認します。
1. 必要なパラメータの値を入力します。
1. **Run Tool**をクリックします。
1. **Tool Result**の下に、`Success`メッセージとMoments APIの結果が表示されます。