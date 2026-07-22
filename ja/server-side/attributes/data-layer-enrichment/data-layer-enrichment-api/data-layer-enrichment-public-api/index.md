---
title: データレイヤーエンリッチメント公開APIについて
description: データレイヤーエンリッチメント公開APIは、訪問がアクティブな訪問中に既知の訪問IDの訪問プロファイルを取得することができます。データレイヤーエンリッチメント公開APIとCustomer Data Hub Profile Definition APIを組み合わせることで、ウェブサイトでのパーソナライゼーション体験を向上させることができます。
url: https://docs.tealium.com/ja/server-side/attributes/data-layer-enrichment/data-layer-enrichment-api/data-layer-enrichment-public-api/
---
### 仕組み

データレイヤーエンリッチメント公開APIがリクエストを受け取ると、APIはCustomer Data Hubプロファイルにホワイトリスト化されたドメインがあるかどうかを確認します。ホワイトリストが利用可能な場合、データレイヤーエンリッチメント公開APIはリファラーとホワイトリスト化されたドメインを一致させようとします。

APIの検証は、プロファイルによって以下の結果を返すことがあります：

* ホワイトリストが見つからない  
ホワイトリストが利用可能でない場合、データレイヤーエンリッチメント公開APIはURLの訪問IDを使用します。
* ホワイトリストが見つかり、ドメインが一致する  
リファラーとホワイトリスト化されたドメインが一致する場合、データレイヤーエンリッチメント公開APIはサードパーティのTAPIDクッキーから訪問IDを取得します。
* ホワイトリストが見つかり、ドメインが一致しない  
リファラーとホワイトリスト化されたドメインが一致しない場合、データレイヤーエンリッチメント公開APIはURLから訪問IDを取得します。

データレイヤーエンリッチメント公開APIは、リファラーがホワイトリスト化されたドメインと一致する場合はTAPIDクッキーを使用し、それ以外の場合はURLから訪問IDを使用します。

### 次のページのパーソナライゼーション

Customer Data Hub Profile Definition APIとデータレイヤーエンリッチメント公開APIを組み合わせることで、ウェブサイト訪問のパーソナライズ体験を向上させることができます。この例では、コンテンツ管理システム（CMS）を使用したウェブサイトで次のページのパーソナライゼーションを有効にしたいと考えています。

既知の訪問IDのCustomer Data Hubプロファイルを取得するには、CMSで自動スクリプトを定期的に（例えば、1時間ごとに）実行してCustomer Data Hub Profile Definition APIをトリガーします。APIは、訪問に割り当てられる可能性のあるオーディエンスとバッジをインポートします。CMSは、データレイヤーエンリッチメント公開APIと共に使用するためのオーディエンスとバッジ情報を保存します。

この情報はCMS内に保存され、以下のステップで継続的に参照されます：

1. 訪問IDをキャプチャする以下のコードを実行するスクリプトをCMSに作成します：  

      ```
      document.cookie.match(https://docs.tealium.com/v_id:([^$]+)/)[1]
      ```

 スクリプトはページのロード時に実行され、CMSがすでに訪問IDを持っていない場合にのみ実行されます。  
このスクリプトは、`utag_main`クッキー名前空間から`v_id`キーの値をインポートします。これは`utag.data["cp.utag_main_v_id"]`とも呼ばれます。  

<blockquote>
スクリプトにインポートされるアカウントとプロファイルは、AudienceStreamのアカウントとプロファイルを指します。多くのクライアントは、AudienceStreamのプロファイルと異なるTealium iQタグ管理プロファイルを持っています。例えば、Tealium iQのプロファイル`tealium/audiencestream`と`tealium/tiq`は、AudienceStreamのプロファイル`tealium/main`を指すことがあります。
</blockquote>


1. データレイヤーエンリッチメント公開APIをトリガーします。

