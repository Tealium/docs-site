---
title: iQ GETプロファイルAPI
description: iQ GETプロファイルAPIは、iQタグ管理アカウントのプロファイルを取得し、特定の構成コンポーネントとバージョン履歴を含みます。
url: https://docs.tealium.com/ja/api/v3/iq-profiles/iq-get-profile-api/
---
## 動作方法

GETメソッドを使用してアカウントプロファイルを取得します：

```bash
GET /v3/tiq/accounts/{ACCOUNT}/profiles/{PROFILE}?includes={INCLUDE}&amp;publishVersion={PUBLISH_VERSION}
```

## 認証

Bearerトークンは、すべてのAPI呼び出しを認証するために使用され、APIキーは認証呼び出しでのみ使用されます。Bearerトークンに加えて、認証応答には、後続のサーバーサイドAPI呼び出しで使用する必要がある地域固有のホスト名が含まれています。

APIキーからBearerトークンを生成する方法については、[認証]()を参照してください。

## GET操作のパラメータ

このコマンドは以下のパラメータを使用します：

|パラメータ| タイプ| 必須| 説明|
|---| ---| ---| ---|
|publishVersion| 文字列| 任意| 取得するプロファイルのバージョンID。このパラメータを省略すると、最新のバージョンが取得されます。&lt;br&gt; バージョンIDは `YYYYMMDDhhmm` の形式です&lt;br&gt; 例：`&#34;202202111806&#34;`|
|includes| 配列| 任意| 応答に含める構成コンポーネントの配列。含める各コンポーネントに対してこのクエリ文字列パラメータを追加します。&lt;br&gt; 例えば、変数と拡張機能を取得するには：`&amp;includes=variables&amp;includes=extensions` デフォルト：なし&lt;br&gt; 値：`loadRules`, `tags`, `tags.templateList`, `tags.template`, `extensions`, `variables`, `events` , および `versionIDs` |

 プロファイルのタグテンプレートリストを取得するには、GETリクエストに `tags` と `tags.templateList` を含める必要があります。例えば、`&amp;includes=tags&amp;includes=tags.templateList`。&lt;br&gt; タグテンプレート自体を取得するには、`tags` と `tags.template` を含めます。例えば、`&amp;includes=tags&amp;includes=tags.template`。 

### cURLリクエストの例

```bash
curl -H &#39;Authorization: Bearer {token}&#39; \
https://platform.tealiumapis.com/v3/tiq/accounts/{ACCOUNT}/profiles/{PROFILE}?includes=loadRules&amp;includes=extensions&amp;includes=tags&amp;includes=tags.template&amp;includes=variables&amp;includes=events&amp;includes=versionIds&amp;publishVersion=202003161355
```
### 例の応答



