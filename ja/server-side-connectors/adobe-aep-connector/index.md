---
title: Adobe Experience Platform コネクタ構成ガイド
description: この記事では、Adobe Experience Platform コネクタの構成方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/adobe-aep-connector/
---
Adobe Experience Platform Edge Networkは、Adobe Experience CloudまたはAdobe Experience Platform Edgeサービスとのやり取りを最適化する方法を提供します。

APIはライブラリのロードに依存しないため、Adobe Experience Platform Edge Networkおよびサポートされるソリューション（Adobe Analytics、Adobe Audience Manager、Adobe Targetなど）とのやり取りを非常に高速に行うことができます。

## 動作原理

Adobe Experience Platform コネクタは、Adobe Experience Platform サービスとのやり取りを最適化する方法を提供します。このコネクタはイベントデータをAdobe Experience Platformを通じてAdobe Experience Cloudサービス（Adobe Analytics、Adobe Audience Manager、Adobe Target、Adobe CDPなど）に送信します。

### データタイプ

Adobe Experience Platform コネクタは、Tealiumのすべてのデータタイプをサポートしていますが、配列とマップはコネクタ内で変換され、データがAdobeに送信される前に変換されます。

#### オブジェクトの配列のマッピング

動的な長さのオブジェクトの配列をマッピングするために、コネクタはオブジェクト属性ごとに1つの配列を受け入れます。その後、これらのプロパティを適切に形成されたJSONオブジェクトの配列にマージします。

たとえば、Adobe Analyticsのリストを送信したい場合、このコネクタを使用してデータをオブジェクトの配列として送信できます。コネクタは次のようにリストをマッピングします：

* `_experience.analytics.customDimensions.lists.list1.list.key` を `['productCategories','productCategories','productCategories']` に
* `_experience.analytics.customDimensions.lists.list1.list.value` を `['clothing','shoes','accessories']` に

コネクタはこれらの配列を次のJSON形式にマージします：

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

オプショナルな配列値を空でコネクタに渡すと、コネクタは対応するオブジェクトの属性で空の値を渡します。たとえば、`experience.analytics.customDimensions.lists.list1.list.key` を `['clothing','','accessories']` にマッピングした場合、リスト配列の2番目のオブジェクトには属性キーが存在しません。

スキーマが属性を必要としており、配列に含まれていない場合、そのオブジェクト全体はAdobeに送信される配列に含まれません。

#### マップ属性の送信

コネクタ構成では、ID名前空間を持つマップ属性が必要になる場合があります。このデータをAdobeに送信するには、文字列、数字、および文字列の配列属性を使用します。数値には文字列または文字列の配列を使用することをお勧めします。なぜなら、数字の配列にはnull値や空の値を含めることができないからです。

たとえば、次の `segmentMembership` の値をAdobeに送信したい場合：

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
コネクタで次の配列をマッピングする必要があります：

* `segmentMembership.Email`: `["a@example.com","b@example.com","c@example.com"]`
* `segmentMembership.Email.version`: `["1", "", "3"]` (2番目のメールのために空の値を含む文字列の配列)
* `segmentMembership.Email.status`: `['', 'exited', 'in']` (最初のメールのために空の値を含む)
* `segmentMembership.Email.validUntil`: `null`

## API情報

このコネクタは次のベンダーAPIを使用します：

