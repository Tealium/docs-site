---
title: Yandex Metrica コネクタ構成ガイド
description: この記事では、Yandex Metricaコネクタの構成方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/yandex-metrica-connector/
---
## API情報

このコネクタは、以下のベンダーAPIを使用します：

* API名：Yandex API
* APIバージョン：v1.0
* APIエンドポイント：`https://api-metrika.yandex.net/cdp/api/v1`
* ドキュメンテーション：[Yandex API](https://yandex.com/dev/metrika/doc/api2/concept/about.html)

## バッチ制限
  
このコネクタは、ベンダーへの大量データ転送をサポートするためにバッチリクエストを使用します。詳細については、[バッチアクション]()を参照してください。リクエストは、以下のいずれかの閾値が達成されるか、プロファイルが公開されるまでキューに入れられます：

* リクエストの最大数：100,000
* 最古のリクエストからの最大時間：5分
* リクエストの最大サイズ：2 MB

## アクション

| アクション名 | AudienceStream | EventStream |
| --- | :---: | :---: |
| Send Order Event | ✗ | ✓ |
| Send Order Event Batch | ✗ | ✓ |
| Upsert Contact | ✓ | ✓ |
| Upsert Contact Batch | ✗ | ✓ |
| Send Page View Event | ✗ | ✓ |
| Send Goal Event | ✓ | ✓ |
| Send Ecommerce Event | ✗ | ✓ |
| Send Advanced Matching Event | ✓ | ✓ |

## 構成

コネクタマーケットプレイスに移動し、新しいコネクタを追加します。コネクタの追加方法の一般的な指示については、[コネクタについて]()を参照してください。

コネクタを追加した後、以下の構成を行います：

* **Bearer Token**：
   * TealiumがYandexアプリにアクセスできるように許可を与えることで、bearerトークンを生成します。[Yandex OAuthサービス](https://oauth.yandex.ru/authorize?response_type=token&amp;client_id=2d25c09a45cc4c7090d6edbb318e65f0)を使用します。
   * Yandexアプリでアクセスを許可した後、トークンをコピーできるページにリダイレクトされます。
   * トークンをYandex Metricaコネクタに貼り付けます。
   * トークンは1年間有効です。
* **Counter ID**：
    構成のためのカウンターID。

## アクション

以下のセクションでは、各アクションでサポートされているパラメータをリストアップしています。

### Send Order Event

#### パラメータ

| **パラメータ** | **説明** |
| --- | --- |
| Update Type | &lt;ul&gt;&lt;li&gt;Save - 以前に送信された情報はすべて新しい情報で完全に置き換えられます。&lt;/li&gt;&lt;li&gt;Update - 現在ロードしている情報のみが更新されます。&lt;/li&gt;&lt;li&gt;Append - 新しい情報が以前にダウンロードしたデータに追加されます。&lt;/li&gt;&lt;/ul&gt; |
| ID | &lt;ul&gt;&lt;li&gt;必須&lt;/li&gt;&lt;li&gt;注文ID。&lt;/li&gt;&lt;/ul&gt; |
| Client Unique ID | &lt;ul&gt;&lt;li&gt;必須&lt;/li&gt;&lt;li&gt;注文に関連付けられたCRMの顧客ID。&lt;/li&gt;&lt;/ul&gt; |
| Create Date Time | &lt;ul&gt;&lt;li&gt;必須&lt;/li&gt;&lt;li&gt;注文が作成された日時（カウンターのタイムゾーン）。この値は変更できません。&lt;/li&gt;&lt;li&gt;詳細については、[日付と時刻の形式](https://yandex.ru/dev/metrika/doc/api2/crm/date.html#orders)を参照してください。&lt;/li&gt;&lt;/ul&gt; |
| Order Status | &lt;ul&gt;&lt;li&gt;必須&lt;/li&gt;&lt;li&gt;注文ステータスID。&lt;/li&gt;&lt;li&gt;任意の文字列。&lt;/li&gt;&lt;li&gt;ステータスは変更可能です。&lt;/li&gt;&lt;li&gt;詳細については、[注文ステータスの比較](https://yandex.ru/dev/metrika/doc/api2/crm/schema/maporderstatuses.html)を参照してください。&lt;/li&gt;&lt;li&gt;デフォルトの可能な値：**PAID**, **IN_PROGRESS**, **CANCELLED**, **SPAM**。&lt;/li&gt;&lt;li&gt;作成した追加の値も受け入れられます。&lt;/li&gt;&lt;/ul&gt; |
| Update Date Time | &lt;ul&gt;&lt;li&gt;注文が更新された日時（カウンターのタイムゾーン）。&lt;/li&gt;&lt;li&gt;パラメータが渡されない場合、値は自動的に代入されます。&lt;/li&gt;&lt;li&gt;詳細については、[日付と時刻の形式](https://yandex.ru/dev/metrika/doc/api2/crm/date.html#orders)を参照してください。&lt;/li&gt;&lt;/ul&gt; |
| Finish Date Time | &lt;ul&gt;&lt;li&gt;注文が完了した日時（カウンターのタイムゾーン）。&lt;/li&gt;&lt;li&gt;詳細については、[日付と時刻の形式](https://yandex.ru/dev/metrika/doc/api2/crm/date.html#orders)を参照してください。&lt;/li&gt;&lt;/ul&gt; |
| Revenue | &lt;ul&gt;&lt;li&gt;収入 - 注文の合計費用。&lt;/li&gt;&lt;li&gt;Decimal - 注文からの収益を転送します。&lt;/li&gt;&lt;li&gt;この値は、広告チャネルからの収入を表示するために[エンドツーエンド分析](https://yandex.ru/dev/metrika/doc/api2/api_v1/presets/preset_crm_orders.html#preset_cdp_orders)レポートで使用されます。&lt;/li&gt;&lt;li&gt;値は**Revenue**メトリックで表示されます。&lt;/li&gt;&lt;/ul&gt; |
| Cost | &lt;ul&gt;&lt;li&gt;原価。&lt;/li&gt;&lt;li&gt;[エンドツーエンド分析](https://yandex.ru/dev/metrika/doc/api2/api_v1/presets/preset_crm_orders.html#preset_cdp_orders)レポートで利益を考慮に入れるために、注文のコストを渡すことができます。&lt;/li&gt;&lt;li&gt;利益は次の式を使用して計算されます：`Revenue - Cost`。&lt;/li&gt;&lt;/ul&gt; |
| Product IDs | &lt;ul&gt;&lt;li&gt;必須&lt;/li&gt;&lt;li&gt;製品識別子とその数量をオブジェクトで渡します。&lt;/li&gt;&lt;li&gt;製品のリストを転送しない場合、識別子はMetricaでセグメントを作成する際に利用可能になります。&lt;/li&gt;&lt;li&gt;[製品のリストを作成](https://yandex.ru/dev/metrika/doc/api2/crm/schema/createproducts.html)する場合、これらのリストからのデータがYandex Metricaで利用可能になります。&lt;/li&gt;&lt;li&gt;例：`{&#34;Product A&#34; : 173, &#34;Product B&#34; : 146}`。&lt;/li&gt;&lt;/ul&gt; |
| Product Quantities | &lt;ul&gt;&lt;li&gt;必須&lt;/li&gt;&lt;li&gt;製品の数量。&lt;/li&gt;&lt;/ul&gt; |
| Attribute Values | &lt;ul&gt;&lt;li&gt;指定した順序でカスタマイズして渡す属性。&lt;/li&gt;&lt;/ul&gt; |

### Send Order Event Batch

#### パラメータ

| **パラメータ** | **説明** |
| --- | --- |
| Update Type | &lt;ul&gt;&lt;li&gt;Save - 以前に送信された情報はすべて新しい情報で完全に置き換えられます。&lt;/li&gt;&lt;li&gt;Update - 現在ロードしている情報のみが更新されます。&lt;/li&gt;&lt;li&gt;Append - 新しい情報が以前にダウンロードしたデータに追加されます。&lt;/li&gt;&lt;/ul&gt; |
| ID | &lt;ul&gt;&lt;li&gt;必須&lt;/li&gt;&lt;li&gt;注文ID。&lt;/li&gt;&lt;/ul&gt; |
| Client Unique ID | &lt;ul&gt;&lt;li&gt;必須&lt;/li&gt;&lt;li&gt;注文に関連付けられたCRMの顧客ID。&lt;/li&gt;&lt;/ul&gt; |
| Create Date Time | &lt;ul&gt;&lt;li&gt;必須&lt;/li&gt;&lt;li&gt;注文が作成された日時（カウンターのタイムゾーン）。この値は変更できません。&lt;/li&gt;&lt;li&gt;詳細については、[日付と時刻の形式](https://yandex.ru/dev/metrika/doc/api2/crm/date.html#orders)を参照してください。&lt;/li&gt;&lt;li&gt;例：`2023-04-21 10:00:00`。&lt;/li&gt;&lt;/ul&gt; |
| Order Status | &lt;ul&gt;&lt;li&gt;必須&lt;/li&gt;&lt;li&gt;注文ステータスID。&lt;/li&gt;&lt;li&gt;任意の文字列。&lt;/li&gt;&lt;li&gt;ステータスは変更可能です。&lt;/li&gt;&lt;li&gt;[idフィールドでステータスをマッチング](https://yandex.ru/dev/metrika/doc/api2/crm/schema/maporderstatuses.html)したときに渡した値を指定します。&lt;/li&gt;&lt;li&gt;デフォルトの可能な値：PAID, IN_PROGRESS, CANCELLED, SPAM。&lt;/li&gt;&lt;li&gt;ユーザーは追加の値を作成できるため、他の値も受け入れる必要があります。&lt;/li&gt;&lt;/ul&gt; |
| Update Date Time | &lt;ul&gt;&lt;li&gt;注文が更新された日時（カウンターのタイムゾーン）。&lt;/li&gt;&lt;li&gt;パラメータが渡されない場合、値は自動的に代入されます。&lt;/li&gt;&lt;li&gt;詳細については、[日付と時刻の形式](https://yandex.ru/dev/metrika/doc/api2/crm/date.html#orders)を参照してください。&lt;/li&gt;&lt;/ul&gt; |
| Finish Date Time | &lt;ul&gt;&lt;li&gt;注文が完了した日時（カウンターのタイムゾーン）。&lt;/li&gt;&lt;li&gt;詳細については、[日付と時刻の形式](https://yandex.ru/dev/metrika/doc/api2/crm/date.html#orders)を参照してください。&lt;/li&gt;&lt;/ul&gt; |
| Revenue | &lt;ul&gt;&lt;li&gt;収入 - 注文の合計費用。&lt;/li&gt;&lt;li&gt;Decimal - 注文からの収益を転送します。&lt;/li&gt;&lt;li&gt;この値は、広告チャネルからの収入を表示するために[エンドツーエンド分析](https://yandex.ru/dev/metrika/doc/api2/api_v1/presets/preset_crm_orders.html#preset_cdp_orders)レポートで使用されます。&lt;/li&gt;&lt;li&gt;値はRevenueメトリックで表示されます。&lt;/li&gt;&lt;/ul&gt; |
| Cost | &lt;ul&gt;&lt;li&gt;原価。&lt;/li&gt;&lt;li&gt;[エンドツーエンド分析](https://yandex.ru/dev/metrika/doc/api2/api_v1/presets/preset_crm_orders.html#preset_cdp_orders)レポートで利益を考慮に入れるために、注文のコストを渡すことができます。&lt;/li&gt;&lt;li&gt;利益は次の式を使用して計算されます：`Revenue - Cost`。&lt;/li&gt;&lt;/ul&gt; |
| 商品ID | &lt;ul&gt;&lt;li&gt;必須&lt;/li&gt;&lt;li&gt;オブジェクト内に商品識別子とその数量を渡します。&lt;/li&gt;&lt;li&gt;商品のリストを転送しない場合、識別子はMetricaでセグメントを作成する際に利用可能になります。&lt;/li&gt;&lt;li&gt;あなたが[商品のリストを作成する](https://yandex.ru/dev/metrika/doc/api2/crm/schema/createproducts.html)場合、これらのリストからのデータはYandex Metricaで利用可能になります。&lt;/li&gt;&lt;li&gt;例えば、`{&#34;Product A&#34; : 173, &#34;Product B&#34; : 146}`。&lt;/li&gt;&lt;/ul&gt; |
| 商品の数量 | &lt;ul&gt;&lt;li&gt;必須&lt;/li&gt;&lt;li&gt;商品の数量。&lt;/li&gt;&lt;/ul&gt; |
| 属性値 | &lt;ul&gt;&lt;li&gt;指定した順序でカスタマイズされ、渡される属性。&lt;/li&gt;&lt;/ul&gt; |

### Upsert Contact

#### パラメータ

| **パラメータ** | **説明** |
| --- | --- |
| 更新タイプ | &lt;ul&gt;&lt;li&gt;保存 - 以前に送信された情報はすべて新しい情報で完全に置き換えられます。&lt;/li&gt;&lt;li&gt;更新 - 現在ロードしている情報のみが更新されます。&lt;/li&gt;&lt;li&gt;追加 - 新しい情報が以前にダウンロードしたデータに追加されます。&lt;/li&gt;&lt;/ul&gt; |
| ユニークID | &lt;ul&gt;&lt;li&gt;必須&lt;/li&gt;&lt;li&gt;カスタムクライアントID。`customer_id`または`tealium_visitor_id`のいずれかになります。&lt;/li&gt;&lt;/ul&gt; |
| クライアントID | &lt;ul&gt;&lt;li&gt;Yandex MetrikaクライアントID (`_ym_uid`)。&lt;/li&gt;&lt;/ul&gt; |
| 名前 | &lt;ul&gt;&lt;li&gt;クライアントの名前。&lt;/li&gt;&lt;li&gt;姓、名、パトロニミックを提供すると、行は**John S**の形式に縮小されます。ここで**S**は姓の省略形です。&lt;/li&gt;&lt;/ul&gt; |
| 作成日時 | &lt;ul&gt;&lt;li&gt;コンタクトがカウンターのタイムゾーンで作成された日時。&lt;/li&gt;&lt;li&gt;値は変更できません。&lt;/li&gt;&lt;li&gt;詳細は[日付と時刻の形式](https://yandex.ru/dev/metrika/doc/api2/crm/date.html#orders)を参照してください。&lt;/li&gt;&lt;/ul&gt; |
| 更新日時 | &lt;ul&gt;&lt;li&gt;コンタクトがカウンターのタイムゾーンで更新された日時。&lt;/li&gt;&lt;li&gt;パラメータが渡されない場合、値は自動的に代入されます。&lt;/li&gt;&lt;li&gt;詳細は[日付と時刻の形式](https://yandex.ru/dev/metrika/doc/api2/crm/date.html#orders)を参照してください。&lt;/li&gt;&lt;/ul&gt; |
| クライアントID | &lt;ul&gt;&lt;li&gt;クライアントIDのリスト。&lt;/li&gt;&lt;/ul&gt; |
| メール | &lt;ul&gt;&lt;li&gt;クライアントのメールアドレスのリスト。&lt;/li&gt;&lt;/ul&gt; |
| 電話番号 | &lt;ul&gt;&lt;li&gt;クライアントの電話番号のリスト。&lt;/li&gt;&lt;/ul&gt; |
| メール MD5 | &lt;ul&gt;&lt;li&gt;クライアントのメールアドレスのリスト、[MD5形式でハッシュ化](https://yandex.ru/dev/metrika/doc/api2/practice/crm/hashing.html#hashing)。&lt;/li&gt;&lt;li&gt;ハッシュ化する前にメールアドレスを正規化します。&lt;/li&gt;&lt;li&gt;テキストを小文字に変換します。&lt;/li&gt;&lt;li&gt;先頭/末尾のスペースとカンマを削除します。&lt;/li&gt;&lt;li&gt;Googleドメインのアドレスの場合、ユーザー名のドットを削除します。例えば、`name.example@gmail.com`を`nameexample@gmail.com`に変換します。&lt;/li&gt;&lt;li&gt;Yandexドメインのアドレスの場合、ユーザー名のドットをダッシュに置き換えます。例えば、`name.example@yandex.ru`を`name-example@yandex.ru`に変換します。&lt;/li&gt;&lt;li&gt;`@ya.ru`や`@yandex.com`などの複数のYandexドメインのアドレスは、`@yandex.ru`に統一します。例えば、`example@@ya.ru`を`example@yandex.ru`に変更します。&lt;/li&gt;&lt;li&gt;メールアドレスに`&#43;`記号が含まれている場合、例えば`name&#43;commercial@example.com`の場合、`&#43;`の前の名前のみを保持します：`name@example.com`。&lt;/li&gt;&lt;/ul&gt; |
| 電話番号 MD5 | &lt;ul&gt;&lt;li&gt;顧客の電話番号のリスト、[MD5形式でハッシュ化](https://yandex.ru/dev/metrika/doc/api2/practice/crm/hashing.html#hashing)。&lt;/li&gt;&lt;li&gt;`&#43;`記号を除いた国コード付きの番号を入力します。&lt;/li&gt;&lt;li&gt;ハッシュ化する前に電話番号を正規化します。&lt;/li&gt;&lt;li&gt;テキストを小文字に変換します。&lt;/li&gt;&lt;li&gt;先頭/末尾のスペースとカンマを削除します。&lt;/li&gt;&lt;li&gt;数字のみを使用します。&lt;/li&gt;&lt;li&gt;例えば、`70123456789`。&lt;/li&gt;&lt;/ul&gt; |
| 属性値 | &lt;ul&gt;&lt;li&gt;指定した順序でカスタマイズされ、渡される属性。&lt;/li&gt;&lt;/ul&gt; |

### Upsert Contact Batch

#### パラメータ

| **パラメータ** | **説明** |
| --- | --- |
| 更新タイプ | &lt;ul&gt;&lt;li&gt;保存 - 以前に送信された情報はすべて新しい情報で完全に置き換えられます。&lt;/li&gt;&lt;li&gt;更新 - 現在ロードしている情報のみが更新されます。&lt;/li&gt;&lt;li&gt;追加 - 新しい情報が以前にダウンロードしたデータに追加されます。&lt;/li&gt;&lt;/ul&gt; |
| ユニークID | &lt;ul&gt;&lt;li&gt;必須&lt;/li&gt;&lt;li&gt;カスタムクライアントID。`customer_id`または`tealium_visitor_id`のいずれかになります。&lt;/li&gt;&lt;/ul&gt; |
| クライアントID | &lt;ul&gt;&lt;li&gt;必須&lt;/li&gt;&lt;li&gt;Yandex MetrikaクライアントID (`_ym_uid`)。&lt;/li&gt;&lt;/ul&gt; |
| 名前 | &lt;ul&gt;&lt;li&gt;クライアントの名前。&lt;/li&gt;&lt;li&gt;姓、名、パトロニミックを提供すると、行は**John S**の形式に縮小されます。ここで**S**は姓の省略形です。&lt;/li&gt;&lt;/ul&gt; |
| 作成日時 | &lt;ul&gt;&lt;li&gt;コンタクトがカウンターのタイムゾーンで作成された日時。&lt;/li&gt;&lt;li&gt;値は変更できません。&lt;/li&gt;&lt;li&gt;詳細は[日付と時刻の形式](https://yandex.ru/dev/metrika/doc/api2/crm/date.html#orders)を参照してください。&lt;/li&gt;&lt;/ul&gt; |
| 更新日時 | &lt;ul&gt;&lt;li&gt;コンタクトがカウンターのタイムゾーンで更新された日時。&lt;/li&gt;&lt;li&gt;パラメータが渡されない場合、値は自動的に代入されます。&lt;/li&gt;&lt;li&gt;詳細は[日付と時刻の形式](https://yandex.ru/dev/metrika/doc/api2/crm/date.html#orders)を参照してください。&lt;/li&gt;&lt;/ul&gt; |
| クライアントID | &lt;ul&gt;&lt;li&gt;クライアントIDのリスト。&lt;/li&gt;&lt;/ul&gt; |
| メール | &lt;ul&gt;&lt;li&gt;クライアントのメールアドレスのリスト。&lt;/li&gt;&lt;/ul&gt; |
| 電話番号 | &lt;ul&gt;&lt;li&gt;クライアントの電話番号のリスト。&lt;/li&gt;&lt;/ul&gt; |
| メール MD5 | &lt;ul&gt;&lt;li&gt;クライアントのメールアドレスのリスト、[MD5形式でハッシュ化](https://yandex.ru/dev/metrika/doc/api2/practice/crm/hashing.html#hashing)。&lt;/li&gt;&lt;li&gt;ハッシュ化する前にメールアドレスを正規化します。&lt;/li&gt;&lt;li&gt;テキストを小文字に変換します。&lt;/li&gt;&lt;li&gt;先頭/末尾のスペースとカンマを削除します。&lt;/li&gt;&lt;li&gt;Googleドメインのアドレスの場合、ユーザー名のドットを削除します。例えば、`name.example@gmail.com`を`nameexample@gmail.com`に変換します。&lt;/li&gt;&lt;li&gt;Yandexドメインのアドレスの場合、ユーザー名のドットをダッシュに置き換えます。例えば、`name.example@yandex.ru`を`name-example@yandex.ru`に変換します。&lt;/li&gt;&lt;li&gt;`@ya.ru`や`@yandex.com`などの複数のYandexドメインのアドレスは、`@yandex.ru`に統一します。例えば、`example@@ya.ru`を`example@yandex.ru`に変更します。&lt;/li&gt;&lt;li&gt;メールアドレスに`&#43;`記号が含まれている場合、例えば`name&#43;commercial@example.com`の場合、`&#43;`の前の名前のみを保持します：`name@example.com`。&lt;/li&gt;&lt;/ul&gt; |
| 電話番号 MD5 | &lt;ul&gt;&lt;li&gt;顧客の電話番号のリスト、[MD5形式でハッシュ化](https://yandex.ru/dev/metrika/doc/api2/practice/crm/hashing.html#hashing)。&lt;/li&gt;&lt;li&gt;`&#43;`記号を除いた国コード付きの番号を入力します。&lt;/li&gt;&lt;li&gt;ハッシュ化する前に電話番号を正規化します。&lt;/li&gt;&lt;li&gt;テキストを小文字に変換します。&lt;/li&gt;&lt;li&gt;先頭/末尾のスペースとカンマを削除します。&lt;/li&gt;&lt;li&gt;数字のみを使用します。&lt;/li&gt;&lt;li&gt;例えば、`70123456789`。&lt;/li&gt;&lt;/ul&gt; |
| 属性値 | &lt;ul&gt;&lt;li&gt;指定した順序でカスタマイズされ、渡される属性。&lt;/li&gt;&lt;/ul&gt; |

### Send Page View Event

#### パラメータ

| **パラメータ** | **説明** |
| --- | --- |
| ページURL | &lt;ul&gt;&lt;li&gt;現在のURL&lt;/li&gt;&lt;/ul&gt; |
| YandexクライアントID | &lt;ul&gt;&lt;li&gt;必須&lt;/li&gt;&lt;li&gt;Yandex MetricaクライアントID (`_ym_uid`)。&lt;/li&gt;&lt;/ul&gt; |
| ページRef | &lt;ul&gt;&lt;li&gt;リファラルURL。空の場合、デフォルトのURLは`https://tealium.com`です。&lt;/li&gt;&lt;/ul&gt; |
| サイト情報 | &lt;ul&gt;&lt;li&gt;カスタムオブジェクト。&lt;/li&gt;&lt;/ul&gt; |
| カスタムクエリパラメータ | &lt;ul&gt;&lt;li&gt;追加のカスタムクエリパラメータ。&lt;/li&gt;&lt;/ul&gt; |

### 新しいセッションを作成する

#### パラメータ

| **パラメータ** | **説明** |
| --- | --- |
| ページURL | &lt;ul&gt;&lt;li&gt;現在のURL&lt;/li&gt;&lt;/ul&gt; |
| YandexクライアントID | &lt;ul&gt;&lt;li&gt;必須&lt;/li&gt;&lt;li&gt;Yandex MetricaクライアントID (`_ym_uid`)。&lt;/li&gt;&lt;/ul&gt; |
| ページRef | &lt;ul&gt;&lt;li&gt;リファラルURL。空の場合、デフォルトのURLは`https://tealium.com`です。&lt;/li&gt;&lt;/ul&gt; |
| サイト情報 | &lt;ul&gt;&lt;li&gt;カスタムオブジェクト。&lt;/li&gt;&lt;/ul&gt; |
| カスタムクエリパラメータ | &lt;ul&gt;&lt;li&gt;追加のカスタムクエリパラメータ。&lt;/li&gt;&lt;/ul&gt; |

### Send Goal Event

#### パラメータ

| **パラメータ** | **説明** |
| --- | --- |
| トリガーオープンセッションコール | &lt;ul&gt;&lt;li&gt;Yandex Metricaは、**Send Goal Event**アクションをトリガーする前にオープンセッションコールが必要です。&lt;/li&gt;&lt;/ul&gt; |
| サイトドメイン | &lt;ul&gt;&lt;li&gt;必須&lt;/li&gt;&lt;li&gt;サイトのドメイン。&lt;/li&gt;&lt;/ul&gt; |
| ゴールID | &lt;ul&gt;&lt;li&gt;必須&lt;/li&gt;&lt;li&gt;ゴールの番号。&lt;/li&gt;&lt;/ul&gt; |
| YandexクライアントID | &lt;ul&gt;&lt;li&gt;必須&lt;/li&gt;&lt;li&gt;Yandex MetricaクライアントID (`_ym_uid`)&lt;/li&gt;&lt;/ul&gt; |
| ページRef | &lt;ul&gt;&lt;li&gt;リファラルURL。空の場合、デフォルトのURLは`https://tealium.com`です。&lt;/li&gt;&lt;/ul&gt; |
| サイト情報 | &lt;ul&gt;&lt;li&gt;カスタムオブジェクト。&lt;/li&gt;&lt;/ul&gt; |
| カスタムクエリパラメータ | &lt;ul&gt;&lt;li&gt;追加のカスタムクエリパラメータ。&lt;/li&gt;&lt;/ul&gt; |

### Eコマースイベントを送信

#### パラメータ

| **パラメータ** | **説明** |
| --- | --- |
| トリガーオープンセッションコール | &lt;ul&gt;&lt;li&gt;Yandex Metricaは、**Eコマースイベントを送信**アクションをトリガーする前に、オープンセッションコールが必要です。&lt;/li&gt;&lt;/ul&gt; |
| ページURL | &lt;ul&gt;&lt;li&gt;リファラルURL。空の場合、デフォルトのURLは `https://tealium.com` です。&lt;/li&gt;&lt;/ul&gt; |
| YandexクライアントID | &lt;ul&gt;&lt;li&gt;必須&lt;/li&gt;&lt;li&gt;Yandex MetricaクライアントID (`_ym_uid`)。&lt;/li&gt;&lt;/ul&gt; |
| アクションタイプ | &lt;ul&gt;&lt;li&gt;`actionType`を置き換えるフィールド名は、一連の製品で実行されるアクションの識別子として機能します。&lt;/li&gt;&lt;li&gt;可能な値：&lt;/li&gt;&lt;li&gt;詳細：アイテムの完全な説明（製品カード）を表示します。&lt;/li&gt;&lt;li&gt;追加：アイテムをバスケットに追加します。&lt;/li&gt;&lt;li&gt;削除：アイテムをバスケットから削除します。&lt;/li&gt;&lt;li&gt; 購入：アイテムを購入します。&lt;/li&gt;&lt;li&gt;アイテムの削除に関する情報がYandex Metricaに送信された場合、レポートにはアイテムの負の数（合計は、削除されたアイテムの数を追加されたアイテムの合計から引いたもの）が表示される可能性があります。アイテムの価格が送信された場合、レポートには負の値が表示される可能性があります。&lt;/li&gt;&lt;/ul&gt; |
| 通貨コード | &lt;ul&gt;&lt;li&gt;3文字の[ISO 4217通貨コード](https://www.six-group.com/en/products-services/financial-information/data-standards.html#scrollTo=currency-codes)。&lt;/li&gt;&lt;li&gt;異なる通貨が渡された場合、通貨と金額の代わりにnull値が送信されます。&lt;/li&gt;&lt;/ul&gt; |
| ID | &lt;ul&gt;&lt;li&gt;購入した製品のID。&lt;/li&gt;&lt;/ul&gt; |
| クーポン | &lt;ul&gt;&lt;li&gt;全体の購入に関連するプロモーションコード。&lt;/li&gt;&lt;/ul&gt; |
| ゴールID | &lt;ul&gt;&lt;li&gt;[ゴール](https://yandex.ru/support/metrica/general/goals.html)番号。&lt;/li&gt;&lt;li&gt;**Eコマースイベントを送信** [アクション](https://yandex.ru/support/metrica/ecommerce/data.html#about__action_type)がゴールであった場合に指定します。&lt;/li&gt;&lt;li&gt;ゴールは[JavaScriptイベント](https://yandex.ru/support/metrica/general/goal-js-event.html)タイプとして構成する必要があります。&lt;/li&gt;&lt;li&gt;ゴール番号を見るには、Yandex Metricaダッシュボードで**ゴール**タブを選択し、**構成**を選択します。&lt;/li&gt;&lt;/ul&gt; |
| 収益 | &lt;ul&gt;&lt;li&gt;受け取った収益。&lt;/li&gt;&lt;li&gt;省略された場合、購入に関連するすべてのアイテムの価格の合計として自動的に計算されます。&lt;/li&gt;&lt;/ul&gt; |
| ID | &lt;ul&gt;&lt;li&gt;アイテムID。&lt;/li&gt;&lt;li&gt;例えば、SKU。&lt;/li&gt;&lt;li&gt;**名前**または**ID**のいずれかを指定する必要があります。&lt;/li&gt;&lt;/ul&gt; |
| 名前 | &lt;ul&gt;&lt;li&gt;製品の名前。&lt;/li&gt;&lt;li&gt; 例えば、**Tシャツ**。&lt;/li&gt;&lt;li&gt;**名前**または**ID**のいずれかを指定する必要があります。&lt;/li&gt;&lt;/ul&gt; |
| ブランド | &lt;ul&gt;&lt;li&gt;アイテムに関連するブランドまたは商標。&lt;/li&gt;&lt;li&gt;例えば、**Yandex**。&lt;/li&gt;&lt;/ul&gt; |
| カテゴリ | &lt;ul&gt;&lt;li&gt;アイテムが属するカテゴリ。&lt;/li&gt;&lt;li&gt;カテゴリの階層は最大5レベルまでサポートしています。レベルを区切るには `/` 記号を使用します。&lt;/li&gt;&lt;li&gt;例えば、**衣類/男性用**、**衣類/Tシャツ**。&lt;/li&gt;&lt;/ul&gt; |
| クーポン | &lt;ul&gt;&lt;li&gt;アイテムに関連するプロモーションコード。&lt;/li&gt;&lt;li&gt;例えば、`PARTNER_SITE_15.`&lt;/li&gt;&lt;/ul&gt; |
| 位置 | &lt;ul&gt;&lt;li&gt;リスト内のアイテムの位置。&lt;/li&gt;&lt;li&gt;例えば、`2`。&lt;/li&gt;&lt;/ul&gt; |
| 価格 | &lt;ul&gt;&lt;li&gt;製品単位の価格。&lt;/li&gt;&lt;/ul&gt; |
| 数量 | &lt;ul&gt;&lt;li&gt;製品単位の数量。&lt;/li&gt;&lt;/ul&gt; |
| バリアント | &lt;ul&gt;&lt;li&gt;アイテムのバリエーション。&lt;/li&gt;&lt;li&gt;例えば、**赤**。&lt;/li&gt;&lt;/ul&gt; |
| カスタムクエリパラメータ | &lt;ul&gt;&lt;li&gt;追加のカスタムクエリパラメータ。&lt;/li&gt;&lt;/ul&gt; |

### アドバンスドマッチングイベントを送信

#### パラメータ

| **パラメータ** | **説明** |
| --- | --- |
| トリガーオープンセッションコール | Yandex Metricaは、**アドバンスドマッチングイベントを送信**アクションをトリガーする前に、オープンセッションコールが必要です。 |
| ページURL | リファラルURL。空の場合、デフォルトのURLは `https://tealium.com` です。 |
| YandexクライアントID | 必須。Yandex MetricaクライアントID (`_ym_uid`)。 |
| MD5ハッシュ化 | 値がMD5ハッシュ化されている場合は選択します。 |
| メール | ユーザーのメールアドレス。 |
| 電話番号 | 国コードを含む電話番号を入力します。`&#43;`記号とスペースは含めません。例えば、`70123456789`。 |
| 名 | ユーザーの名前。 |
| 姓 | ユーザーの姓。 |
| 通り | 通り。 |
| 市区町村 | 市区町村。 |
| 地域 | 地域。 |
| 郵便番号 | 任意の整数を受け入れます。 |
| 国 | 任意の文字列を受け入れます。 |
| カスタムクエリパラメータ | 追加のカスタムクエリパラメータ。 |