```json
{
    &#34;account&#34;: &#34;my_account&#34;,
    &#34;profile&#34;: &#34;main&#34;,
    &#34;versionTitle&#34;: &#34;Version 2022.03.22.2108&#34;,
    &#34;version&#34;: &#34;202203222108&#34;,
    &#34;minorVersion&#34;: &#34;202203222108&#34;,
    &#34;parentVersion&#34;: &#34;202309191127&#34;,
    &#34;creation&#34;: &#34;202201131654&#34;,
    &#34;customTargets&#34;: null,
    &#34;versionDetails&#34;: {
        &#34;environmentVersions&#34;: {
            &#34;qa&#34;: true,
            &#34;prod&#34;: false,
            &#34;dev&#34;: true
        },
        &#34;user&#34;: &#34;user1@tealium.com&#34;,
        &#34;notes&#34;: &#34;&#34;
    },
    &#34;environmentVersions&#34;: {
        &#34;qa&#34;: &#34;202203222108&#34;,
        &#34;prod&#34;: &#34;202203222108&#34;,
        &#34;dev&#34;: &#34;202203222108&#34;
    },
    &#34;dataCloudLinkedProfiles&#34;: &#34;{}&#34;,
    &#34;libraryType&#34;: &#34;NONE&#34;,
    &#34;linkedProfiles&#34;: null,
    &#34;linkedLibraries&#34;: [
        {
            &#34;environment&#34;: &#34;Dev&#34;,
            &#34;name&#34;: &#34;LibraryName&#34;,
            &#34;required&#34;: true
        },
        {
            &#34;environment&#34;: &#34;Prod&#34;,
            &#34;name&#34;: &#34;LibraryName&#34;,
            &#34;required&#34;: true
        }
    ],
    &#34;variables&#34;:[
        {
            &#34;id&#34;: 37,
            &#34;uniqueIdentifier&#34;: &#34;dom.viewport_height&#34;,
            &#34;name&#34;: &#34;viewport_height&#34;,
            &#34;alias&#34;: &#34;Viewport Height&#34;,
            &#34;type&#34;: &#34;dom&#34;,
            &#34;notes&#34;: null,
            &#34;context&#34;: null,
            &#34;library&#34;: null,
            &#34;imported&#34;: null,
            &#34;usedIn&#34;: {
                &#34;tags&#34;: [],
                &#34;events&#34;: [],
                &#34;extensions&#34;: [],
                &#34;consent&#34;: [],
                &#34;loadRules&#34;: [, &#34;/ja/early-access/api/api-v3/iq-profiles/iq-get-profile-api&#34;]
            }
        }
    ],
   &#34;loadRules&#34;:[
        {
            &#34;id&#34;:2,
            &#34;name&#34;:&#34;US Site Only&#34;,
            &#34;status&#34;:&#34;active&#34;,
            &#34;library&#34;: null,
            &#34;notes&#34;: &#34;notes 1&#34;,
            &#34;startDate&#34;: &#34;202203010000&#34;,
            &#34;endDate&#34;: &#34;202203152359&#34;,
            &#34;environmentVersions&#34;: {
                &#34;qa&#34;: &#34;202203222108&#34;,
                &#34;prod&#34;: &#34;202203222108&#34;,
                &#34;dev&#34;: &#34;202203222108&#34;
            },
            &#34;usedIn&#34;: {
                &#34;tags&#34;: [],
                &#34;extensions&#34;: [],
                &#34;consent&#34;: [
                   &#34;gdpr&#34;
                ],
                &#34;loadRules&#34;: null
            },
            &#34;loadRuleCondition&#34;: [
                [
                    {
                        &#34;variable&#34;: &#34;js.variable1&#34;,
                        &#34;operator&#34;: &#34;contains&#34;,
                        &#34;value&#34;: &#34;1&#34;
                    },
                    {
                        &#34;variable&#34;: &#34;js.order_discount&#34;,
                        &#34;operator&#34;: &#34;does_not_equal&#34;,
                        &#34;value&#34;: &#34;2&#34;
                    },
                ],
                [
                    {
                        &#34;variable&#34;: &#34;dom.viewport_height&#34;,
                        &#34;operator&#34;: &#34;does_not_end_with_ignore_case&#34;,
                        &#34;value&#34;: &#34;3&#34;},
                    {
                        &#34;variable&#34;: &#34;meta.metadata&#34;,
                        &#34;operator&#34;: &#34;does_not_equal_ignore_case&#34;,
                        &#34;value&#34;: &#34;7&#34;
                    }
                ],
            , &#34;/ja/early-access/api/api-v3/iq-profiles/iq-get-profile-api&#34;]
        }
    ],
    &#34;extensions&#34;:[
       {
            &#34;id&#34;:4,
            &#34;extensionId&#34;: 100036,
            &#34;extenstionType&#34;: &#34;Javascript Code&#34;,
            &#34;name&#34;: &#34;Build Data Layer&#34;,
            &#34;library&#34;: &#34;synclib&#34;,
            &#34;scope&#34;: &#34;Pre Loader&#34;,
            &#34;occurrence&#34;: &#34;Run Always&#34;,
            &#34;notes&#34;: &#34;&#34;,
            &#34;loadRule&#34;: null,
            &#34;status&#34;:&#34;active&#34;,
            &#34;selectedTargets&#34;: {
                &#34;qa&#34;: true,
                &#34;prod&#34;: true,
                &#34;dev&#34;: true
            },
            &#34;environmentVersions&#34;: {
                &#34;qa&#34;: &#34;202204072336&#34;,
                &#34;prod&#34;: &#34;202204072336&#34;,
                &#34;dev&#34;: &#34;202204072336&#34;
            },
            &#34;conditions&#34;:null,
            &#34;configuration&#34;: [, &#34;/ja/early-access/api/api-v3/iq-profiles/iq-get-profile-api&#34;]
       },
       {
            &#34;id&#34;:70,
            &#34;extensionId&#34;: 100036,
            &#34;type&#34;:&#34;Set Data Values&#34;,
            &#34;name&#34;:&#34;Set Checkout Step 1 Complete Event&#34;,
            &#34;library&#34;: &#34;synclib&#34;,
            &#34;status&#34;:&#34;inactive&#34;,
            &#34;scope&#34;:&#34;global&#34;,
            &#34;occurrence&#34;: &#34;Run Always&#34;,
            &#34;notes&#34;:&#34;&#34;,
            &#34;loadRule&#34;: null,
            &#34;selectedTargets&#34;: {
                &#34;qa&#34;: true,
                &#34;prod&#34;: true,
                &#34;dev&#34;: true
            },
            &#34;environmentVersions&#34;: {
                &#34;qa&#34;: &#34;202204072336&#34;,
                &#34;prod&#34;: &#34;202204072336&#34;,
                &#34;dev&#34;: &#34;202204072336&#34;
            },
            &#34;conditions&#34;:null,
            &#34;configuration&#34;: [, &#34;/ja/early-access/api/api-v3/iq-profiles/iq-get-profile-api&#34;]
       }
    ],
    &#34;tags&#34;:[
        {
            &#34;id&#34;: &#34;322&#34;,
            &#34;tagId&#34;:&#34;20048&#34;,
            &#34;tagName&#34;:&#34;Twitter&#34;,
            &#34;name&#34;:&#34;Twitter&#34;,
            &#34;library&#34;: null,
            &#34;status&#34;:&#34;active&#34;,
            &#34;notes&#34;:&#34;&#34;,
            &#34;loadRule&#34;:&#34;50,3&#34;,
            &#34;loadRuleJoinOperator&#34;:&#34;all&#34;,
            &#34;dataMappings&#34;:[
                { 
                    &#34;mappings&#34;: [
                        &#34;a1&#34;,
                        &#34;a2&#34;
                    ],
                    &#34;type&#34;: &#34;dom&#34;,
                    &#34;variable&#34;: &#34;title&#34;
                },
                {
                    &#34;mappings&#34;: [
                        &#34;a3&#34;,
                        &#34;a4&#34;
                    ],
                    &#34;type&#34;: &#34;static.text&#34;,
                    &#34;variable&#34;: &#34;height&#34;
                }
            ],
            &#34;selectedTargets&#34;: {
                &#34;qa&#34;: true,
                &#34;prod&#34;: true,
                &#34;dev&#34;: true
            },
            &#34;environmentVersions&#34;: {
                &#34;qa&#34;: &#34;202203222108&#34;,
                &#34;prod&#34;: &#34;202203222108&#34;,
                &#34;dev&#34;: &#34;202203222108&#34;
            },
            &#34;advancedConfiguration&#34;: {
                &#34;bundleFlag&#34;: false,
                &#34;syncLoadType&#34;: true,
                &#34;optOut&#34;: true,
                &#34;sendFlag&#34;: true,
                &#34;scriptSource&#34;: &#34;&#34;,
                &#34;tagTiming&#34;: &#34;DOM Ready&#34;
            },
            &#34;configuration&#34;: {
                &#34;config_EMUserSecret&#34;: &#34;&#34;,
                &#34;multipleLoadRules&#34;: &#34;3,2&#34;,
                &#34;_multipleLoadRules&#34;: &#34;3,2&#34;
           },
           &#34;rules&#34;: {
               &#34;apply&#34;: null,
               &#34;exclude&#34;: null
           },
           &#34;template&#34;: null
       }
    ],
    &#34;events&#34;: [
        {
            &#34;id&#34;: 25,
            &#34;eventId&#34;: 100045,
            &#34;name&#34;: &#34;Home and Decor Homepage Click&#34;,
            &#34;status&#34;: &#34;active&#34;,
            &#34;eventType&#34;: &#34;mouseevents&#34;,
            &#34;scope&#34;: &#34;DOM Ready&#34;,
            &#34;trackingEvent&#34;: &#34;link&#34;,
            &#34;notes&#34;: &#34;&#34;,
            &#34;library&#34;: null,
            &#34;eventLoadRuleList&#34;: &#34;all&#34;,
            &#34;eventTrigger&#34;: {
                &#34;object&#34;: &#34;mouseevents&#34;,
                &#34;cssSelector&#34;: &#34;&#34;,
                &#34;title&#34;: &#34;Mouse Events&#34;,
                &#34;mouseEvent&#34;: &#34;mousedown&#34;,
                &#34;triggerFrequency&#34;: &#34;runAlways&#34;
            },
            &#34;selectedTargets&#34;: {
                &#34;prod&#34;: true,
                &#34;dev&#34;: true,
                &#34;qa&#34;: true
            },
            &#34;environmentVersions&#34;: {
                &#34;qa&#34;: &#34;202301202252&#34;,
                &#34;prod&#34;: &#34;202301202252&#34;,
                &#34;dev&#34;: &#34;202301202252&#34;
            },
            &#34;eventVariables&#34;: [
                {
                    &#34;variable&#34;: &#34;udo.tealium_event&#34;,
                    &#34;type&#34;: &#34;text&#34;,
                    &#34;value&#34;: &#34;mousedown&#34;
                }
            ],
            &#34;rules&#34;: {
                &#34;apply&#34;: null,
                &#34;exclude&#34;: null
            },
            &#34;usedIn&#34;: {
                &#34;tags&#34;: [],
                &#34;events&#34;: null,
                &#34;extensions&#34;: null,
                &#34;consent&#34;: null,
                &#34;loadRules&#34;: null
            }
        }
    ],
    &#34;versionIds&#34;: [
        &#34;202309191128&#34;,
        &#34;202309191127&#34;,
        &#34;202309061342&#34;
    ],
    &#34;templateList&#34;: null
}
```