* API名: Adobe Experience Platform API
* APIバージョン: v2.0
* APIエンドポイント: `https://server.adobedc.net/ee/v2/interact`
* ドキュメント: [Adobe Experience Platform API](https://experienceleague.adobe.com/docs/experience-platform/edge-network-server-api/data-collection/interactive-data-collection.html?lang=en)

## 構成

TealiumでAdobe Experience Platformコネクタを構成する前に、Adobe Developer Consoleで認証情報を生成するために次のステップを完了する必要があります。

1. 新しいAdobe Developer Consoleプロジェクトを作成するか、既存のプロジェクトを使用します。[プロジェクト概要](https://developer.adobe.com/developer-console/docs/guides/projects/)を参照してください。
1. プロジェクト認証情報に関連付けたいサービスをプロジェクトに追加します。[サービス概要](https://developer.adobe.com/developer-console/docs/guides/services/)を参照してください。このコネクタには次のAdobeサービスが必要です：
    * Experience Platform API
    * I/O Events
1. サービスをプロジェクトに追加した後、プロジェクト認証情報にアクセスできます。[認証情報](https://developer.adobe.com/developer-console/docs/guides/credentials/)を参照してください。プロジェクト概要に移動し、**Credentials** セクションで **OAuth Server-to-Server** を選択します。
このコネクタに必要な認証情報は次のとおりです：
    * クライアントID（APIキー）
    * クライアントシークレット
    * 組織ID
1. 認証情報をメモして、コネクタ構成を完了するためにTealiumに戻ります。
1. Tealiumで、Connector Marketplaceに移動し、新しいコネクタを追加します。コネクタの追加方法についての一般的な指示については、[コネクタについて](https://docs.tealium.com/about-connectors/)を参照してください。
1. コネクタを追加した後、前のステップで生成した認証情報を使用して次の構成を構成します：
    * **クライアントID**  
    （必須）クライアントID。
    * **クライアントシークレット**  
    （必須）クライアントシークレット。
    * **組織ID**  
    （必須）組織ID。
    * **Sandbox**  
    （オプション）API呼び出しがデフォルトの環境（prod）以外の環境を参照する場合は、このフィールドに指定します。

## アクション

| アクション名 | AudienceStream | EventStream |
| --- | :---: | :---: |
| イベント送信 | ✓ | ✓ |
| イベント送信（バッチ処理） | ✓ | ✓ |
| レコードデータストリーミング | ✓ | ✓ |
| レコードデータストリーミング（バッチ処理） | ✓ | ✓ |

### イベント送信


#### パラメータ

| **パラメータ** | **説明** |
| --- | --- |
| Datastream ID | このアクションに使用するAdobeサーバーサイドのDatastream構成です。 |
| XDM スキーマ | データストリームを通じてデータを送信するために使用されるエクスペリエンスデータモデル（XDM）スキーマ。使用するデータストリームにXDMスキーマが関連付けられていることを確認してください。XDMスキーマをデータストリームに関連付ける方法の詳細については、[データストリーム識別子の生成](https://developer.adobe.com/client-sdks/resources/user-guides/getting-started-with-platform/overview/#generate-a-datastream-identifier)を参照してください。 |
| Identity Namespaces | メールアドレスや数値CRM IDなど、アイデンティティが関連するものを示します。プロファイルフラグメント間でレコードデータを照合する際、Adobe Experience Platformはアイデンティティ値とネームスペースを使用してプロファイルデータをマージします。<br>選択した**XDMスキーマ**にマップ属性の種類が含まれている場合、マッピングで使用するアイデンティティネームスペースをこのパラメータで選択してください。 |
| XDM スキーマパラメータ | XDMスキーマに関連するパラメータ。必須属性はロックアイコンが隣に表示され、読み取り専用です。左側のドロップダウンリストで有効なマッピングを提供する必要があります。<br>注：`identityMap`属性は、そのネームスペースの少なくとも1つに`primary`が`true`と構成されている必要があります。パラメータにアイデンティティネームスペースが含まれていない場合は、ダッシュ（`-`）を入力してください。 |
| XDM スキーマテンプレート | XDMスキーマのJSONテンプレートを提供してください。テンプレートはXDMスキーマの構造に一致する必要があり、JSON構造内でテンプレート変数を使用できます。このフィールドに値が提供されると、上記のXDMスキーマパラメータは無視されます。<br>詳細については、[Adobe Developer: Interact Endpoint](https://developer.adobe.com/data-collection-apis/docs/endpoints/interact/)を参照してください。 |
| データ | 既存のJSONデータレイヤーオブジェクトをXDMスキーマにマッピングするためにこのフィールドを使用します。データオブジェクトのサブプロパティは、キャプチャしたいデータレイヤープロパティにマッピングする方法で構築できます。この属性は完全にカスタマイズ可能です。 |
| テンプレート変数 | テンプレートにデータ入力としてテンプレート変数を提供します。ドット表記を使用してネストされたテンプレート変数を名前付けします。例えば、`items.name`。ネストされたテンプレート変数は通常、データレイヤーリスト属性から構築されます。<br>詳細および使用例については、[connector-template-variables](https://docs.tealium.com/connector-template-variables/)を参照してください。|
| テンプレート | データセクションで参照されるテンプレートを提供します。テンプレートは名前で識別され、サポートされるフィールドに二重中括弧で挿入されます。例えば、`{{SomeTemplateName}}`。<br>詳細および使用例については、[connector-template-variables](https://docs.tealium.com/connector-template-variables/)を参照してください。|
| Referer | イベントが発生したページまたはリソースの完全なURLを識別します。AEPが正しい参照コンテキストとのインタラクションを関連付けるために使用されます。デフォルト値は、利用可能な場合はブラウザのRefererヘッダー、または対応するデータレイヤープロパティです。 |
| X-Forwarded-For | Tealiumまたは他のプロキシを通じて接続するクライアントの元のIPアドレスを含みます。AEPによる地理位置情報と帰属のために使用されます。デフォルト値は、受信リクエストで提供されたIPアドレスまたは訪問のIPアドレスを表すTealiumシステム変数から取得されます。 |
| X-Forwarded-Proto | クライアントが接続に使用したプロトコル（HTTPまたはHTTPS）を指定します。プロキシを介してルーティングされた場合に元のリクエストスキームをAEPが解釈するのに役立ちます。デフォルト値は`HTTPS`です。 |
| X-Forwarded-Host | クライアントによって要求された元のホストを識別します。例えば、`www.clientsite.com`。AEPによる正確なホスト帰属を維持するために必要です。 |
| User-Agent | クライアントのブラウザ、オペレーティングシステム、およびレンダリングエンジンを識別する完全なユーザーエージェント文字列を提供します。AEPによるデバイスおよびブラウザ検出のために使用されます。 |
| Sec-CH-UA | (必須) ブラウザのブランドとバージョンをリストする低エントロピーのクライアントヒントヘッダー。 |
| Sec-CH-UA-Mobile | (必須) クライアントがモバイルデバイス上にあるかどうかを示します。AEPによるモバイル分類のために必要です。 |
| Sec-CH-UA-Platform | ブラウザが実行されているプラットフォームを識別します（例：`Windows`、`macOS`、`Android`）。 |
| Sec-CH-UA-Platform-Version | オペレーティングシステムプラットフォームのバージョンを提供します。高度なデバイスおよび互換性の帰属のために使用されます。 |
| Sec-CH-UA-Arch | クライアントデバイスのCPUアーキテクチャを指定します（例：`x86`、`arm`）。 |
| Sec-CH-UA-Model | デバイスモデルを識別します。主にモバイルデバイス用です。 |
| Sec-CH-UA-Bitness | クライアントアーキテクチャのビット数を示します（例：`64`）。 |
| Sec-CH-UA-WoW64 | クライアントが64ビットのWindowsシステム上で32ビットプロセスを実行しているかどうかを示します。 |
| Custom Header Key CSV | リクエストと共に送信するカスタムヘッダーキーを提供してください。 |
| Custom Header Value CSV | リクエストと共に送信するカスタムヘッダー値を提供してください。この値はカスタムヘッダーキーのシーケンスに対応します。 |

### イベント送信（バッチ処理）

#### バッチ制限

このアクションは、ベンダーへの大量データ転送をサポートするためにバッチリクエストを使用します。並行処理により、イベントがベンダーに順不同で到達する可能性があります。順序が重要な場合は、イベントにシーケンス値を追加してください。詳細については、[バッチ処理アクション](https://docs.tealium.com/batched-actions/)を参照してください。リクエストは、次のいずれかの閾値が満たされるか、プロファイルが公開されるまでキューに入れられます：

* 最大リクエスト数：6,000
* 最古のリクエストからの最大時間：15分
#### パラメータ

| **パラメータ** | **説明** |
| --- | --- |
| データストリームID | このアクションに使用するAdobeサーバーサイドのデータストリーム構成です。 |
| XDMスキーマ | データストリームを通じてデータを送信するために使用されるエクスペリエンスデータモデル（XDM）スキーマ。使用するデータストリームにXDMスキーマが関連付けられていることを確認してください。XDMスキーマをデータストリームに関連付ける方法の詳細については、[データストリーム識別子の生成](https://developer.adobe.com/client-sdks/resources/user-guides/getting-started-with-platform/overview/#generate-a-datastream-identifier)を参照してください。 |
| アイデンティティ名前空間 | 電子メールアドレスや数値CRM IDなど、アイデンティティが関連するものを示します。プロファイルフラグメント間でレコードデータを照合する際、Adobe Experience Platformはアイデンティティ値と名前空間を使用してプロファイルデータをマージします。<br>選択した**XDMスキーマ**にマップタイプの属性が含まれている場合、マッピングで使用するアイデンティティ名前空間をこのパラメータで選択してください。<br>アイデンティティ名前空間が含まれていない場合は、ダッシュ（`-`）を入力してください。 |
| XDMスキーマパラメータ | XDMスキーマに関連するパラメータ。必須属性はロックアイコンが表示され、読み取り専用です。左側のドロップダウンリストで有効なマッピングを提供する必要があります。<br>注：`identityMap`属性は、その名前空間の少なくとも一つに`primary`が`true`に構成されている必要があります。 |
| XDMスキーマテンプレート | XDMスキーマのJSONテンプレートを提供してください。テンプレートはXDMスキーマの構造に一致している必要があり、JSON構造内でテンプレート変数を使用できます。このフィールドに値が提供された場合、上記のXDMスキーマパラメータは無視されます。<br>詳細については、[Adobe Developer: Interact Endpoint](https://developer.adobe.com/data-collection-apis/docs/endpoints/interact/)を参照してください。 |
| データ | 既存のJSONデータレイヤーオブジェクトをXDMスキーマにマッピングするためにこのフィールドを使用します。データオブジェクトのサブプロパティは、キャプチャしたいデータレイヤープロパティにマッピングする方法で構築できます。この属性は完全にカスタマイズ可能です。 |
| テンプレート変数 | テンプレートにデータ入力としてテンプレート変数を提供します。ドット表記を使用してネストされたテンプレート変数を名前付けします。例えば、`items.name`。ネストされたテンプレート変数は通常、データレイヤーリスト属性から構築されます。<br>詳細および使用例については、[connector-template-variables](https://docs.tealium.com/connector-template-variables/)を参照してください。|
| テンプレート | データセクションで参照されるテンプレートを提供します。テンプレートは名前で識別され、サポートされるフィールドに二重中括弧で注入されます。例えば、`{{SomeTemplateName}}`。<br>詳細および使用例については、[connector-template-variables](https://docs.tealium.com/connector-template-variables/)を参照してください。|
| リファラー | イベントが発生したページまたはリソースの完全なURLを識別します。AEPが正しい参照コンテキストとの関連付けを行うために使用されます。デフォルト値は、利用可能な場合はブラウザのリファラーヘッダー、または対応するデータレイヤープロパティです。 |
| X-Forwarded-For | Tealiumまたは他のプロキシを通じて接続するクライアントの元のIPアドレスを含みます。AEPによる地理位置情報と帰属のために使用されます。デフォルト値は、受信リクエストで提供されたIPアドレスまたは訪問のIPアドレスを表すTealiumシステム変数から取得されます。 |
| X-Forwarded-Proto | クライアントが接続に使用したプロトコル（HTTPまたはHTTPS）を指定します。プロキシを通じてルーティングされた場合に元のリクエストスキームをAEPが解釈するのに役立ちます。デフォルト値は`HTTPS`です。 |
| X-Forwarded-Host | クライアントによって要求された元のホストを識別します。例えば、`www.clientsite.com`。AEPによる正確なホスト帰属の維持に必要です。 |
| ユーザーエージェント | クライアントのブラウザ、オペレーティングシステム、およびレンダリングエンジンを識別する完全なユーザーエージェント文字列を提供します。AEPによるデバイスおよびブラウザ検出に使用されます。 |
| Sec-CH-UA | (必須) ブラウザのブランドとバージョンをリストする低エントロピーのクライアントヒントヘッダーです。 |
| Sec-CH-UA-Mobile | (必須) クライアントがモバイルデバイス上にあるかどうかを示します。AEPによるモバイル分類のために必要です。 |
| Sec-CH-UA-Platform | ブラウザが実行されているプラットフォームを識別します（例：`Windows`、`macOS`、`Android`）。 |
| Sec-CH-UA-Platform-Version | オペレーティングシステムプラットフォームのバージョンを提供します。高度なデバイスおよび互換性の帰属に使用されます。 |
| Sec-CH-UA-Arch | クライアントデバイスのCPUアーキテクチャを指定します（例：`x86`、`arm`）。 |
| Sec-CH-UA-Model | デバイスモデルを識別します。主にモバイルデバイス用です。 |
| Sec-CH-UA-Bitness | クライアントアーキテクチャのビット数を示します（例：`64`）。 |
| Sec-CH-UA-WoW64 | クライアントが64ビットのWindowsシステム上で32ビットプロセスを実行しているかどうかを示します。 |
| カスタムヘッダーキーCSV | リクエストと共に送信するカスタムヘッダーキーを提供してください。 |
| カスタムヘッダー値CSV | リクエストと共に送信するカスタムヘッダー値を提供してください。この値はカスタムヘッダーキーのシーケンスに対応します。 |

### ストリームレコードデータ

#### パラメータ

| **パラメータ** | **説明** |
| --- | --- |
| データセット | レコードデータのソースデータセットを選択します。 |
| 接続 | 接続IDです。<br>新しい接続IDの場合：<ol><li>**作成**をクリックします。</li><li>**接続作成**画面で、接続IDの名前を入力し、**完了**をクリックします。</li><li>Adobe AEPエンドポイントへの接続を完了するために**接続**をクリックします。</li></ol>既存の接続IDの場合：<ol><li>Adobe AEPエンドポイントへの接続を作成するために**接続**をクリックします。</li></ol>接続が正常に確立されると、**接続完了**メッセージが表示されます。 |
| IDネームスペース | IDが関連するものを示します。例えば、メールアドレスや数値CRM IDなどです。プロファイルフラグメント間でレコードデータをマッチングする際、Adobe Experience PlatformはID値とネームスペースを使用してプロファイルデータをマージします。<br>選択した**XDMスキーマ**にマップ属性が含まれている場合、マッピングで使用するIDネームスペースをこのパラメータで選択します。パラメータにIDネームスペースが含まれていない場合は、ダッシュ（`-`）を入力します。 |
| ボディパラメータ | XDMスキーマに関連するパラメータです。必須属性はロックアイコンが隣に表示され、読み取り専用です。ドロップダウンリストで有効なマッピングを提供してください。<br>注：`identityMap`属性は、そのネームスペースの少なくとも一つに`primary`が`true`に構成されている必要があります。 |
| 作成日時 | 接続の作成時刻を記録するタイムスタンプです。 |
| ソース名 | （オプション）ソースの名前です。この値が欠けている場合、ストリーミングメッセージは自動的にストリーミング接続定義からソースIDを追加します。 |
| リファラー | イベントが発生したページまたはリソースの完全なURLを識別します。AEPは、正しい参照コンテキストとのインタラクションを関連付けるために使用します。デフォルト値は、利用可能な場合はブラウザのリファラーヘッダー、または対応するデータレイヤープロパティです。 |
| X-Forwarded-For | Tealiumまたは他のプロキシを通じて接続するクライアントの元のIPアドレスを含みます。AEPは、地理位置情報と帰属を目的として使用します。デフォルト値は、受信リクエストで提供されたIPアドレスまたは訪問のIPアドレスを表すTealiumシステム変数から取得されます。 |
| X-Forwarded-Proto | クライアントが接続に使用したプロトコル（HTTPまたはHTTPS）を指定します。プロキシを通じてルーティングされた場合に元のリクエストスキームをAEPが解釈するのに役立ちます。デフォルト値は`HTTPS`です。 |
| X-Forwarded-Host | クライアントによって要求された元のホストを識別します。例えば`www.clientsite.com`です。AEPが正確なホスト帰属を維持するために必要です。 |
| User-Agent | クライアントのブラウザ、オペレーティングシステム、レンダリングエンジンを識別する完全なユーザーエージェント文字列を提供します。AEPは、デバイスおよびブラウザの検出に使用します。 |
| Sec-CH-UA | （必須）ブラウザのブランドとバージョンをリストする低エントロピーのクライアントヒントヘッダーです。 |
| Sec-CH-UA-Mobile | （必須）クライアントがモバイルデバイス上にあるかどうかを示します。AEPによるモバイル分類に必要です。 |
| Sec-CH-UA-Platform | ブラウザが実行されているプラットフォームを識別します（例：`Windows`, `macOS`, `Android`）。 |
| Sec-CH-UA-Platform-Version | オペレーティングシステムプラットフォームのバージョンを提供します。高度なデバイスおよび互換性の帰属に使用されます。 |
| Sec-CH-UA-Arch | クライアントデバイスのCPUアーキテクチャを指定します（例：`x86`, `arm`）。 |
| Sec-CH-UA-Model | デバイスモデルを識別します。主にモバイルデバイスに使用されます。 |
| Sec-CH-UA-Bitness | クライアントアーキテクチャのビット数を示します（例：`64`）。 |
| Sec-CH-UA-WoW64 | クライアントが64ビットのWindowsシステム上で32ビットプロセスを実行しているかどうかを示します。 |
| カスタムヘッダーキーCSV | リクエストと共に送信するカスタムヘッダーキーを提供します。 |
| カスタムヘッダーバリューCSV | リクエストと共に送信するカスタムヘッダー値を提供します。この値はカスタムヘッダーキーのシーケンスに対応します。 |
| テンプレート変数 | テンプレートのデータ入力としてテンプレート変数を提供します。ドット表記でネストされたテンプレート変数を名前付けします。例えば、`items.name`です。ネストされたテンプレート変数は通常、データレイヤーリスト属性から構築されます。<br>詳細および使用例については、[connector-template-variables](https://docs.tealium.com/connector-template-variables/)を参照してください。|
| テンプレート | ボディパラメータセクションで参照されるテンプレートを提供します。テンプレートは、サポートされるフィールドに名前で二重中括弧で注入されます。例えば、`{{SomeTemplateName}}`です。<br>詳細および使用例については、[connector-template-variables](https://docs.tealium.com/connector-template-variables/)を参照してください。|

### ストリームレコードデータ（バッチ処理）

#### バッチ制限

このアクションは、ベンダーへの大量データ転送をサポートするためにバッチリクエストを使用します。並列処理により、イベントがベンダーに順不同で到達する可能性があります。順序が重要な場合は、イベントにシーケンス値を追加してください。詳細については、[バッチ処理アクション](https://docs.tealium.com/batched-actions/)を参照してください。次のいずれかの閾値に達するか、プロファイルが公開されるまでリクエストはキューに入れられます：

* 最大リクエスト数：6,000
* 最古のリクエストからの最大時間：60分
* リクエストの最大サイズ：1 MB
#### パラメータ

| **パラメータ** | **説明** |
| --- | --- |
| データセット | レコードデータを取り込むデータセットを選択します。 |
| 接続 | 接続IDです。<br>新しい接続IDの場合：<ol><li>**作成**をクリックします。</li><li>**接続作成**画面で、接続IDの名前を入力し、**完了**をクリックします。</li><li>Adobe AEPエンドポイントへの接続を完了するために**接続**をクリックします。</li></ol>既存の接続IDの場合：<ol><li>Adobe AEPエンドポイントへの接続を作成するために**接続**をクリックします。</li></ol>接続が正常に確立されると、**接続完了**メッセージが表示されます。 |
| アイデンティティ名前空間 | このパラメータは、アイデンティティが関連するコンテキストを示し、電子メールアドレスや数値CRM IDなど、異なるタイプのアイデンティティ値を区別します。プロファイルデータをマージする際、Adobe Experience Platformはアイデンティティ値と名前空間を使用します。マッピングしたい名前空間を選択します。<br>アイデンティティ名前空間が含まれていない場合は、ダッシュ（`-`）を入力します。 |
| ボディパラメータ | XDMスキーマに関連するパラメータです。必須属性はロックアイコンが表示され、読み取り専用です。ドロップダウンリストで有効なマッピングを提供します。<br>注：`identityMap`属性は、その名前空間の少なくとも1つに`primary`が`true`に構成されている必要があります。 |
| 作成日時 | 接続の作成時刻を示すタイムスタンプです。 |
| ソース名 | （オプション）ソースの名前です。この値が欠けている場合、ストリーミングメッセージは自動的にストリーミング接続定義からソースIDを追加します。 |
| リファラー | イベントが発生したページまたはリソースの完全なURLを識別します。AEPが正しい参照コンテキストとのインタラクションを関連付けるために使用されます。デフォルト値は、利用可能な場合はブラウザのリファラーヘッダー、または対応するデータレイヤープロパティです。 |
| X-Forwarded-For | Tealiumまたは他のプロキシを介して接続するクライアントの元のIPアドレスを含みます。AEPによる地理位置情報と帰属のために使用されます。デフォルト値は、受信リクエストで提供されたIPアドレスまたは訪問のIPアドレスを表すTealiumシステム変数から取得されます。 |
| X-Forwarded-Proto | クライアントが接続に使用したプロトコル（HTTPまたはHTTPS）を指定します。プロキシを介してルーティングされた場合に元のリクエストスキームをAEPが解釈するのに役立ちます。デフォルト値は`HTTPS`です。 |
| X-Forwarded-Host | クライアントによって要求された元のホストを識別します。例えば、`www.clientsite.com`です。AEPによる正確なホスト帰属を維持するために必要です。 |
| User-Agent | クライアントのブラウザ、オペレーティングシステム、およびレンダリングエンジンを識別する完全なユーザーエージェント文字列を提供します。AEPによるデバイスおよびブラウザ検出のために使用されます。 |
| Sec-CH-UA | （必須）ブラウザのブランドとバージョンをリストする低エントロピーのクライアントヒントヘッダーです。 |
| Sec-CH-UA-Mobile | （必須）クライアントがモバイルデバイス上にあるかどうかを示します。AEPによるモバイル分類のために必要です。 |
| Sec-CH-UA-Platform | ブラウザが実行されているプラットフォームを識別します（例：`Windows`、`macOS`、`Android`）。 |
| Sec-CH-UA-Platform-Version | オペレーティングシステムプラットフォームのバージョンを提供します。高度なデバイスおよび互換性の帰属のために使用されます。 |
| Sec-CH-UA-Arch | クライアントデバイスのCPUアーキテクチャを指定します（例：`x86`、`arm`）。 |
| Sec-CH-UA-Model | デバイスモデルを識別します。主にモバイルデバイス用です。 |
| Sec-CH-UA-Bitness | クライアントアーキテクチャのビット数を示します（例：`64`）。 |
| Sec-CH-UA-WoW64 | クライアントが64ビットのWindowsシステム上で32ビットプロセスを実行しているかどうかを示します。 |
| カスタムヘッダーキーCSV | リクエストと共に送信するカスタムヘッダーキーを提供します。 |
| カスタムヘッダー値CSV | リクエストと共に送信するカスタムヘッダー値を提供します。この値はカスタムヘッダーキーのシーケンスに関連します。 |
| テンプレート変数 | テンプレートのデータ入力としてテンプレート変数を提供します。ドット表記を使用してネストされたテンプレート変数に名前を付けます。例えば、`items.name`です。ネストされたテンプレート変数は通常、データレイヤーリスト属性から構築されます。<br>詳細および使用例については、[connector-template-variables](https://docs.tealium.com/connector-template-variables/)を参照してください。|
| テンプレート | ボディパラメータセクションで参照されるテンプレートを提供します。テンプレートは、サポートされるフィールドに名前で二重中括弧で挿入されます。例えば、`{{SomeTemplateName}}`です。<br>詳細および使用例については、[connector-template-variables](https://docs.tealium.com/connector-template-variables/)を参照してください。|

## 使用例

### Adobe Analyticsにアナリティクスデータを送信

Adobe Experience Platformコネクタを使用してAdobe Analyticsにアナリティクスデータを送信するには、まずAdobe Experience PlatformでXDMスキーマ、データストリーム、およびサービスを構成する必要があります。Adobeの構成を完了した後、Tealiumでコネクタを構成できます。

#### XDMスキーマ

Adobe Experience Edgeにデータを送信する際は、Adobe XDMスキーマに準拠していることを確認する必要があります。Adobe Analyticsがイベントを受信すると、ページビューやリンクイベントなど、より構造化されたデータに変換され、簡単に管理できるようになります。XDMデータとAdobe Analyticsについての詳細は、[Implement Adobe Analytics with Adobe Experience Platform Edge](https://experienceleague.adobe.com/docs/analytics/implementation/aep-edge/overview.html?lang=en)を参照してください。

ページビューやリンクイベントが適切に処理されるように、AdobeはデータがAdobe Experience Edgeネットワークに送信される前に特定のロジックを適用します。このロジックは、データが適切にフォーマットされ、必要な変換や集約が適用され、XDMスキーマに準拠していることを保証します。その後、データは処理および分析のためにAdobe Analyticsに転送されます。

以下の表は、XDMペイロードのデータ例と、スキーマに基づいてAdobe Analyticsがデータをどのように解釈するかを示しています：

| **XDMペイロードデータ** | **Adobe Analyticsの解釈** |
| --- | --- |
| `web.webPageDetails.name` または<br> `web.webPageDetails.URL` および<br> `web.webInteraction.type` がない場合 | ペイロードはページビューとみなされます。|
|`web.webInteraction.type` および<br> (`web.webInteraction.name` または `web.webInteraction.url`) | ペイロードはリンクイベントとみなされます。|
|`web.webInteraction.type` および<br> (`web.webPageDetails.name` または `web.webPageDetails.url`)| ペイロードはリンクイベントとみなされます。`web.webPageDetails.name` および `web.webPageDetails.URL` は `null` に構成されます。|
|`web.webInteraction.type` がなく、<br> (`webPageDetails.name` および `web.webPageDetails.URL` がない場合) | ペイロードは破棄され、データは無視されます。|

Adobe Analyticsにデータを送信するために使用できるさまざまな変数の完全なリストについては、[Analytics variable mapping in Adobe Experience Edge](https://experienceleague.adobe.com/docs/analytics/implementation/aep-edge/variable-mapping.html?lang=en)を参照してください。

以下の例は、変数 `web.webPageDetails.name` および `experience` データがAdobe Analyticsに送信される際のフォーマットを示しています：

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
#### Adobe Experience Platformの構成

1. Adobe Experience Platformで、**データ管理 > スキーマ**に移動し、**スキーマの作成**をクリックします。
1. **スキーマの詳細**セクションで、**エクスペリエンスイベント**オプションを選択し、**次へ**をクリックします。
1. スキーマの名前を入力し、**完了**をクリックします。
1. **データ管理 > スキーマ**で、作成したばかりのスキーマを選択します。
1. スキーマの詳細画面で、**フィールドグループ**セクションに移動し、**追加**をクリックします。**Adobe Analytics ExperienceEventテンプレート**を選択し、**保存**をクリックします。![](https://docs.tealium.com/images/client-side-tags/adobe-experience-platform-schemas.png)
1. **データ収集 > データストリーム**に移動し、データストリーミングに使用するデータストリームを選択し、画面右側の**編集**ボタンをクリックします。まだデータストリームが構成されていない場合は、新しいものを作成できます。
1. データストリームの**構成**画面で、作成したばかりの**イベントスキーマ**を選択し、**保存**をクリックします。![](https://docs.tealium.com/images/client-side-tags/adobe-experience-platform-datastreams.png)
1. **データストリーム**画面で、**サービスの追加**をクリックし、ドロップダウンリストから**Adobe Analytics**オプションを選択し、**レポートスイートの追加**をクリックします。
1. Adobe Analyticsから**レポートスイートID**を入力し、**保存**をクリックします。レポートスイートIDは、**Adobe Analytics > 管理 > レポートスイート**に移動することで見つけることができます。

Adobe Experience Platform Datastream、サービス、およびスキーマの構成に関する詳細は、Adobeのドキュメントの以下の記事を参照してください：

* [データストリームの構成](https://experienceleague.adobe.com/docs/experience-platform/datastreams/configure.html?lang=en)
* [UIでスキーマを作成および編集する](https://experienceleague.adobe.com/docs/experience-platform/xdm/ui/resources/schemas.html?lang=en)
* [Adobe Analyticsの構成](https://experienceleague.adobe.com/docs/experience-platform/datastreams/configure.html?lang=en#analytics)
* [Analyticsフィールドマッピング](https://experienceleague.adobe.com/docs/experience-platform/sources/connectors/adobe-applications/mapping/analytics.html?lang=en)

#### TealiumでAdobe Experience Platformコネクタを構成する

1. [構成の構成](#configure-settings)セクションのAdobe Experience Platformコネクタの構成手順を完了します。
1. **アクション**ステップで、使用するアクションを選択します。
1. 次のパラメーターでアクションを構成します：
    * **Datastream ID**: 以前に作成したデータストリームIDを選択します。
    * **XDMスキーマ**: 対応するデータストリームのXDMスキーマを選択します。Adobe Experience Platformでは、データストリームはすでに単一のXDMスキーマにリンクされている必要があります。このスキーマはドロップダウンリストで確認できるはずです。
    * **Identity Namespaces**: マップする名前空間を選択します。プロファイルフラグメント間でレコードデータを照合する際、Adobe Experience Platformはアイデンティティ値と名前空間を使用してプロファイルデータをマージします。XDMスキーマに`identityMap`のようなマップオブジェクトが含まれている場合、名前空間を選択する必要があります。
    * **XDMスキーマパラメーター**: XDMスキーマパラメーターに関連付ける属性を選択します。
        * `_id`: イベントを識別するランダムな一意のIDです。このIDにマップする特定の属性がない場合は、`tealium_random`を使用します。
        * `timestamp`: イベントが発生した瞬間を表すUTCタイムスタンプです。予想される形式は`YYYY-MM-DDTHH:MM:SSZ`です。
        * マップする必要がある追加の属性を追加します。Adobe Analyticsにデータを送信するために使用できるさまざまな変数の完全なリストについては、[Adobe Experience EdgeでのAnalytics変数マッピング](https://experienceleague.adobe.com/docs/analytics/implementation/aep-edge/variable-mapping.html?lang=en)を参照してください。
1. **完了**をクリックします。

次の画像はTealiumでの例示的なマッピングを示しています：

![](https://docs.tealium.com/images/server-side-connectors/adobe-analytics-tealium-setup.png)

### Adobe Audience Managerにオーディエンスデータを送信する

Adobe Experience Platformコネクタを使用してAdobe Audience Managerにオーディエンスデータを送信するには、まずAdobe Experience PlatformでXDMスキーマの詳細を構成する必要があります。Adobeの構成を完了した後、Tealiumでコネクタを構成できます。

Adobe Audience ManagerおよびXDMフィールドマッピングの完全なリストについては、Adobeのドキュメントの[Audience Managerフィールドマッピング](https://experienceleague.adobe.com/docs/experience-platform/sources/connectors/adobe-applications/mapping/audience-manager.html?lang=en)を参照してください。

次の例は、Adobe Audience Managerに送信された際にオーディエンスデータがXDMスキーマにどのようにマッピングされるかを示しています。

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
#### Adobe Experience Platformの構成

Adobe Audience Managerは、Experience EventおよびIndividual Profileスキーマを使用してリアルタイムデータとプロファイルデータの両方を受け入れます。リアルタイムデータセットアップの場合はExperience Eventオプションを選択し、次の手順を完了します。Individual Profileを使用する場合は、ステップ2でIndividual Profileオプションを選択してください。

1. Adobe Experience Platformで、**データ管理 > スキーマ**に移動し、**スキーマの作成**をクリックします。
1. **スキーマの詳細**セクションで、**エクスペリエンスイベント**オプションを選択し、**次へ**をクリックします。
1. スキーマの名前を入力し、**完了**をクリックします。
1. **データ管理 > スキーマ**で、作成したばかりのスキーマを選択します。
1. スキーマの詳細画面で、**フィールドグループ**セクションに移動し、**Adobe Audience Managerテンプレート**を選択し、**保存**をクリックします。![](https://docs.tealium.com/images/server-side-connectors/adobe-audience-manager-schema.png)
1. **データ収集 > データストリーム**に移動し、データストリーミングに使用するデータストリームを選択し、画面右側の**編集**ボタンをクリックします。まだデータストリームが構成されていない場合は、新しいものを作成できます。
1. データストリームの**構成**画面で、作成したばかりの**イベントスキーマ**を選択し、**保存**をクリックします。
1. **データストリーム**画面で、**サービスの追加**をクリックし、ドロップダウンリストから**Adobe Audience Manager**オプションを選択し、**保存**をクリックします。

Adobe Experience Platform Datastream、サービス、およびスキーマの構成に関する詳細は、Adobeのドキュメントの以下の記事を参照してください：

* [データストリームの構成](https://experienceleague.adobe.com/docs/experience-platform/datastreams/configure.html?lang=en)
* [UIでスキーマを作成および編集する](https://experienceleague.adobe.com/docs/experience-platform/xdm/ui/resources/schemas.html?lang=en)
* [Adobe Audience Manager](https://experienceleague.adobe.com/docs/experience-platform/sources/connectors/adobe-applications/audience-manager.html?lang=en)
* [Adobe Audience Managerフィールドマッピング](https://experienceleague.adobe.com/docs/experience-platform/sources/connectors/adobe-applications/mapping/audience-manager.html?lang=en)
#### TealiumでAdobe Experience Platformコネクタを構成する

Adobe Audience Managerにデータを送信するには、[TealiumでAdobe Experience Platformコネクタを構成する](#configure-the-adobe-experience-platform-connector-in-tealium)セクションの手順を完了してください。

Adobe Audience Managerで利用可能なデータマッピングとそれに対応するXDMフィールドについての詳細は、Adobeのドキュメントにある[Audience Managerフィールドマッピング](https://experienceleague.adobe.com/docs/experience-platform/sources/connectors/adobe-applications/mapping/audience-manager.html?lang=en)を参照してください。

### Adobe Targetにデータを送信する

Adobe Experience Platformコネクタを使用してAdobe Targetにオーディエンスデータを送信するには、まずAdobe Experience PlatformでXDMスキーマの詳細を構成する必要があります。Adobeの構成を完了した後、Tealiumでコネクタを構成できます。

Adobe TargetとXDMフィールドマッピングの完全なリストについては、Adobeのドキュメントにある[Audience Targetフィールドマッピング](https://experienceleague.adobe.com/docs/experience-platform/sources/connectors/adobe-applications/mapping/target.html?lang=en)を参照してください。

次の例は、Adobe Targetに送信されたデータがXDMスキーマにどのようにマッピングされるかを示しています。

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
```
#### Adobe Experience Platformを構成する

1. Adobe Experience Platformで**Data Management > Schemas**に移動し、**Create Schema**をクリックします。
1. **Schema Details**セクションで**Experience Event**オプションを選択し、**Next**をクリックします。
1. スキーマの名前を入力し、**Finish**をクリックします。
1. **Data Management > Schemas**で作成したばかりのスキーマを選択します。
1. スキーマの詳細画面で**Field groups**セクションに移動し、**Add**をクリックします。**Adobe Target ExperienceEvent Template**を選択し、**Save**をクリックします。![](https://docs.tealium.com/images/server-side-connectors/adobe-target-schema.png)
1. **Data Collection > Datastreams**に移動し、データストリーミングに使用するデータストリームを選択し、画面右側の**Edit**ボタンをクリックします。まだデータストリームが構成されていない場合は、新しいものを作成できます。
1. データストリームの**Configure**画面で、作成したばかりの**Event Schema**を選択し、**Save**をクリックします。
1. **Datastreams**画面で**Add Service**をクリックし、ドロップダウンリストから**Adobe Target**オプションを選択し、**Save**をクリックします。

Adobe Experience Platformのデータストリーム、サービス、スキーマの構成についての詳細は、Adobeのドキュメントの次の記事を参照してください：

* [データストリームを構成する](https://experienceleague.adobe.com/docs/experience-platform/datastreams/configure.html?lang=en)
* [UIでスキーマを作成および編集する](https://experienceleague.adobe.com/docs/experience-platform/xdm/ui/resources/schemas.html?lang=en)
* [Adobe Target](https://experienceleague.adobe.com/docs/target.html?lang=en)
* [Adobe Targetフィールドマッピング](https://experienceleague.adobe.com/docs/experience-platform/sources/connectors/adobe-applications/mapping/target.html?lang=en)

#### TealiumでAdobe Experience Platformコネクタを構成する

Adobe Targetにデータを送信するためにコネクタを構成するには、[TealiumでAdobe Experience Platformコネクタを構成する](##configure-the-adobe-experience-platform-connector-in-tealium)セクションの手順を完了してください。

次の画像はTealiumでの例示的なマッピングを示しています：

![](https://docs.tealium.com/images/server-side-connectors/adobe-target-tealium-setup.png)


### Adobe Identity Serviceにプロファイリングデータを送信する

Adobe Experience Platformコネクタを使用してAdobe Identity Serviceにプロファイリングデータを送信するには、まずAdobe Experience PlatformでXDMスキーマの詳細を構成する必要があります。Adobeの構成を完了した後、Tealiumでコネクタを構成できます。

Identity Serviceを使用するための次の概念が役立ちます：

* **Identity**: 個体、通常は個人に固有のデータで、ログインID、ECID、またはロイヤルティIDなどがあります。
* **Identity namespaces**: アイデンティティのコンテキストまたはタイプを区別します。たとえば、アイデンティティは`name@email.com`をメールアドレスとして区別したり、`443522`を数値のCRM IDとして区別します。Identity namespacesは個々のアイデンティティを検索し、アイデンティティ値のコンテキストを提供するために使用されます。これにより、異なる主要IDを持つが、同じメールアイデンティティ名前空間の値を共有する2つのプロファイルフラグメントが同じ個人であると判断できます。
* **Identity Graph**: 異なるアイデンティティ間の関係のマップで、顧客のアイデンティティがどのように繋がっているか、そしてどのように理解できるかを視覚化し、よりよく理解することができます。グラフはIdentity Serviceによって自動的に作成され、異なるアイデンティティ名前空間をマッピングし、異なるチャンネルを通じてブランドとの顧客のやり取りを視覚的に表現します。
* **Experience Cloud ID (ECID)**: Adobe Experience PlatformおよびAdobe Experience Cloudアプリケーション全体で使用される共有アイデンティティ名前空間です。ECIDは顧客アイデンティティの基盤として使用され、デバイスの主要IDおよびアイデンティティグラフの基本ノードとして使用されます。
#### マージポリシー

Adobe Experience Platformでは、複数のソースからデータフラグメントを集めて統合し、個々の顧客の完全なビューを作成することができます。マージポリシーは、Adobe Experience Platformがデータを優先する方法と、顧客の統一されたビューを作成するためにどのデータを組み合わせるかを決定するルールのセットです。

各プロファイルフラグメントには、個人に存在可能なアイデンティティの総数のうちの1つのアイデンティティに関する情報のみが含まれています。そのデータをマージして顧客プロファイルを形成する際には、情報が競合する可能性があり、優先順位を指定する必要があります。

マージ方法を選択することで、データセット間でマージ競合が発生した場合に優先するデータセット属性を指定できます。マージ方法には「データセット優先」と「タイムスタンプ順」の2つがあります。データセット優先はデータセットに基づいてフラグメントを優先し、タイムスタンプ順は最新のフラグメントを優先します。

アイデンティティスティッチングは、データフラグメントを識別し、それらを組み合わせて完全なプロファイルレコードを形成するプロセスです。アイデンティティスティッチングのためのプロファイルをマージする方法には、「なし」と「プライベートグラフ」の2つがあります。**なし**を選択すると、1人の顧客が複数のプロファイルを持つことがあり、異なるオーディエンスに適格であるため、複数のマーケティングメッセージが発生します。**プライベートグラフ**を選択すると、同一個人に関連する複数のアイデンティティが繋がり、1つのプロファイルと1つのマーケティングメッセージが生成されます。

次の例は、アイデンティティデータがAdobe Identity Serviceに送信されたときにXDMスキーマにどのようにマッピングされるかを示しています。Adobe Identity Serviceは、`myemail@example.com`のメールアドレスを持つプロファイルを検索します。一致するプロファイルが見つかった場合、`myNEWemail@example.com`のメールアドレスと`77828292900000`の電話番号を追加します。Identity Serviceが一致するものを見つけられない場合、両方のメールアドレスと電話番号を持つ新しいプロファイルを作成します。

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

Adobe Experience PlatformのIdentity Serviceの構成に関する詳細は、Adobeのドキュメントの以下の記事を参照してください：

* [Identity Service Overview](https://experienceleague.adobe.com/docs/experience-platform/identity/home.html?lang=en)
* [Identity Namespace Overview](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=en)
* [Merge Policies Overview](https://experienceleague.adobe.com/docs/experience-platform/profile/merge-policies/overview.html?lang=en) 
* [Adobe Data Collection](https://experienceleague.adobe.com/docs/experience-platform/sources/connectors/adobe-applications/data-collection.html?lang=en)

#### Adobe Experience Platformの構成


<blockquote>
Adobe Experience Platformで顧客データを更新するには、Adobe製品全体からデータをスティッチングする必要がある場合があります。たとえば、Adobe Journey Optimizerで実行されるメールキャンペーンのためにプロファイルが作成され、その後、Interactive Data Collectionエンドポイントを通じて送信される異なるイベントで更新されることがあります。
</blockquote>


1. Adobe Experience Platformで**Data Management > Schemas**に移動し、使用したいスキーマを選択するか、**Create Schema**をクリックして新しいスキーマを作成します。
    * 新しいスキーマ
        1. **Schema Details**セクションで、**Experience Event**または**Individual Profile**オプションを選択し、**Next**をクリックします。
        1. スキーマの名前を入力し、**Finish**をクリックします。
    * 既存のスキーマ
        1. スキーマの詳細画面で、**Field groups**セクションに移動し、**Personal Contact Details**を選択して**Save**をクリックします。
        1. このスキーマを使用する際に更新したいプロファイル属性を追加します。たとえば、メールアドレスと電話番号を追加するには：
            * **personalEmail**プロパティを展開し、**address**をクリックし、スキーマ画面の右側にある**Field Properties**セクションで**Identity**チェックボックスをクリックします。
            * **mobilePhone**プロパティを展開し、**number**をクリックし、スキーマ画面の右側にある**Field Properties**セクションで**Identity**チェックボックスをクリックします。
1. **Save**をクリックします。![](https://docs.tealium.com/images/server-side-connectors/adobe-identity-schema.png)
1. **Data Management > Datasets**に移動し、**Create Dataset**をクリックします。
1. **Create Dataset from Schema**をクリックし、リストからスキーマを選択して**Next**をクリックします。
1. データセットの名前を入力し、**Finish**をクリックします。
1. **Customer > Profiles**に移動し、**Merge Policies**タブをクリックして**Create merge policy**をクリックします。
1. スキーマ名を入力します。スキーマクラスを**XDM Individual Profile**として、IDスティッチングを**Private Graph**として残し、**Save**をクリックします。
1. **Connection > Sources**に移動し、**Adobe Data Collection**を検索して**Set Up**をクリックします。

詳細については、[Adobe Data Collection](https://experienceleague.adobe.com/docs/experience-platform/sources/connectors/adobe-applications/data-collection.html?lang=en)を参照してください。

#### TealiumでAdobe Experience Platformコネクタを構成する

Adobe Identity Serviceにデータを送信するためにコネクタを構成するには、[TealiumでAdobe Experience Platformコネクタを構成する](#configure-the-adobe-experience-platform-connector-in-tealium)セクションの手順を完了してください。

Event Experienceスキーマを使用している場合は、**Send Event**アクションを作成します。Individual Profileスキーマを使用している場合は、**Stream Record Data**アクションを作成する必要があります。

次の画像はTealiumでの例示的なマッピングを示しています：

![](https://docs.tealium.com/images/server-side-connectors/adobe-identity-service-tealium-setup.png)

#### Adobe Experience Platformでプロファイル更新を確認する

Adobe Experience Platformで更新されたプロファイルを確認するには、**Customer > Profiles**に移動します。すべてのプロファイル属性を表示するには、**Attributes**タブをクリックします。

## Adobe Experience Platformでイベントコールをデバッグする

イベントコールをデバッグするには、**Connection > Sources**に移動し、**Dataflows**タブをクリックします。

データストリーム用に自動的に作成されたデータフローをクリックし、レコードが失敗しているかどうかを確認します。イベントが処理されていない場合は、まだデータフローが表示されないかもしれません。

エラーが見つかった場合は、エラーの詳細を表示するために**Dataflow Run Start**値をクリックします。
![](https://docs.tealium.com/images/server-side-connectors/adobe-dataflows-tab.png)

この例では、タイムスタンプの形式が正しくないため、イベントが処理されていません。
![](https://docs.tealium.com/images/server-side-connectors/adobe-dataflow-run-error.png)