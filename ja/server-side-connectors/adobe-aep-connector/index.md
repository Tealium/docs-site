---
title: Adobe Experience Platformコネクタ構成ガイド
description: この記事では、Adobe Experience Platformコネクタの構成方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/adobe-aep-connector/
---
Adobe Experience Platform Edge Networkは、Adobe Experience CloudまたはAdobe Experience Platform Edgeの各種サービスを利用する顧客に、最適化された連携方法を提供します。

このAPIはライブラリの読み込みに依存しないため、Adobe Experience Platform Edge Networkや、Adobe Analytics、Adobe Audience Manager、Adobe Targetなどの対応ソリューションと非常に高速に連携できます。

## 仕組み

Adobe Experience Platformコネクタは、Adobe Experience Platformの各種サービスと連携するための最適化された方法を提供します。このコネクタは、Adobe Experience Platformを介して、Adobe Analytics、Adobe Audience Manager、Adobe Target、Adobe CDPなどのAdobe Experience Cloudサービスにイベントデータを送信します。

### データ型

Adobe Experience PlatformコネクタはTealiumのすべてのデータ型をサポートしていますが、配列とマップは、データがAdobeに送信される前にコネクタ内で変換されます。

#### オブジェクト配列のマッピング

長さが動的に変化するオブジェクト配列をマッピングするために、コネクタはオブジェクトの属性ごとに配列を受け取ります。その後、コネクタはこれらのプロパティを、適切に構成されたJSONオブジェクト配列に統合します。

たとえば、Adobe Analyticsのリストを送信する場合、このコネクタを使用してデータをオブジェクト配列として送信できます。コネクタは、次のようにリストをマッピングします。

* `_experience.analytics.customDimensions.lists.list1.list.key`から`['productCategories','productCategories','productCategories']`
* `_experience.analytics.customDimensions.lists.list1.list.value`から`['clothing','shoes','accessories']`

コネクタは、これらの配列を次のJSON形式に統合します。

```json
"xdm": {
    "_experience": {
        "analytics": {
            "customDimensions": {
                "lists": {
                    "list1": {
                        "list": [
                            {
                                "key": "productCategories",
                                "value": "clothing"
                            },
                            {
                                "key": "productCategories",
                                "value": "shoes"
                            },
                            {
                                "key": "productCategories",
                                "value": "accessories"
                            }
                        ]
                    }
                }
            }
        }
    }
}
```

空のオプション配列値をコネクタに渡すと、コネクタは対応するオブジェクトの属性に空の値を渡します。たとえば、`experience.analytics.customDimensions.lists.list1.list.key`を`['clothing','','accessories']`にマッピングした場合、リスト配列内の2番目のオブジェクトにはkey属性が含まれません。

スキーマで属性が必須とされているにもかかわらず、その属性が配列に含まれていない場合、そのオブジェクト全体がAdobeに送信される配列から除外されます。

#### マップ属性の送信

コネクタの構成で、ID名前空間を含むマップ属性が必要になる場合があります。このデータをAdobeに送信するには、文字列、数値、および文字列配列の属性を使用します。数値配列にはnull値や空の値を含められないため、数値には文字列または文字列配列を使用することをお勧めします。

たとえば、次の`segmentMembership`値をAdobeに送信する場合を考えます。

```json
"segmentMembership":{
   "Email":{
      "a@example.com":{
        "version": 1,
      },
      "b@example.com":{
        "status": "exited"
      },
      "c@example.com":{
        "version": 3,
        "status": "in"
      },
   }
}
```

コネクタで次の配列をマッピングする必要があります。

* `segmentMembership.Email`: `["a@example.com","b@example.com","c@example.com"]`
* `segmentMembership.Email.version`: `["1", "", "3"]`（2番目のメールアドレスに対応する空の値を含む文字列配列。）
* `segmentMembership.Email.status`: `['', 'exited', 'in']`（1番目のメールアドレスに対応する空の値を含みます。）
* `segmentMembership.Email.validUntil`: `null`

## API情報

このコネクタは、次のベンダーAPIを使用します。