### エラーメッセージ

このエンドポイントの潜在的なエラーメッセージ：

|エラーコード| エラーメッセージ|
|---| ---|
|400|  `&#34;プロファイルライブラリが古くなっています。プロファイルをパッチする前に変更をマージしてください - {ACCOUNT} \| プロファイル: {PROFILE}&#34;`&lt;br&gt;  `&#34;変数の検証に失敗しました - variableId: {VARIABLE ID} \| {ACCOUNT} \| プロファイル: {PROFILE}. 原因: {cause}&#34;` |
|404|  `&#34;プロファイルが見つかりません - アカウント: {ACCOUNT} \| プロファイル: {PROFILE}&#34;`&lt;br&gt;   `&#34;プロファイルライブラリが見つかりません - アカウント: {ACCOUNT} \| プロファイル: {PROFILE}&#34;` &lt;br&gt;   `&#34;プロファイル（レガシー）が見つかりません - アカウント: {ACCOUNT} \| プロファイル: {PROFILE}&#34;` &lt;br&gt;      `&#34;次の拡張IDの取得エラー - {ACCOUNT} プロファイル: {PROFILE}&#34;`  |
|409|`&#34;同じアカウントを現在他のユーザーが閲覧中です: {ACCOUNT} \| プロファイル: {PROFILE}&#34;` &lt;br&gt;  `&#34;プロファイル拡張との競合: _id: {ID}, extType: {TYPE}, name: {NAME} - {ACCOUNT} \| プロファイル: {PROFILE}&#34;` |
|500|  `&#34;拡張のためのjson処理エラー - アカウント: {ACCOUNT} \| プロファイル: {PROFILE}&#34;` |