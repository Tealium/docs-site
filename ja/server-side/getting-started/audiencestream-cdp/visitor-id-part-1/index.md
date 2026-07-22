---
title: 訪問ID パート1
description: このステップでは、訪問ID属性を安全に作成する方法を示し、オーディエンスディスカバリーを紹介します。これにより、最終決定を行う前にアイデンティティ解決戦略を検証できます。
url: https://docs.tealium.com/ja/server-side/getting-started/audiencestream-cdp/visitor-id-part-1/
---
この例では、前のステップからの要件に基づいて、ユーザー登録イベント中にメールアドレスをキャプチャします。

## メールアドレスのキャプチャ

このステップでは、すでに `email_address` のイベント属性と、それを送信する `user_register` というイベントがあることを前提としています。ここから、メールアドレスのための文字列訪問属性を作成し、オーディエンスディスカバリーでテストした後、最終的な訪問ID属性を作成します。

1. **Transform > Visitor / Visit Attributes** に移動し、**+ Add Attribute** をクリックします。
1. スコープを **Visitor** に構成し、**Continue** をクリックします。
1. データタイプ **String** を選択し、**Continue** をクリックします。
1. 属性名に `Email Address` を入力します。
1. **Add Enrichment** をクリックし、**Set String** を選択して、イベント変数 `email_address` に **Visitor String** を構成します。
1. **WHEN** は **Any Event** のままにして、**Create a New Rule** をクリックします。
1. 例えば、次のようなルールを作成します：

[
  [
    {
      "input": "tealium_event",
      "operator": "equals",
      "filter": "user_register"
    }
  ]
]

1. **Finish** をクリックし、その後 **Save** をクリックします。

これで、適格なイベント中に顧客のメールアドレスをキャプチャする訪問属性ができました。このロジックを他の資格イベント（購入やリードフォームなど）にも拡張することができます。

この時点で、アカウントを保存して公開し、オーディエンスストリームがこのデータの収集を開始するのを数日待ちます。十分なサンプルデータが得られたら、オーディエンスディスカバリーを使用してアイデンティティ解決戦略を検証し、訪問ID属性でそれを最終決定します。

データ検証のためのオーディエンスディスカバリーの使用方法を学ぶには、**Visitor ID Discovery** をクリックしてください。