* API名：Adobe Experience Platform API
* APIバージョン：v2.0
* APIエンドポイント：`https://server.adobedc.net/ee/v2/interact`
* ドキュメント：[Adobe Experience Platform API](https://experienceleague.adobe.com/docs/experience-platform/edge-network-server-api/data-collection/interactive-data-collection.html?lang=en)

## 構成

TealiumでAdobe Experience Platformコネクタを構成する前に、Adobe Developer Consoleで認証情報を生成するため、次の手順を完了する必要があります。

1. 新しいAdobe Developer Consoleプロジェクトを作成するか、既存のプロジェクトを使用します。[プロジェクトの概要](https://developer.adobe.com/developer-console/docs/guides/projects/)を参照してください。
1. プロジェクトの認証情報に関連付けるサービスをプロジェクトに追加します。[サービスの概要](https://developer.adobe.com/developer-console/docs/guides/services/)を参照してください。  
このコネクタとの統合には、次のAdobeサービスが必要です。
    * Experience Platform API
    * I/O Events
1. プロジェクトにサービスを追加すると、プロジェクトの認証情報にアクセスできるようになります。[認証情報](https://developer.adobe.com/developer-console/docs/guides/credentials/)を参照してください。プロジェクトの概要に移動し、**Credentials**セクションで**OAuth Server-to-Server**を選択します。  
このコネクタには、次の認証情報が必要です。
    * Client ID（API Key）
    * Client secret
    * Organization ID
1. 認証情報を記録し、Tealiumに戻ってコネクタの構成を完了します。
1. Tealiumでコネクタマーケットプレイスに移動し、新しいコネクタを追加します。詳細については、[about-connectors](https://docs.tealium.com/about-connectors/)を参照してください。
1. コネクタを追加したら、前の手順で生成した認証情報を使用して、次の項目を構成します。
    * **Client ID**  
    （必須）Client ID。
    * **Client Secret**  
    （必須）Client Secret。
    * **Organization ID**  
    （必須）Organization ID。
    * **Sandbox**  
    （任意）API呼び出しでデフォルト環境（prod）とは異なる環境を参照する場合は、このフィールドで指定します。

## アクション

| アクション名 | 訪問プロファイル | イベントデータ |
| --- | :---: | :---: |
| イベントを送信 | ✓ | ✓ |
| イベントを送信（バッチ） | ✓ | ✓ |
| レコードデータをストリーミング | ✓ | ✓ |
| レコードデータをストリーミング（バッチ） | ✓ | ✓ |

### イベントを送信
#### パラメーター

| **パラメーター** | **説明** |
| --- | --- |
| Datastream ID | このアクションで使用する Adobe サーバーサイドの Datastream 構成。 |
| XDM Schema | Datastream を介してデータを送信するために使用する Experience Data Model（XDM）スキーマ。XDM スキーマが、使用する Datastream に関連付けられていることを確認してください。XDM スキーマと Datastream の関連付けについて詳しくは、[Datastream 識別子の生成](https://developer.adobe.com/client-sdks/resources/user-guides/getting-started-with-platform/overview/#generate-a-datastream-identifier)を参照してください。 |
| Identity Namespaces | メールアドレスや数値の CRM ID など、ID が何に関連するかを示します。プロファイルフラグメント間でレコードデータを照合する際、Adobe Experience Platform は ID 値と名前空間を使用してプロファイルデータを統合します。<br>選択した **XDM Schema** に何らかのマップ属性が含まれている場合は、このパラメーターを使用して、マッピングで使用する ID 名前空間を選択します。 |
| XDM Schema Parameters | XDM スキーマに関連付けられたパラメーター。必須属性はロックアイコンの横に表示され、読み取り専用です。左側のドロップダウンリストで有効なマッピングを指定する必要があります。<br>注：`identityMap` 属性では、少なくとも 1 つの名前空間でプロパティ `primary` が `true` に構成されている必要があります。パラメーターに ID 名前空間が含まれていない場合は、ダッシュ（`-`）を入力してください。 |
| XDM Schema Template | XDM スキーマの JSON テンプレートを指定します。テンプレートは XDM スキーマの構造と一致している必要があり、JSON 構造内でテンプレート変数を使用できます。このフィールドに値を指定すると、上記の XDM Schema Parameters は無視されます。<br>詳しくは、[Adobe Developer：Interact エンドポイント](https://developer.adobe.com/data-collection-apis/docs/endpoints/interact/)を参照してください。 |
| Data | 既存の JSON データレイヤーオブジェクトを XDM スキーマにマッピングするには、このフィールドを使用します。データオブジェクトのサブプロパティは、取得するデータレイヤープロパティにマッピングできるように構成できます。この属性は完全にカスタマイズ可能です。 |
| Template Variables | Templates のデータ入力としてテンプレート変数を指定します。ネストされたテンプレート変数にはドット表記で名前を付けます。例：`items.name`。ネストされたテンプレート変数は通常、データレイヤーのリスト属性から作成されます。<br>詳しい情報と使用例については、[connector-template-variables](https://docs.tealium.com/connector-template-variables/)を参照してください。|
| Templates | Data セクションで参照するテンプレートを指定します。サポート対象のフィールドには、名前を二重中括弧で囲んでテンプレートを挿入します。例：`{{SomeTemplateName}}`。<br>詳しい情報と使用例については、[connector-template-variables](https://docs.tealium.com/connector-template-variables/)を参照してください。|
| Referer | イベントの発生元となったページまたはリソースの完全な URL を示します。AEP がインタラクションを正しい参照元コンテキストに関連付けるために使用します。デフォルト値は、利用可能な場合はブラウザーの Referer ヘッダー、それ以外の場合は対応するデータレイヤープロパティです。 |
| X-Forwarded-For | Tealium または別のプロキシを介して接続しているクライアントの送信元 IP アドレスが含まれます。AEP が位置情報の特定とアトリビューションに使用します。デフォルト値は、受信リクエストで提供された IP アドレス、または訪問の IP アドレスを表す Tealium システム変数から取得されます。 |
| X-Forwarded-Proto | クライアントが接続に使用したプロトコル（HTTP または HTTPS）を指定します。プロキシ経由でルーティングされた場合に、AEP が元のリクエストスキームを解釈する際に役立ちます。デフォルト値は `HTTPS` です。 |
| X-Forwarded-Host | `www.clientsite.com` など、クライアントが最初にリクエストしたホストを示します。AEP が正確なホストアトリビューションを維持するために必要です。 |
| User-Agent | クライアントのブラウザー、オペレーティングシステム、レンダリングエンジンを識別する完全なユーザーエージェント文字列を指定します。AEP がデバイスとブラウザーを検出するために使用します。 |
| Sec-CH-UA | （必須）ブラウザーのブランドとバージョンを列挙する、低エントロピーの Client Hint ヘッダー。 |
| Sec-CH-UA-Mobile | （必須）クライアントがモバイルデバイス上にあるかどうかを示します。AEP によるモバイル分類に必要です。 |
| Sec-CH-UA-Platform | ブラウザーが実行されているプラットフォーム（例：`Windows`、`macOS`、`Android`）を示します。 |
| Sec-CH-UA-Platform-Version | オペレーティングシステムプラットフォームのバージョンを指定します。高度なデバイスおよび互換性のアトリビューションに使用します。 |
| Sec-CH-UA-Arch | クライアントデバイスの CPU アーキテクチャ（例：`x86`、`arm`）を指定します。 |
| Sec-CH-UA-Model | デバイスモデルを示します。主にモバイルデバイスで使用されます。 |
| Sec-CH-UA-Bitness | クライアントアーキテクチャのビット数（例：`64`）を示します。 |
| Sec-CH-UA-WoW64 | クライアントが 64 ビット版 Windows システム上で 32 ビットプロセスを実行しているかどうかを示します。 |
| Custom Header Key CSV | リクエストとともに送信するカスタムヘッダーキーを指定します。 |
| Custom Header Value CSV | リクエストとともに送信するカスタムヘッダー値を指定します。この値は、カスタムヘッダーキーの順序に対応します。 |

### イベントの送信（バッチ）

#### バッチ制限

このアクションでは、ベンダーへの大量データ転送をサポートするためにバッチリクエストを使用します。並列処理により、イベントが順不同でベンダーに到達する場合があります。順序が重要な場合は、イベントにシーケンス値を追加してください。詳しくは、[バッチアクション](https://docs.tealium.com/batched-actions/)を参照してください。リクエストは、次のいずれかのしきい値に達するか、プロファイルが公開されるまでキューに保持されます。

* リクエストの最大数：6,000
* 最も古いリクエストからの最大経過時間：15 分
#### パラメータ

| **パラメータ** | **説明** |
| --- | --- |
| データストリーム ID | このアクションで使用する Adobe サーバーサイドのデータストリーム構成。 |
| XDM スキーマ | データストリームを介したデータ送信に使用する Experience Data Model（XDM）スキーマ。XDM スキーマが、使用するデータストリームに関連付けられていることを確認してください。XDM スキーマとデータストリームの関連付けについて詳しくは、[データストリーム識別子の生成](https://developer.adobe.com/client-sdks/resources/user-guides/getting-started-with-platform/overview/#generate-a-datastream-identifier)を参照してください。 |
| ID 名前空間 | メールアドレスや数値形式の CRM ID など、ID が何に関連するかを示します。Adobe Experience Platform は、プロファイルフラグメント間でレコードデータを照合する際に、ID 値と名前空間を使用してプロファイルデータを統合します。<br>選択した **XDM スキーマ**に何らかのマップ型属性が含まれている場合は、このパラメータを使用して、マッピングに使用する ID 名前空間を選択します。<br>パラメータに ID 名前空間が含まれていない場合は、ダッシュ（`-`）を入力します。 |
| XDM スキーマパラメータ | XDM スキーマに関連付けられたパラメータ。必須属性は鍵アイコンの横に表示され、読み取り専用です。左側のドロップダウンリストで有効なマッピングを指定する必要があります。<br>注：`identityMap` 属性では、その名前空間のうち少なくとも 1 つで、プロパティ `primary` が `true` に構成されている必要があります。 |
| XDM スキーマテンプレート | XDM スキーマの JSON テンプレートを指定します。テンプレートは XDM スキーマの構造と一致している必要があり、JSON 構造内でテンプレート変数を使用できます。このフィールドに値を指定すると、上記の XDM スキーマパラメータは無視されます。<br>詳しくは、[Adobe Developer：Interact エンドポイント](https://developer.adobe.com/data-collection-apis/docs/endpoints/interact/)を参照してください。 |
| データ | このフィールドを使用して、既存の JSON データレイヤーオブジェクトを XDM スキーマにマッピングします。データオブジェクトのサブプロパティは、取得するデータレイヤープロパティにマッピングできるように構成できます。この属性は全面的にカスタマイズできます。 |
| テンプレート変数 | テンプレートのデータ入力としてテンプレート変数を指定します。ネストされたテンプレート変数にはドット表記で名前を付けます。例：`items.name`。ネストされたテンプレート変数は通常、データレイヤーのリスト属性から作成されます。<br>詳しい情報と使用例については、[connector-template-variables](https://docs.tealium.com/connector-template-variables/)を参照してください。 |
| テンプレート | 「データ」セクションで参照するテンプレートを指定します。テンプレートは、サポートされているフィールドに二重波括弧を使用して名前で挿入されます。例：`{{SomeTemplateName}}`。<br>詳しい情報と使用例については、[connector-template-variables](https://docs.tealium.com/connector-template-variables/)を参照してください。 |
| リファラー | イベントの発生元となったページまたはリソースの完全な URL を識別します。AEP がインタラクションを正しい参照元コンテキストに関連付けるために使用します。デフォルト値は、利用可能な場合はブラウザーの Referer ヘッダー、または対応するデータレイヤープロパティです。 |
| X-Forwarded-For | Tealium または別のプロキシを介して接続しているクライアントの送信元 IP アドレスが含まれます。AEP が位置情報の特定とアトリビューションに使用します。デフォルト値は、受信リクエストで提供された IP アドレス、または訪問の IP アドレスを表す Tealium システム変数から取得されます。 |
| X-Forwarded-Proto | クライアントが接続に使用したプロトコル（HTTP または HTTPS）を指定します。プロキシを介してルーティングされる場合に、AEP が元のリクエストスキームを解釈するのに役立ちます。デフォルト値は `HTTPS` です。 |
| X-Forwarded-Host | `www.clientsite.com` など、クライアントが最初にリクエストしたホストを識別します。正確なホストアトリビューションを維持するために AEP で必須です。 |
| User-Agent | クライアントのブラウザー、オペレーティングシステム、レンダリングエンジンを識別する完全なユーザーエージェント文字列を提供します。AEP がデバイスとブラウザーの検出に使用します。 |
| Sec-CH-UA | （必須）ブラウザーブランドとバージョンを一覧表示する、低エントロピーの Client Hint ヘッダー。 |
| Sec-CH-UA-Mobile | （必須）クライアントがモバイルデバイスを使用しているかどうかを示します。AEP がモバイルとして分類するために必須です。 |
| Sec-CH-UA-Platform | ブラウザーが実行されているプラットフォーム（例：`Windows`、`macOS`、`Android`）を識別します。 |
| Sec-CH-UA-Platform-Version | オペレーティングシステムプラットフォームのバージョンを提供します。高度なデバイスおよび互換性のアトリビューションに使用されます。 |
| Sec-CH-UA-Arch | クライアントデバイスの CPU アーキテクチャ（例：`x86`、`arm`）を指定します。 |
| Sec-CH-UA-Model | デバイスモデルを識別します。主にモバイルデバイスで使用されます。 |
| Sec-CH-UA-Bitness | クライアントアーキテクチャのビット数（例：`64`）を示します。 |
| Sec-CH-UA-WoW64 | クライアントが 64 ビット Windows システム上で 32 ビットプロセスを実行しているかどうかを示します。 |
| カスタムヘッダーキー CSV | リクエストとともに送信するカスタムヘッダーキーを指定します。 |
| カスタムヘッダー値 CSV | リクエストとともに送信するカスタムヘッダー値を指定します。この値は、カスタムヘッダーキーの順序に対応します。 |

### レコードデータのストリーミング
#### パラメータ

| **パラメータ** | **説明** |
| --- | --- |
| データセット | レコードデータのソースデータセットを選択します。 |
| 接続 | 接続 ID。<br>新しい接続 ID の場合：<ol><li>**作成**をクリックします。</li><li>**接続を作成**画面で接続 ID の名前を入力し、**完了**をクリックします。</li><li>**接続**をクリックして、Adobe AEP エンドポイントへの接続の作成を完了します。</li></ol>既存の接続 ID の場合：<ol><li>**接続**をクリックして、Adobe AEP エンドポイントへの接続を作成します。</li></ol>接続が正常に確立されると、**接続完了**メッセージが表示されます。 |
| ID 名前空間 | メールアドレスや数値形式の CRM ID など、ID が何に関連するかを示します。プロファイルフラグメント間でレコードデータを照合する際、Adobe Experience Platform は ID 値と名前空間を使用してプロファイルデータを統合します。<br>選択した **XDM スキーマ**にマップ属性が含まれている場合は、このパラメータを使用して、マッピングで使用する ID 名前空間を選択します。このパラメータに ID 名前空間が含まれていない場合は、ダッシュ（`-`）を入力します。 |
| 本文パラメータ | XDM スキーマに関連付けられたパラメータ。必須属性はロックアイコンの横に表示され、読み取り専用です。ドロップダウンリストで有効なマッピングを指定します。<br>注：`identityMap` 属性では、少なくとも 1 つの名前空間の `primary` プロパティが `true` に構成されている必要があります。 |
| 作成日時 | 接続が作成された日時を示すタイムスタンプ。 |
| ソース名 | （任意）ソースの名前。この値がない場合、ストリーミングメッセージによって、ストリーミング接続定義のソース ID が自動的に追加されます。 |
| リファラー | イベントの発生元となったページまたはリソースの完全な URL を識別します。AEP がインタラクションを適切な参照元コンテキストに関連付けるために使用します。デフォルト値は、使用可能な場合はブラウザーの Referer ヘッダー、または対応するデータレイヤープロパティです。 |
| X-Forwarded-For | Tealium または別のプロキシを経由して接続するクライアントの送信元 IP アドレスを含みます。AEP が位置情報の特定とアトリビューションに使用します。デフォルト値は、受信リクエストで提供された IP アドレス、または訪問の IP アドレスを表す Tealium システム変数から取得されます。 |
| X-Forwarded-Proto | クライアントが接続に使用したプロトコル（HTTP または HTTPS）を指定します。プロキシ経由でルーティングされたときに、AEP が元のリクエストスキームを解釈するために役立ちます。デフォルト値は `HTTPS` です。 |
| X-Forwarded-Host | `www.clientsite.com` など、クライアントがリクエストした元のホストを識別します。AEP が正確なホストアトリビューションを維持するために必要です。 |
| User-Agent | クライアントのブラウザー、オペレーティングシステム、レンダリングエンジンを識別する完全なユーザーエージェント文字列を提供します。AEP がデバイスとブラウザーを検出するために使用します。 |
| Sec-CH-UA | （必須）ブラウザーのブランドとバージョンを列挙する、低エントロピーの Client Hint ヘッダー。 |
| Sec-CH-UA-Mobile | （必須）クライアントがモバイルデバイスを使用しているかどうかを示します。AEP がモバイルデバイスとして分類するために必要です。 |
| Sec-CH-UA-Platform | ブラウザーが動作しているプラットフォーム（例：`Windows`、`macOS`、`Android`）を識別します。 |
| Sec-CH-UA-Platform-Version | オペレーティングシステムプラットフォームのバージョンを提供します。高度なデバイスおよび互換性のアトリビューションに使用します。 |
| Sec-CH-UA-Arch | クライアントデバイスの CPU アーキテクチャ（例：`x86`、`arm`）を指定します。 |
| Sec-CH-UA-Model | デバイスモデルを識別します。主にモバイルデバイスで使用します。 |
| Sec-CH-UA-Bitness | クライアントアーキテクチャのビット数（例：`64`）を示します。 |
| Sec-CH-UA-WoW64 | クライアントが 64 ビット Windows システム上で 32 ビットプロセスを実行しているかどうかを示します。 |
| カスタムヘッダーキー CSV | リクエストとともに送信するカスタムヘッダーキーを指定します。 |
| カスタムヘッダー値 CSV | リクエストとともに送信するカスタムヘッダー値を指定します。この値は、カスタムヘッダーキーの順序に対応します。 |
| テンプレート変数 | テンプレートのデータ入力として使用するテンプレート変数を指定します。ネストされたテンプレート変数にはドット表記で名前を付けます。例：`items.name`。ネストされたテンプレート変数は通常、データレイヤーのリスト属性から構築されます。<br>詳細および使用例については、[connector-template-variables](https://docs.tealium.com/connector-template-variables/)を参照してください。 |
| テンプレート | 「本文パラメータ」セクションで参照するテンプレートを指定します。テンプレートは、サポートされているフィールドに二重中括弧で囲んだ名前を使用して挿入します。例：`{{SomeTemplateName}}`。<br>詳細および使用例については、[connector-template-variables](https://docs.tealium.com/connector-template-variables/)を参照してください。 |

### レコードデータのストリーミング（バッチ処理）

#### バッチ制限

このアクションは、ベンダーへの大容量データ転送をサポートするために、バッチリクエストを使用します。並列処理により、イベントが順不同でベンダーに到達する場合があります。順序が重要な場合は、イベントにシーケンス値を追加してください。詳細については、[バッチアクション](https://docs.tealium.com/batched-actions/)を参照してください。リクエストは、次のいずれかのしきい値に達するか、プロファイルが公開されるまでキューに保持されます。

* リクエストの最大数：6,000
* 最も古いリクエストからの最大経過時間：60 分
* リクエストの最大サイズ：1 MB
#### パラメータ

| **パラメータ** | **説明** |
| --- | --- |
| データセット | レコードデータの取り込み先となるデータセットを選択します。 |
| 接続 | 接続 ID。<br>新しい接続 ID の場合：<ol><li>**Create** をクリックします。</li><li>**Create Connection** 画面で接続 ID の名前を入力し、**Done** をクリックします。</li><li>**Connect** をクリックして、Adobe AEP エンドポイントへの接続の作成を完了します。</li></ol>既存の接続 ID の場合：<ol><li>**Connect** をクリックして、Adobe AEP エンドポイントへの接続を作成します。</li></ol>接続が正常に確立されると、**Connection Done** メッセージが表示されます。 |
| ID 名前空間 | このパラメータは、ID が関連付けられるコンテキストを示し、メールアドレスや数値の CRM ID など、さまざまな種類の ID 値を区別します。Adobe Experience Platform は、複数のプロファイルフラグメントにわたってレコードデータを照合する際に、ID 値と名前空間を使用してプロファイルデータを統合します。マッピングする名前空間を選択します。<br>このパラメータに ID 名前空間が含まれていない場合は、ダッシュ（`-`）を入力します。 |
| Body パラメータ | XDM スキーマに関連付けられたパラメータ。必須属性は鍵アイコンの横に表示され、読み取り専用です。ドロップダウンリストで有効なマッピングを指定します。<br>注：`identityMap` 属性では、少なくとも 1 つの名前空間の `primary` プロパティを `true` に構成する必要があります。 |
| 作成日時 | 接続の作成日時を示すタイムスタンプ。 |
| ソース名 | （任意）ソースの名前。この値がない場合、ストリーミングメッセージによって、ストリーミング接続の定義にあるソース ID が自動的に追加されます。 |
| Referer | イベントの発生元となったページまたはリソースの完全な URL を識別します。AEP がインタラクションを正しい参照元コンテキストに関連付けるために使用します。デフォルト値は、利用可能な場合はブラウザーの Referer ヘッダー、または対応するデータレイヤープロパティです。 |
| X-Forwarded-For | Tealium または別のプロキシを介して接続するクライアントの送信元 IP アドレスを格納します。AEP が位置情報の特定とアトリビューションに使用します。デフォルト値は、受信リクエストで提供された IP アドレス、または訪問の IP アドレスを表す Tealium システム変数から取得されます。 |
| X-Forwarded-Proto | クライアントが接続に使用したプロトコル（HTTP または HTTPS）を指定します。プロキシ経由でルーティングされた場合に、AEP が元のリクエストスキームを解釈するために役立ちます。デフォルト値は `HTTPS` です。 |
| X-Forwarded-Host | `www.clientsite.com` など、クライアントがリクエストした元のホストを識別します。AEP が正確なホストアトリビューションを維持するために必要です。 |
| User-Agent | クライアントのブラウザー、オペレーティングシステム、レンダリングエンジンを識別する完全なユーザーエージェント文字列を提供します。AEP がデバイスとブラウザーを検出するために使用します。 |
| Sec-CH-UA | （必須）ブラウザーのブランドとバージョンを列挙する、低エントロピーの Client Hint ヘッダー。 |
| Sec-CH-UA-Mobile | （必須）クライアントがモバイルデバイスであるかどうかを示します。AEP がモバイルデバイスを分類するために必要です。 |
| Sec-CH-UA-Platform | ブラウザーが動作しているプラットフォーム（`Windows`、`macOS`、`Android` など）を識別します。 |
| Sec-CH-UA-Platform-Version | オペレーティングシステムプラットフォームのバージョンを提供します。高度なデバイスおよび互換性のアトリビューションに使用します。 |
| Sec-CH-UA-Arch | クライアントデバイスの CPU アーキテクチャ（`x86`、`arm` など）を指定します。 |
| Sec-CH-UA-Model | デバイスモデルを識別します。主にモバイルデバイスで使用されます。 |
| Sec-CH-UA-Bitness | クライアントアーキテクチャのビット数（`64` など）を示します。 |
| Sec-CH-UA-WoW64 | クライアントが 64 ビット Windows システム上で 32 ビットプロセスを実行しているかどうかを示します。 |
| カスタムヘッダーキー CSV | リクエストとともに送信するカスタムヘッダーキーを指定します。 |
| カスタムヘッダー値 CSV | リクエストとともに送信するカスタムヘッダー値を指定します。この値は、カスタムヘッダーキーの順序に対応します。 |
| テンプレート変数 | テンプレートへのデータ入力としてテンプレート変数を指定します。ネストされたテンプレート変数にはドット表記で名前を付けます。例：`items.name`。ネストされたテンプレート変数は通常、データレイヤーのリスト属性から作成されます。<br>詳細および使用例については、[connector-template-variables](https://docs.tealium.com/connector-template-variables/)を参照してください。 |
| テンプレート | Body パラメータセクションで参照するテンプレートを指定します。サポートされているフィールドには、テンプレート名を二重波括弧で囲んで挿入します。例：`{{SomeTemplateName}}`。<br>詳細および使用例については、[connector-template-variables](https://docs.tealium.com/connector-template-variables/)を参照してください。 |

## ユースケース

### Adobe Analytics に分析データを送信する

Adobe Experience Platform コネクタを使用して分析データを Adobe Analytics に送信するには、まず Adobe Experience Platform で XDM スキーマ、データストリーム、サービスを構成する必要があります。Adobe 側の構成が完了したら、Tealium でコネクタを構成できます。

#### XDM スキーマ

Adobe Experience Edge にデータを送信する際は、そのデータが Adobe XDM スキーマに準拠していることを確認する必要があります。Adobe Analytics がイベントを受信すると、イベントはページビューやリンクイベントなど、管理しやすい、より構造化されたデータに変換されます。XDM データと Adobe Analytics の詳細については、[Adobe Experience Platform Edge を使用した Adobe Analytics の実装](https://experienceleague.adobe.com/docs/analytics/implementation/aep-edge/overview.html?lang=en)を参照してください。

ページビューとリンクイベントが適切に処理されるように、Adobe はデータを Adobe Experience Edge ネットワークに送信する前に、そのデータに特定のロジックを適用します。このロジックにより、データが適切にフォーマットされ、必要な変換や集計が適用され、XDM スキーマに準拠していることが保証されます。その後、データは処理および分析のために Adobe Analytics に転送されます。

次の表に、XDM ペイロード内のデータ例と、スキーマに基づく Adobe Analytics でのデータの解釈方法を示します。

| **XDM ペイロードデータ** | **Adobe Analytics での解釈** |
| --- | --- |
| `web.webPageDetails.name`、または<br> `web.webPageDetails.URL` があり、<br>`web.webInteraction.type` がない | ペイロードはページビューと見なされます。 |
| `web.webInteraction.type` と<br>（`web.webInteraction.name` または `web.webInteraction.url`） | ペイロードはリンクイベントと見なされます。 |
| `web.webInteraction.type` と<br>（`web.webPageDetails.name` または `web.webPageDetails.url`） | ペイロードはリンクイベントと見なされます。`web.webPageDetails.name` と `web.webPageDetails.URL` は `null` に構成されます。 |
| `web.webInteraction.type` がなく、<br>（`webPageDetails.name` も `web.webPageDetails.URL` もない） | ペイロードは破棄され、データは無視されます。 |

Adobe Analytics へのデータ送信に使用できる各種変数の完全な一覧については、[Adobe Experience Edge での Analytics 変数のマッピング](https://experienceleague.adobe.com/docs/analytics/implementation/aep-edge/variable-mapping.html?lang=en)を参照してください。

次の例は、変数 `web.webPageDetails.name` のデータと `experience` データが Adobe Analytics への送信時にどのようにフォーマットされるかを示しています。

```json
"xdm": {
  "web": {
    "webPageDetails": {
      "name": "Home Page"
    }
  },
  "_experience": {
    "analytics": {
      "customDimensions": {
        "props": {
          "prop1": "value1"
        },
        "eVars": {
          "eVar1": "value2"
        }
      }
    }
  }
}
```
#### Adobe Experience Platform を構成する

1. Adobe Experience Platform で、**データ管理（Data Management）> スキーマ（Schemas）**に移動し、**スキーマを作成（Create Schema）**をクリックします。
1. **スキーマの詳細（Schema Details）**セクションで、**エクスペリエンスイベント（Experience Event）**オプションを選択し、**次へ（Next）**をクリックします。
1. スキーマの名前を入力し、**完了（Finish）**をクリックします。
1. **データ管理（Data Management）> スキーマ（Schemas）**で、作成したスキーマを選択します。
1. スキーマの詳細画面で、**フィールドグループ（Field groups）**セクションに移動して**追加（Add）**をクリックします。**Adobe Analytics ExperienceEvent Template**を選択し、**保存（Save）**をクリックします。![](https://docs.tealium.com/images/client-side-tags/adobe-experience-platform-schemas.png)
1. **データ収集（Data Collection）> データストリーム（Datastreams）**に移動し、データストリーミングに使用するデータストリームを選択して、画面右側の**編集（Edit）**ボタンをクリックします。データストリームをまだ構成していない場合は、新しく作成できます。
1. データストリームの**構成（Configure）**画面で、作成した**イベントスキーマ（Event Schema）**を選択し、**保存（Save）**をクリックします。![](https://docs.tealium.com/images/client-side-tags/adobe-experience-platform-datastreams.png)
1. **データストリーム（Datastreams）**画面で、**サービスを追加（Add Service）**をクリックし、ドロップダウンリストから**Adobe Analytics**オプションを選択して、**レポートスイートを追加（Add Report Suite）**をクリックします。
1. Adobe Analytics の**レポートスイート ID（Report Suite ID）**を入力し、**保存（Save）**をクリックします。レポートスイート ID は、**Adobe Analytics > 管理者（Admin）> レポートスイート（Report Suites）**に移動すると確認できます。

Adobe Experience Platform のデータストリーム、サービス、およびスキーマの構成について詳しくは、Adobe ドキュメントの次の記事を参照してください。

* [データストリームの構成](https://experienceleague.adobe.com/docs/experience-platform/datastreams/configure.html?lang=en)
* [UI でのスキーマの作成と編集](https://experienceleague.adobe.com/docs/experience-platform/xdm/ui/resources/schemas.html?lang=en)
* [Adobe Analytics の構成](https://experienceleague.adobe.com/docs/experience-platform/datastreams/configure.html?lang=en#analytics)
* [Analytics フィールドのマッピング](https://experienceleague.adobe.com/docs/experience-platform/sources/connectors/adobe-applications/mapping/analytics.html?lang=en)

#### Tealium で Adobe Experience Platform コネクタを構成する

1. [構成の構成](#configure-settings)セクションに記載されている、Adobe Experience Platform コネクタの構成手順を完了します。
1. **アクション（Action）**ステップで、使用するアクションを選択します。
1. 次のパラメータを使用してアクションを構成します。
    * **データストリーム ID（Datastream ID）**：先ほど作成したデータストリーム ID を選択します。
    * **XDM スキーマ（XDM Schema）**：対応するデータストリームの XDM スキーマを選択します。Adobe Experience Platform では、データストリームがすでに単一の XDM スキーマにリンクされている必要があります。このスキーマはドロップダウンリストに表示されます。
    * **ID 名前空間（Identity Namespaces）**：マッピングする名前空間を選択します。Adobe Experience Platform は、プロファイルフラグメント間でレコードデータを照合する際に、ID 値と名前空間を使用してプロファイルデータを結合します。XDM スキーマに `identityMap` などのマップオブジェクトが含まれている場合は、名前空間を選択する必要があります。
    * **XDM スキーマパラメータ（XDM Schema Parameters）**：XDM スキーマパラメータに関連付ける属性を選択します。
        * `_id`：イベントを識別するランダムな一意の ID。この ID にマッピングする特定の属性がまだない場合は、`tealium_random` を使用します。
        * `timestamp`：イベントが発生した時点を表す UTC タイムスタンプ。想定される形式は `YYYY-MM-DDTHH:MM:SSZ` です。
        * マッピングが必要なその他の属性を追加します。Adobe Analytics へのデータ送信に使用できる各種変数の完全なリストについては、[Adobe Experience Edge での Analytics 変数のマッピング](https://experienceleague.adobe.com/docs/analytics/implementation/aep-edge/variable-mapping.html?lang=en)を参照してください。
1. **完了（Finish）**をクリックします。

次の画像は、Tealium でのマッピング例を示しています。

![](https://docs.tealium.com/images/server-side-connectors/adobe-analytics-tealium-setup.png)

### オーディエンスデータを Adobe Audience Manager に送信する

Adobe Experience Platform コネクタを使用してオーディエンスデータを Adobe Audience Manager に送信するには、まず Adobe Experience Platform で XDM スキーマの詳細を構成する必要があります。Adobe 側の構成が完了したら、Tealium でコネクタを構成できます。

Adobe Audience Manager と XDM のフィールドマッピングの完全なリストについては、Adobe ドキュメントの[Audience Manager のフィールドマッピング](https://experienceleague.adobe.com/docs/experience-platform/sources/connectors/adobe-applications/mapping/audience-manager.html?lang=en)を参照してください。

次の例は、Adobe Audience Manager に送信する際に、オーディエンスデータが XDM スキーマへどのようにマッピングされるかを示しています。

```json
  "xdm": {
      "identityMap": {
        "ECID": {
          "_id": "12345"
        },
        "CORE": {
          "_id": "67890"
        }
      },
      "segmentMemberships": {
        "AAMTraits": ["trait1", "trait2"],
        "AAMSegments": ["segment1", "segment2"]
      },
      "profileStitch": [],
      "device": {
        "type": "desktop"
      },
      "placeContext": {
        "geo": {
          "countryCode": "US"
        }
      },
      "environment": {
        "browserDetails": {
          "userAgent": "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/58.0.3029.110 Safari/537.3"
        }
      }
  }
```

#### Adobe Experience Platform を構成する

Adobe Audience Manager は、エクスペリエンスイベントスキーマと個人プロファイルスキーマを使用して、リアルタイムデータとプロファイルデータという 2 種類のデータを受け入れます。次の例は、エクスペリエンスイベントのユースケース向けに Adobe Experience Platform を構成する方法を示しています。個人プロファイルを使用する場合は、次の手順を実行しますが、手順 2 では「個人プロファイル」オプションを選択してください。

1. Adobe Experience Platform で、**データ管理（Data Management）> スキーマ（Schemas）**に移動し、**スキーマを作成（Create Schema）**をクリックします。
1. **スキーマの詳細（Schema Details）**セクションで、リアルタイムデータを構成するための**エクスペリエンスイベント（Experience Event）**オプションを選択し、**次へ（Next）**をクリックします。
1. スキーマの名前を入力し、**完了（Finish）**をクリックします。
1. **データ管理（Data Management）> スキーマ（Schemas）**で、作成したスキーマを選択します。
1. スキーマの詳細画面で、**フィールドグループ（Field groups）**セクションに移動し、**Adobe Audience Manager Template**を選択して、**保存（Save）**をクリックします。![](https://docs.tealium.com/images/server-side-connectors/adobe-audience-manager-schema.png)
1. **データ収集（Data Collection）> データストリーム（Datastreams）**に移動し、データストリーミングに使用するデータストリームを選択して、画面右側の**編集（Edit）**ボタンをクリックします。データストリームをまだ構成していない場合は、新しく作成できます。
1. データストリームの**構成（Configure）**画面で、作成した**イベントスキーマ（Event Schema）**を選択し、**保存（Save）**をクリックします。
1. **データストリーム（Datastreams）**画面で、**サービスを追加（Add Service）**をクリックし、ドロップダウンリストから**Adobe Audience Manager**オプションを選択して、**保存（Save）**をクリックします。

Adobe Experience Platform のデータストリーム、サービス、およびスキーマの構成について詳しくは、Adobe ドキュメントの次の記事を参照してください。

* [データストリームの構成](https://experienceleague.adobe.com/docs/experience-platform/datastreams/configure.html?lang=en)
* [UI でのスキーマの作成と編集](https://experienceleague.adobe.com/docs/experience-platform/xdm/ui/resources/schemas.html?lang=en)
* [Adobe Audience Manager](https://experienceleague.adobe.com/docs/experience-platform/sources/connectors/adobe-applications/audience-manager.html?lang=en)
* [Adobe Audience Manager のフィールドマッピング](https://experienceleague.adobe.com/docs/experience-platform/sources/connectors/adobe-applications/mapping/audience-manager.html?lang=en)
#### Tealium で Adobe Experience Platform コネクタを構成する

Adobe Audience Manager にデータを送信するようコネクタを構成するには、[Tealium で Adobe Experience Platform コネクタを構成する](#configure-the-adobe-experience-platform-connector-in-tealium)セクションの手順を完了します。

Adobe Audience Manager で利用可能なデータマッピングと、それに対応する XDM フィールドの詳細については、Adobe ドキュメントの[Audience Manager のフィールドマッピング](https://experienceleague.adobe.com/docs/experience-platform/sources/connectors/adobe-applications/mapping/audience-manager.html?lang=en)を参照してください。

### Adobe Target にデータを送信する

Adobe Experience Platform コネクタを使用してオーディエンスデータを Adobe Target に送信するには、最初に Adobe Experience Platform で XDM スキーマの詳細を構成する必要があります。Adobe での構成が完了したら、Tealium でコネクタを構成できます。

Adobe Target と XDM のフィールドマッピングの完全な一覧については、Adobe ドキュメントの[Audience Target のフィールドマッピング](https://experienceleague.adobe.com/docs/experience-platform/sources/connectors/adobe-applications/mapping/target.html?lang=en)を参照してください。

次の例は、Adobe Target に送信する際にデータが XDM スキーマへどのようにマッピングされるかを示しています。

```json
"xdm": {
        "channel": {
            "_id": "web"
        },
        "environment": {
            "browserDetails": {
                "userAgent": "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/58.0.3029.110 Safari/537.3"
            }
        },
        "_experience": {
            "target": {
                "clientCode": "adobetarget",
                "mboxName": "mbox1",
                "activities": [
                    {
                        "activityID": "12345"
                    }
                ]
            }
        },
        "device": {
            "type": "desktop"
        },
        "placeContext": {
            "geo": {
                "countryCode": "US"
            }
        },
        "commerce": {
            "order": {
                "priceTotal": 100.0
            }
        },
        "web": {
            "webReferrer": {
                "url": "https://www.example.com"
            }
        }
    }
}
```

#### Adobe Experience Platform を構成する

1. Adobe Experience Platform で、**Data Management > Schemas** に移動し、**Create Schema** をクリックします。
1. **Schema Details** セクションで **Experience Event** オプションを選択し、**Next** をクリックします。
1. スキーマの名前を入力し、**Finish** をクリックします。
1. **Data Management > Schemas** で、作成したスキーマを選択します。
1. スキーマの詳細画面で **Field groups** セクションに移動し、**Add** をクリックします。**Adobe Target ExperienceEvent Template** を選択し、**Save** をクリックします。![](https://docs.tealium.com/images/server-side-connectors/adobe-target-schema.png)
1. **Data Collection > Datastreams** に移動し、データストリーミングに使用するデータストリームを選択して、画面右側の **Edit** ボタンをクリックします。データストリームをまだ構成していない場合は、新しく作成できます。
1. データストリームの **Configure** 画面で、作成した **Event Schema** を選択し、**Save** をクリックします。
1. **Datastreams** 画面で **Add Service** をクリックし、ドロップダウンリストから **Adobe Target** オプションを選択して、**Save** をクリックします。

Adobe Experience Platform のデータストリーム、サービス、およびスキーマの構成について詳しくは、Adobe ドキュメントの次の記事を参照してください。

* [データストリームの構成](https://experienceleague.adobe.com/docs/experience-platform/datastreams/configure.html?lang=en)
* [UI でのスキーマの作成と編集](https://experienceleague.adobe.com/docs/experience-platform/xdm/ui/resources/schemas.html?lang=en)
* [Adobe Target](https://experienceleague.adobe.com/docs/target.html?lang=en)
* [Adobe Target のフィールドマッピング](https://experienceleague.adobe.com/docs/experience-platform/sources/connectors/adobe-applications/mapping/target.html?lang=en)

#### Tealium で Adobe Experience Platform コネクタを構成する

Adobe Target にデータを送信するようコネクタを構成するには、[Tealium で Adobe Experience Platform コネクタを構成する](##configure-the-adobe-experience-platform-connector-in-tealium)セクションの手順を完了します。

次の画像は、Tealium でのマッピング例を示しています。

![](https://docs.tealium.com/images/server-side-connectors/adobe-target-tealium-setup.png)

### Adobe Identity Service にプロファイリングデータを送信する

Adobe Experience Platform コネクタを使用してプロファイリングデータを Adobe Identity Service に送信するには、最初に Adobe Experience Platform で XDM スキーマの詳細を構成する必要があります。Adobe での構成が完了したら、Tealium でコネクタを構成できます。

以下の概念は、Adobe Experience Platform 内で Identity Service の使用を開始する際に役立ちます。

* **ID**：ログイン ID、ECID、ロイヤルティ ID など、通常は個人であるエンティティに固有のデータです。
* **ID 名前空間**：ID のコンテキストまたは種類を区別します。たとえば、ID により、`name@email.com` はメールアドレス、`443522` は数値の CRM ID として区別されます。ID 名前空間は、個々の ID の検索や、ID 値にコンテキストを付与するために使用されます。これにより、異なるプライマリ ID を含んでいても、メール ID 名前空間で同じ値を共有する 2 つのプロファイルフラグメントが同一人物のものであると判断できます。
* **ID グラフ**：異なる ID 間の関係を表すマップです。どの顧客 ID が結合されているか、またそれらがどのように結合されているかを視覚化し、より深く理解できます。このグラフは Identity Service によって自動的に作成され、異なる ID 名前空間をマッピングすることで、顧客がさまざまなチャネルを通じてブランドとどのようにやり取りしているかを視覚的に表します。
* **Experience Cloud ID（ECID）**：Adobe Experience Platform と Adobe Experience Cloud アプリケーション全体で使用される共有 ID 名前空間です。ECID は顧客 ID の基盤となり、デバイスのプライマリ ID および ID グラフのベースノードとして使用されます。
#### 結合ポリシー

Adobe Experience Platform では、複数のソースからデータフラグメントを収集して結合し、個々の顧客の全体像を把握できます。結合ポリシーとは、Adobe Experience Platform がデータの優先順位を構成し、顧客の統合ビューを作成するためにどのデータを結合するかを決定する一連のルールです。

各プロファイルフラグメントには、個人に存在する可能性があるすべての ID のうち、1 つの ID に関する情報のみが含まれます。それらのデータを結合して顧客プロファイルを作成する際に情報が競合する可能性があるため、優先順位を指定する必要があります。

結合方法を選択すると、データセット間で結合の競合が発生した場合に、どのデータセット属性を優先するかを指定できます。結合方法には、「データセットの優先順位」と「タイムスタンプ順」の 2 つがあります。「データセットの優先順位」ではデータセットに基づいてフラグメントが優先され、「タイムスタンプ順」では最新のフラグメントが優先されます。

ID ステッチとは、データフラグメントを識別して結合し、完全なプロファイルレコードを作成するプロセスです。ID ステッチ用にプロファイルを結合する方法には、「なし」と「プライベートグラフ」の 2 つがあります。**なし**を選択すると、1 人の顧客が異なるオーディエンスの条件を満たす複数のプロファイルを持つ可能性があり、その結果、複数のマーケティングメッセージが送信されます。**プライベートグラフ**を選択すると、同一人物に関連する複数の ID が結合され、1 つのプロファイルと 1 つのマーケティングメッセージにまとめられます。

次の例は、Adobe Identity Service に送信される際に、ID データが XDM スキーマにどのようにマッピングされるかを示しています。Adobe Identity Service は、メールアドレスが `myemail@example.com` のプロファイルを検索します。一致するプロファイルが見つかると、メールアドレス `myNEWemail@example.com` と電話番号 `77828292900000` が追加されます。Identity Service で一致するプロファイルが見つからない場合は、両方のメールアドレスと電話番号を含む新しいプロファイルが作成されます。

```json
{
    "_id": "gjsadfghdfkyweiu2ydudyieds3wuyi2kadsjlksddrdesdhslksdwqe",
    "timestamp": "2023-11-17T02:59:57Z",
    "identityMap": {
        "Email": [
          {
            "id": "myemail@example.com",
            "primary": true
          }
        ]
      },
      "personalEmail": {
        "address": "myNEWemail@example.com"
      },
      "mobilePhone": {
        "number": "77828292900000"
      }
    }
}
```

Adobe Experience Platform での Identity Service の構成について詳しくは、Adobe ドキュメントの次の記事を参照してください。

* [Identity Service の概要](https://experienceleague.adobe.com/docs/experience-platform/identity/home.html?lang=en)
* [ID 名前空間の概要](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=en)
* [結合ポリシーの概要](https://experienceleague.adobe.com/docs/experience-platform/profile/merge-policies/overview.html?lang=en)
* [Adobe Data Collection](https://experienceleague.adobe.com/docs/experience-platform/sources/connectors/adobe-applications/data-collection.html?lang=en)

#### Adobe Experience Platform の構成


<blockquote>
Adobe Experience Platform で顧客データを更新するには、複数の Adobe 製品にまたがるデータのステッチが必要になる場合があります。たとえば、Adobe Journey Optimizer で実行されているメールキャンペーン用にプロファイルを作成した後、Interactive Data Collection エンドポイントを介して送信された別のイベントでそのプロファイルを更新できます。
</blockquote>


1. Adobe Experience Platform で、**Data Management > Schemas**に移動し、使用するスキーマを選択するか、**Create Schema**をクリックして新しいスキーマを作成します。
    * 新しいスキーマ
        1. **Schema Details**セクションで、**Experience Event**または**Individual Profile**オプションを選択し、**Next**をクリックします。
        1. スキーマの名前を入力し、**Finish**をクリックします。
    * 既存のスキーマ
        1. スキーマの詳細画面で、**Field groups**セクションに移動し、**Personal Contact Details**を選択して、**Save**をクリックします。
        1. このスキーマを使用するときに更新するプロファイル属性を追加します。たとえば、メールアドレスと電話番号を追加するには、次の手順を実行します。
            * **personalEmail**プロパティを展開して**address**をクリックし、スキーマ画面の右側にある**Field Properties**セクションで**Identity**チェックボックスをオンにします。
            * **mobilePhone**プロパティを展開して**number**をクリックし、スキーマ画面の右側にある**Field Properties**セクションで**Identity**チェックボックスをオンにします。
1. **Save**をクリックします。![](https://docs.tealium.com/images/server-side-connectors/adobe-identity-schema.png)
1. **Data Management > Datasets**に移動し、**Create Dataset**をクリックします。
1. **Create Dataset from Schema**をクリックし、リストからスキーマを選択して、**Next**をクリックします。
1. データセットの名前を入力し、**Finish**をクリックします。
1. **Customer > Profiles**に移動し、**Merge Policies**タブを選択して、**Create merge policy**をクリックします。
1. スキーマ名を入力します。スキーマクラスは**XDM Individual Profile**、ID ステッチは**Private Graph**のままにします。**Save**をクリックします。
1. **Connection > Sources**に移動し、**Adobe Data Collection**を検索して、**Set Up**をクリックします。

詳しくは、[Adobe Data Collection](https://experienceleague.adobe.com/docs/experience-platform/sources/connectors/adobe-applications/data-collection.html?lang=en)を参照してください。

#### Tealium での Adobe Experience Platform コネクタの構成

Identity Service にデータを送信するようにコネクタを構成するには、[Tealium での Adobe Experience Platform コネクタの構成](#configure-the-adobe-experience-platform-connector-in-tealium)セクションの手順を実行します。

Event Experience スキーマを使用している場合は、**Send Event**アクションを作成します。Individual Profile スキーマを使用している場合は、**Stream Record Data**アクションを作成する必要があります。

次の画像は、Tealium でのマッピング例を示しています。

![](https://docs.tealium.com/images/server-side-connectors/adobe-identity-service-tealium-setup.png)

#### Adobe Experience Platform でのプロファイル更新の確認

Adobe Experience Platform で更新されたプロファイルを確認するには、**Customer > Profiles**に移動します。すべてのプロファイル属性を表示するには、**Attributes**タブをクリックします。

## Adobe Experience Platform でのイベント呼び出しのデバッグ

イベント呼び出しをデバッグするには、**Connection > Sources**に移動し、**Dataflows**タブをクリックします。

データストリーム用に自動作成されたデータフローをクリックし、失敗したレコードがあるかどうかを確認します。イベントがまだ処理されていない場合は、データフローが表示されないことがあります。

エラーが見つかった場合は、**Dataflow Run Start**の値をクリックしてエラーの詳細を表示します。
![](https://docs.tealium.com/images/server-side-connectors/adobe-dataflows-tab.png)

この例では、タイムスタンプの形式が正しくないため、イベントが処理されていません。
![](https://docs.tealium.com/images/server-side-connectors/adobe-dataflow-run-error.png)