1. データレイヤーエンリッチメント公開APIのレスポンスを、Customer Data Hub Profile Definition APIのレスポンスと照らし合わせて、どのオーディエンスとバッジが特定の訪問に割り当てられているかを確認します。この比較により、以下のパーソナライゼーションアクションを実装することができます：

      * ページ8では、訪問にAudienceStreamの"Sample Badge"が割り当てられています。
      * ページ9では、ページのレンダリング前に、CMSがデータレイヤーエンリッチメント公開APIに呼び出しをトリガーし、次のページのパーソナライゼーションのための最新のプロファイルをキャプチャします。

### Customer Data Hub Profile Definition APIを使用して訪問プロファイルを取得する

返される訪問プロファイルには、`metrics 5117`のような属性IDが含まれています。データレイヤーがエンドユーザーにとって意味のあるものを表示するためには、Customer Data Hubプロファイル定義を取得し、属性IDをCustomer Data Hub Profile Definition APIを使用して属性名に変換することができます。

Customer Data Hubプロファイル定義を取得するには、以下のGETコマンドを使用します：

```
    GET http(s)://visitor-service.tealiumiq.com/datacloudprofiledefinitions/{account}/{profile}

```

#### 例のレスポンス

```json
    {
        "audiences" : [
            {
                "id" : "tealiummobile_demo_101",
                "name" : "Sample Audience"
            }
        ],
        "badges" : [
            {
                "id" : 5113,
                "name" : "Sample Badge"
            },
            {
                "id" : 32,
                "name" : "Unbadged"
            },
            {
                "id" : 31,
                "name" : "Frequent visitor"
            },
            {
                "id" : 30,
                "name" : "Fan"
            }
        ]
    }

```


<blockquote>
この例では、オーディエンスとバッジの定義のみが返されます。前の例に`visitor_id`パラメータを追加することもできます。この方法を使用すると、指定された訪問が現在アクティブでない限り、レスポンスは空になります。
</blockquote>


### ドメインのホワイトリスト化

デフォルトでは、データレイヤーエンリッチメント公開APIはすべてのドメインからのリクエストを受け入れます。特定のドメインからのこれらのリクエストを制限したい場合は、Customer Data Hubプロファイルでそれらをホワイトリスト化します。ホワイトリスト化は、信頼できないドメインがTAPIDクッキーの訪問情報にアクセスするのを防ぎます。訪問がホワイトリスト外の潜在的に悪意のある任意のドメインに移動すると、データレイヤーエンリッチメント公開APIはURLパスの訪問IDのみを使用します。

ドメインをホワイトリスト化すると、そのすべてのサブドメインが自動的に含まれます。例えば、`example.com`をホワイトリスト化すると、`*****.example.com`に一致する任意のサブドメインが含まれます。

#### サブドメインの例

```
 http://example.com
 https://mobile.example.com/xyz/index.html
 http://app.mobile.example.com

```

Customer Data Hubプロファイルでホワイトリストを作成するには、以下の手順を完了します：

1. Customer Data Hubプロファイルに移動します。
1. 画面右上の歯車アイコンから**Data Layer Enrichment**を選択します。
1. 信頼するドメインのカンマ区切りリストを入力します。プロファイルごとに最大250のドメインを追加することができます。  
ドメインの前に`http`または`https`プロトコルを挿入しないでください。
1. **Save**をクリックします。
1. **Save/Publish**をクリックして変更を保存し、公開します。

### TAPIDの問題と訪問の切り替え

AudienceStreamは、`TAPID`クッキーのIDを他のIDよりも優先して訪問プロファイルを使用するためのIDとし、エンドポイントがIDの優先順位をどのように扱うかを制御するパラメータを提供します。

例えば、ユーザーがログインし、そのIDが`TAPID`クッキーに追加されると、そのデバイスのすべての匿名ユーザーからのトラフィックがそのユーザーにログされます。2人目のユーザーがそのデバイスに匿名クッキーでログインすると、AudienceStreamは最初のユーザーに対して活動をログし続けます。例えば、訪問が共有のスマートテレビや公共のキオスクを使用すると、訪問のプロファイルデータが混ざる可能性があります。

