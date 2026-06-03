---
title: Webhook - Kony API
description: Kony APIのための高度なWebhook - テンプレート変数を使用したカスタムリクエストアクションの構成方法
url: https://docs.tealium.com/ja/server-side/connectors/webhook-connectors/vendor-examples/webhook-kony-api/
---
## 概要

購読者IDのリストと名前と値のペアを持つhttpリクエストをKonyに送信します。リクエストボディ全体はJSONメッセージです。

## ベンダーの要件

### サンプルのJSONメッセージ:

```json
{
    &#34;messageRequest&#34;: {
        &#34;appId&#34;: &#34;IceMobile&#34;,
        &#34;global&#34;: {},
        &#34;messages&#34;: {
            &#34;message&#34;: {
                &#34;content&#34;: {
                    &#34;priorityService&#34;: &#34;false&#34;,
                    &#34;data&#34;: &#34;Message Body&#34;,
                    &#34;mimeType&#34;: &#34;text/plain&#34;
                },
                &#34;overrideMessageId&#34;: 0,
                &#34;startTimestamp&#34;: 0,
                &#34;expiryTimestamp&#34;: 0,
                &#34;subscribers&#34;: {
                    &#34;subscriber&#34;: [
                        {
                            &#34;ksid&#34;: &#34;95784&#34;
                        },
                        {
                            &#34;ksid&#34;: &#34;97899&#34;
                        }
                    ]
                },
                &#34;platformSpecificProps&#34;: {
                    &#34;iphone&#34;: {
                        &#34;badge&#34;: 0,
                        &#34;customData&#34;: {
                            &#34;key&#34;: [
                                {
                                    &#34;name&#34;: &#34;trip_type&#34;,
                                    &#34;content&#34;: &#34;o&#34;
                                },
                                {
                                    &#34;name&#34;: &#34;o&#34;,
                                    &#34;content&#34;: &#34;LAX&#34;
                                },
                                {
                                    &#34;name&#34;: &#34;d&#34;,
                                    &#34;content&#34;: &#34;NRT&#34;
                                },
                                {
                                    &#34;name&#34;: &#34;dd&#34;,
                                    &#34;content&#34;: &#34;2016-01-09&#34;
                                },
                                {
                                    &#34;name&#34;: &#34;rd&#34;,
                                    &#34;content&#34;: &#34;2016-01-20&#34;
                                }
                            ]
                        }
                    }
                },
                &#34;type&#34;: &#34;PUSH&#34;
            }
        }
    }
}

```

#### ノート

* 購読者の配列は動的で、1つ以上の購読者IDを含むことができます。
* &#34;customData&#34;キーの配列は動的で、1つ以上の名前とコンテンツのオブジェクトを含むことができます。

## アクションの実装

### メソッドフィールド

`POST`に構成します。

### URLフィールド

PutsReqバケットURLに構成します。

一般的な実装をここで示すために、PutsReq URLが適しています。Kony APIのドキュメンテーションを参照してURLを確認してください。

### ボディコンテンツタイプ

`application/json`オプションを選択します。

### ボディデータ

`Body`オプションを選択し、テンプレート参照を提供します。

|名前| 値|
|---| ---|
|`Body`| `{{json_template}}`|

### テンプレート変数

テンプレートで参照され、置換される名前と値のペアを構成します。

|名前| 値| ノート|
|---| ---| ---|
|`subscribers.ksid`| Kony Sub IDs| 文字列のセット属性|
|`customData.name`| Kony Data Names| 文字列のセット属性|
|`customData.content`| Kony Data Contents| 文字列のセット属性|

変数は内部的にJSONに変換され、すべてのテンプレートで利用可能になります。

#### 結果のJSON構造:

```json
{
    &#34;subscribers&#34;: [
        {
            &#34;ksid&#34;: &#34;sub-id-1&#34;
        },
        {
            &#34;ksid&#34;: &#34;sub-id-2&#34;
        }
    ],
    &#34;customData&#34;: [
        {
            &#34;name&#34;: &#34;name-1&#34;,
            &#34;content&#34;: &#34;Content A&#34;
        },
        {
            &#34;name&#34;: &#34;name-2&#34;,
            &#34;content&#34;: &#34;Content B&#34;
        },
        {
            &#34;name&#34;: &#34;name-3&#34;,
            &#34;content&#34;: &#34;Content C&#34;
        }
    ]
}

```

### テンプレート

`json_template`  

```json
{
    &#34;messageRequest&#34;: {
        &#34;appId&#34;: &#34;IceMobile&#34;,
        &#34;global&#34;: {},
        &#34;messages&#34;: {
            &#34;message&#34;: {
                &#34;content&#34;: {
                    &#34;priorityService&#34;: &#34;false&#34;,
                    &#34;data&#34;: &#34;Message Body&#34;,
                    &#34;mimeType&#34;: &#34;text/plain&#34;
                },
                &#34;overrideMessageId&#34;: 0,
                &#34;startTimestamp&#34;: 0,
                &#34;expiryTimestamp&#34;: 0,
                &#34;subscribers&#34;: {
                    &#34;subscriber&#34;: [
                        {{#subscribers}}
                        {
                            &#34;ksid&#34;: &#34;{{ksid}}&#34;
                        }{{#iter.hasNext}}, {{/iter.hasNext}}
                        {{/subscribers}}
                    ]
                },
                &#34;platformSpecificProps&#34;: {
                    &#34;iphone&#34;: {
                        &#34;badge&#34;: 0,
                        &#34;customData&#34;: {
                            &#34;key&#34;: [
                                {{#customData}}
                                {
                                    &#34;name&#34;: &#34;{{name}}&#34;,
                                    &#34;content&#34;: &#34;{{content}}&#34;
                                }{{#iter.hasNext}}, {{/iter.hasNext}}
                                {{/customData}}
                            ]
                        }
                    }
                },
                &#34;type&#34;: &#34;PUSH&#34;
            }
        }
    }
}
```

### レンダリングされたテンプレート

内部的にテンプレートがレンダリングされ、参照された場所にその内容が注入されます。

`json_template`  

```json
{
    &#34;messageRequest&#34;: {
        &#34;appId&#34;: &#34;IceMobile&#34;,
        &#34;global&#34;: {},
        &#34;messages&#34;: {
            &#34;message&#34;: {
                &#34;content&#34;: {
                    &#34;priorityService&#34;: &#34;false&#34;,
                    &#34;data&#34;: &#34;Message Body&#34;,
                    &#34;mimeType&#34;: &#34;text/plain&#34;
                },
                &#34;overrideMessageId&#34;: 0,
                &#34;startTimestamp&#34;: 0,
                &#34;expiryTimestamp&#34;: 0,
                &#34;subscribers&#34;: {
                    &#34;subscriber&#34;: [
                        {
                            &#34;ksid&#34;: &#34;sub-id-1&#34;
                        },
                        {
                            &#34;ksid&#34;: &#34;sub-id-2&#34;
                        }
                    ]
                },
                &#34;platformSpecificProps&#34;: {
                    &#34;iphone&#34;: {
                        &#34;badge&#34;: 0,
                        &#34;customData&#34;: {
                            &#34;key&#34;: [
                                {
                                    &#34;name&#34;: &#34;name-1&#34;,
                                    &#34;content&#34;: &#34;Content A&#34;
                                },
                                {
                                    &#34;name&#34;: &#34;name-2&#34;,
                                    &#34;content&#34;: &#34;Content B&#34;
                                },
                                {
                                    &#34;name&#34;: &#34;name-3&#34;,
                                    &#34;content&#34;: &#34;Content C&#34;
                                }
                            ]
                        }
                    }
                },
                &#34;type&#34;: &#34;PUSH&#34;
            }
        }
    }
}
```

## アクション構成のスクリーンショット

![](/images/server-side/example)
