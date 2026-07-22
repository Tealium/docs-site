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
  
このコネクタは、ベンダーへの大量データ転送をサポートするためにバッチリクエストを使用します。詳細については、[バッチアクション](https://docs.tealium.com/batched-actions/)を参照してください。リクエストは、以下のいずれかの閾値が達成されるか、プロファイルが公開されるまでキューに入れられます：

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

コネクタマーケットプレイスに移動し、新しいコネクタを追加します。コネクタの追加方法の一般的な指示については、[コネクタについて](https://docs.tealium.com/about-connectors/)を参照してください。

コネクタを追加した後、以下の構成を行います：

* **Bearer Token**：
   * TealiumがYandexアプリにアクセスできるように許可を与えることで、bearerトークンを生成します。[Yandex OAuthサービス](https://oauth.yandex.ru/authorize?response_type=token&client_id=2d25c09a45cc4c7090d6edbb318e65f0)を使用します。
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
| Update Type | <ul><li>Save - 以前に送信された情報はすべて新しい情報で完全に置き換えられます。</li><li>Update - 現在ロードしている情報のみが更新されます。</li><li>Append - 新しい情報が以前にダウンロードしたデータに追加されます。</li></ul> |
| ID | <ul><li>必須</li><li>注文ID。</li></ul> |
| Client Unique ID | <ul><li>必須</li><li>注文に関連付けられたCRMの顧客ID。</li></ul> |
| Create Date Time | <ul><li>必須</li><li>注文が作成された日時（カウンターのタイムゾーン）。この値は変更できません。</li><li>詳細については、[日付と時刻の形式](https://yandex.ru/dev/metrika/doc/api2/crm/date.html#orders)を参照してください。</li></ul> |
| Order Status | <ul><li>必須</li><li>注文ステータスID。</li><li>任意の文字列。</li><li>ステータスは変更可能です。</li><li>詳細については、[注文ステータスの比較](https://yandex.ru/dev/metrika/doc/api2/crm/schema/maporderstatuses.html)を参照してください。</li><li>デフォルトの可能な値：**PAID**, **IN_PROGRESS**, **CANCELLED**, **SPAM**。</li><li>作成した追加の値も受け入れられます。</li></ul> |
| Update Date Time | <ul><li>注文が更新された日時（カウンターのタイムゾーン）。</li><li>パラメータが渡されない場合、値は自動的に代入されます。</li><li>詳細については、[日付と時刻の形式](https://yandex.ru/dev/metrika/doc/api2/crm/date.html#orders)を参照してください。</li></ul> |
| Finish Date Time | <ul><li>注文が完了した日時（カウンターのタイムゾーン）。</li><li>詳細については、[日付と時刻の形式](https://yandex.ru/dev/metrika/doc/api2/crm/date.html#orders)を参照してください。</li></ul> |
| Revenue | <ul><li>収入 - 注文の合計費用。</li><li>Decimal - 注文からの収益を転送します。</li><li>この値は、広告チャネルからの収入を表示するために[エンドツーエンド分析](https://yandex.ru/dev/metrika/doc/api2/api_v1/presets/preset_crm_orders.html#preset_cdp_orders)レポートで使用されます。</li><li>値は**Revenue**メトリックで表示されます。</li></ul> |
| Cost | <ul><li>原価。</li><li>[エンドツーエンド分析](https://yandex.ru/dev/metrika/doc/api2/api_v1/presets/preset_crm_orders.html#preset_cdp_orders)レポートで利益を考慮に入れるために、注文のコストを渡すことができます。</li><li>利益は次の式を使用して計算されます：`Revenue - Cost`。</li></ul> |
| Product IDs | <ul><li>必須</li><li>製品識別子とその数量をオブジェクトで渡します。</li><li>製品のリストを転送しない場合、識別子はMetricaでセグメントを作成する際に利用可能になります。</li><li>[製品のリストを作成](https://yandex.ru/dev/metrika/doc/api2/crm/schema/createproducts.html)する場合、これらのリストからのデータがYandex Metricaで利用可能になります。</li><li>例：`{"Product A" : 173, "Product B" : 146}`。</li></ul> |
| Product Quantities | <ul><li>必須</li><li>製品の数量。</li></ul> |
| Attribute Values | <ul><li>指定した順序でカスタマイズして渡す属性。</li></ul> |

### Send Order Event Batch

#### パラメータ

| **パラメータ** | **説明** |
| --- | --- |
| Update Type | <ul><li>Save - 以前に送信された情報はすべて新しい情報で完全に置き換えられます。</li><li>Update - 現在ロードしている情報のみが更新されます。</li><li>Append - 新しい情報が以前にダウンロードしたデータに追加されます。</li></ul> |
| ID | <ul><li>必須</li><li>注文ID。</li></ul> |
| Client Unique ID | <ul><li>必須</li><li>注文に関連付けられたCRMの顧客ID。</li></ul> |
| Create Date Time | <ul><li>必須</li><li>注文が作成された日時（カウンターのタイムゾーン）。この値は変更できません。</li><li>詳細については、[日付と時刻の形式](https://yandex.ru/dev/metrika/doc/api2/crm/date.html#orders)を参照してください。</li><li>例：`2023-04-21 10:00:00`。</li></ul> |
| Order Status | <ul><li>必須</li><li>注文ステータスID。</li><li>任意の文字列。</li><li>ステータスは変更可能です。</li><li>[idフィールドでステータスをマッチング](https://yandex.ru/dev/metrika/doc/api2/crm/schema/maporderstatuses.html)したときに渡した値を指定します。</li><li>デフォルトの可能な値：PAID, IN_PROGRESS, CANCELLED, SPAM。</li><li>ユーザーは追加の値を作成できるため、他の値も受け入れる必要があります。</li></ul> |
| Update Date Time | <ul><li>注文が更新された日時（カウンターのタイムゾーン）。</li><li>パラメータが渡されない場合、値は自動的に代入されます。</li><li>詳細については、[日付と時刻の形式](https://yandex.ru/dev/metrika/doc/api2/crm/date.html#orders)を参照してください。</li></ul> |
| Finish Date Time | <ul><li>注文が完了した日時（カウンターのタイムゾーン）。</li><li>詳細については、[日付と時刻の形式](https://yandex.ru/dev/metrika/doc/api2/crm/date.html#orders)を参照してください。</li></ul> |
| Revenue | <ul><li>収入 - 注文の合計費用。</li><li>Decimal - 注文からの収益を転送します。</li><li>この値は、広告チャネルからの収入を表示するために[エンドツーエンド分析](https://yandex.ru/dev/metrika/doc/api2/api_v1/presets/preset_crm_orders.html#preset_cdp_orders)レポートで使用されます。</li><li>値はRevenueメトリックで表示されます。</li></ul> |
| Cost | <ul><li>原価。</li><li>[エンドツーエンド分析](https://yandex.ru/dev/metrika/doc/api2/api_v1/presets/preset_crm_orders.html#preset_cdp_orders)レポートで利益を考慮に入れるために、注文のコストを渡すことができます。</li><li>利益は次の式を使用して計算されます：`Revenue - Cost`。</li></ul> |
| 商品ID | <ul><li>必須</li><li>オブジェクト内に商品識別子とその数量を渡します。</li><li>商品のリストを転送しない場合、識別子はMetricaでセグメントを作成する際に利用可能になります。</li><li>あなたが[商品のリストを作成する](https://yandex.ru/dev/metrika/doc/api2/crm/schema/createproducts.html)場合、これらのリストからのデータはYandex Metricaで利用可能になります。</li><li>例えば、`{"Product A" : 173, "Product B" : 146}`。</li></ul> |
| 商品の数量 | <ul><li>必須</li><li>商品の数量。</li></ul> |
| 属性値 | <ul><li>指定した順序でカスタマイズされ、渡される属性。</li></ul> |

### Upsert Contact

#### パラメータ

| **パラメータ** | **説明** |
| --- | --- |
| 更新タイプ | <ul><li>保存 - 以前に送信された情報はすべて新しい情報で完全に置き換えられます。</li><li>更新 - 現在ロードしている情報のみが更新されます。</li><li>追加 - 新しい情報が以前にダウンロードしたデータに追加されます。</li></ul> |
| ユニークID | <ul><li>必須</li><li>カスタムクライアントID。`customer_id`または`tealium_visitor_id`のいずれかになります。</li></ul> |
| クライアントID | <ul><li>Yandex MetrikaクライアントID (`_ym_uid`)。</li></ul> |
| 名前 | <ul><li>クライアントの名前。</li><li>姓、名、パトロニミックを提供すると、行は**John S**の形式に縮小されます。ここで**S**は姓の省略形です。</li></ul> |
| 作成日時 | <ul><li>コンタクトがカウンターのタイムゾーンで作成された日時。</li><li>値は変更できません。</li><li>詳細は[日付と時刻の形式](https://yandex.ru/dev/metrika/doc/api2/crm/date.html#orders)を参照してください。</li></ul> |
| 更新日時 | <ul><li>コンタクトがカウンターのタイムゾーンで更新された日時。</li><li>パラメータが渡されない場合、値は自動的に代入されます。</li><li>詳細は[日付と時刻の形式](https://yandex.ru/dev/metrika/doc/api2/crm/date.html#orders)を参照してください。</li></ul> |
| クライアントID | <ul><li>クライアントIDのリスト。</li></ul> |
| メール | <ul><li>クライアントのメールアドレスのリスト。</li></ul> |
| 電話番号 | <ul><li>クライアントの電話番号のリスト。</li></ul> |
| メール MD5 | <ul><li>クライアントのメールアドレスのリスト、[MD5形式でハッシュ化](https://yandex.ru/dev/metrika/doc/api2/practice/crm/hashing.html#hashing)。</li><li>ハッシュ化する前にメールアドレスを正規化します。</li><li>テキストを小文字に変換します。</li><li>先頭/末尾のスペースとカンマを削除します。</li><li>Googleドメインのアドレスの場合、ユーザー名のドットを削除します。例えば、`name.example@gmail.com`を`nameexample@gmail.com`に変換します。</li><li>Yandexドメインのアドレスの場合、ユーザー名のドットをダッシュに置き換えます。例えば、`name.example@yandex.ru`を`name-example@yandex.ru`に変換します。</li><li>`@ya.ru`や`@yandex.com`などの複数のYandexドメインのアドレスは、`@yandex.ru`に統一します。例えば、`example@@ya.ru`を`example@yandex.ru`に変更します。</li><li>メールアドレスに`+`記号が含まれている場合、例えば`name+commercial@example.com`の場合、`+`の前の名前のみを保持します：`name@example.com`。</li></ul> |
| 電話番号 MD5 | <ul><li>顧客の電話番号のリスト、[MD5形式でハッシュ化](https://yandex.ru/dev/metrika/doc/api2/practice/crm/hashing.html#hashing)。</li><li>`+`記号を除いた国コード付きの番号を入力します。</li><li>ハッシュ化する前に電話番号を正規化します。</li><li>テキストを小文字に変換します。</li><li>先頭/末尾のスペースとカンマを削除します。</li><li>数字のみを使用します。</li><li>例えば、`70123456789`。</li></ul> |
| 属性値 | <ul><li>指定した順序でカスタマイズされ、渡される属性。</li></ul> |

### Upsert Contact Batch

#### パラメータ

| **パラメータ** | **説明** |
| --- | --- |
| 更新タイプ | <ul><li>保存 - 以前に送信された情報はすべて新しい情報で完全に置き換えられます。</li><li>更新 - 現在ロードしている情報のみが更新されます。</li><li>追加 - 新しい情報が以前にダウンロードしたデータに追加されます。</li></ul> |
| ユニークID | <ul><li>必須</li><li>カスタムクライアントID。`customer_id`または`tealium_visitor_id`のいずれかになります。</li></ul> |
| クライアントID | <ul><li>必須</li><li>Yandex MetrikaクライアントID (`_ym_uid`)。</li></ul> |
| 名前 | <ul><li>クライアントの名前。</li><li>姓、名、パトロニミックを提供すると、行は**John S**の形式に縮小されます。ここで**S**は姓の省略形です。</li></ul> |
| 作成日時 | <ul><li>コンタクトがカウンターのタイムゾーンで作成された日時。</li><li>値は変更できません。</li><li>詳細は[日付と時刻の形式](https://yandex.ru/dev/metrika/doc/api2/crm/date.html#orders)を参照してください。</li></ul> |
| 更新日時 | <ul><li>コンタクトがカウンターのタイムゾーンで更新された日時。</li><li>パラメータが渡されない場合、値は自動的に代入されます。</li><li>詳細は[日付と時刻の形式](https://yandex.ru/dev/metrika/doc/api2/crm/date.html#orders)を参照してください。</li></ul> |
| クライアントID | <ul><li>クライアントIDのリスト。</li></ul> |
| メール | <ul><li>クライアントのメールアドレスのリスト。</li></ul> |
| 電話番号 | <ul><li>クライアントの電話番号のリスト。</li></ul> |
| メール MD5 | <ul><li>クライアントのメールアドレスのリスト、[MD5形式でハッシュ化](https://yandex.ru/dev/metrika/doc/api2/practice/crm/hashing.html#hashing)。</li><li>ハッシュ化する前にメールアドレスを正規化します。</li><li>テキストを小文字に変換します。</li><li>先頭/末尾のスペースとカンマを削除します。</li><li>Googleドメインのアドレスの場合、ユーザー名のドットを削除します。例えば、`name.example@gmail.com`を`nameexample@gmail.com`に変換します。</li><li>Yandexドメインのアドレスの場合、ユーザー名のドットをダッシュに置き換えます。例えば、`name.example@yandex.ru`を`name-example@yandex.ru`に変換します。</li><li>`@ya.ru`や`@yandex.com`などの複数のYandexドメインのアドレスは、`@yandex.ru`に統一します。例えば、`example@@ya.ru`を`example@yandex.ru`に変更します。</li><li>メールアドレスに`+`記号が含まれている場合、例えば`name+commercial@example.com`の場合、`+`の前の名前のみを保持します：`name@example.com`。</li></ul> |
| 電話番号 MD5 | <ul><li>顧客の電話番号のリスト、[MD5形式でハッシュ化](https://yandex.ru/dev/metrika/doc/api2/practice/crm/hashing.html#hashing)。</li><li>`+`記号を除いた国コード付きの番号を入力します。</li><li>ハッシュ化する前に電話番号を正規化します。</li><li>テキストを小文字に変換します。</li><li>先頭/末尾のスペースとカンマを削除します。</li><li>数字のみを使用します。</li><li>例えば、`70123456789`。</li></ul> |
| 属性値 | <ul><li>指定した順序でカスタマイズされ、渡される属性。</li></ul> |

### Send Page View Event

#### パラメータ

| **パラメータ** | **説明** |
| --- | --- |
| ページURL | <ul><li>現在のURL</li></ul> |
| YandexクライアントID | <ul><li>必須</li><li>Yandex MetricaクライアントID (`_ym_uid`)。</li></ul> |
| ページRef | <ul><li>リファラルURL。空の場合、デフォルトのURLは`https://tealium.com`です。</li></ul> |
| サイト情報 | <ul><li>カスタムオブジェクト。</li></ul> |
| カスタムクエリパラメータ | <ul><li>追加のカスタムクエリパラメータ。</li></ul> |

### 新しいセッションを作成する

#### パラメータ

| **パラメータ** | **説明** |
| --- | --- |
| ページURL | <ul><li>現在のURL</li></ul> |
| YandexクライアントID | <ul><li>必須</li><li>Yandex MetricaクライアントID (`_ym_uid`)。</li></ul> |
| ページRef | <ul><li>リファラルURL。空の場合、デフォルトのURLは`https://tealium.com`です。</li></ul> |
| サイト情報 | <ul><li>カスタムオブジェクト。</li></ul> |
| カスタムクエリパラメータ | <ul><li>追加のカスタムクエリパラメータ。</li></ul> |

### Send Goal Event

#### パラメータ

| **パラメータ** | **説明** |
| --- | --- |
| トリガーオープンセッションコール | <ul><li>Yandex Metricaは、**Send Goal Event**アクションをトリガーする前にオープンセッションコールが必要です。</li></ul> |
| サイトドメイン | <ul><li>必須</li><li>サイトのドメイン。</li></ul> |
| ゴールID | <ul><li>必須</li><li>ゴールの番号。</li></ul> |
| YandexクライアントID | <ul><li>必須</li><li>Yandex MetricaクライアントID (`_ym_uid`)</li></ul> |
| ページRef | <ul><li>リファラルURL。空の場合、デフォルトのURLは`https://tealium.com`です。</li></ul> |
| サイト情報 | <ul><li>カスタムオブジェクト。</li></ul> |
| カスタムクエリパラメータ | <ul><li>追加のカスタムクエリパラメータ。</li></ul> |

### Eコマースイベントを送信

#### パラメータ

| **パラメータ** | **説明** |
| --- | --- |
| トリガーオープンセッションコール | <ul><li>Yandex Metricaは、**Eコマースイベントを送信**アクションをトリガーする前に、オープンセッションコールが必要です。</li></ul> |
| ページURL | <ul><li>リファラルURL。空の場合、デフォルトのURLは `https://tealium.com` です。</li></ul> |
| YandexクライアントID | <ul><li>必須</li><li>Yandex MetricaクライアントID (`_ym_uid`)。</li></ul> |
| アクションタイプ | <ul><li>`actionType`を置き換えるフィールド名は、一連の製品で実行されるアクションの識別子として機能します。</li><li>可能な値：</li><li>詳細：アイテムの完全な説明（製品カード）を表示します。</li><li>追加：アイテムをバスケットに追加します。</li><li>削除：アイテムをバスケットから削除します。</li><li> 購入：アイテムを購入します。</li><li>アイテムの削除に関する情報がYandex Metricaに送信された場合、レポートにはアイテムの負の数（合計は、削除されたアイテムの数を追加されたアイテムの合計から引いたもの）が表示される可能性があります。アイテムの価格が送信された場合、レポートには負の値が表示される可能性があります。</li></ul> |
| 通貨コード | <ul><li>3文字の[ISO 4217通貨コード](https://www.six-group.com/en/products-services/financial-information/data-standards.html#scrollTo=currency-codes)。</li><li>異なる通貨が渡された場合、通貨と金額の代わりにnull値が送信されます。</li></ul> |
| ID | <ul><li>購入した製品のID。</li></ul> |
| クーポン | <ul><li>全体の購入に関連するプロモーションコード。</li></ul> |
| ゴールID | <ul><li>[ゴール](https://yandex.ru/support/metrica/general/goals.html)番号。</li><li>**Eコマースイベントを送信** [アクション](https://yandex.ru/support/metrica/ecommerce/data.html#about__action_type)がゴールであった場合に指定します。</li><li>ゴールは[JavaScriptイベント](https://yandex.ru/support/metrica/general/goal-js-event.html)タイプとして構成する必要があります。</li><li>ゴール番号を見るには、Yandex Metricaダッシュボードで**ゴール**タブを選択し、**構成**を選択します。</li></ul> |
| 収益 | <ul><li>受け取った収益。</li><li>省略された場合、購入に関連するすべてのアイテムの価格の合計として自動的に計算されます。</li></ul> |
| ID | <ul><li>アイテムID。</li><li>例えば、SKU。</li><li>**名前**または**ID**のいずれかを指定する必要があります。</li></ul> |
| 名前 | <ul><li>製品の名前。</li><li> 例えば、**Tシャツ**。</li><li>**名前**または**ID**のいずれかを指定する必要があります。</li></ul> |
| ブランド | <ul><li>アイテムに関連するブランドまたは商標。</li><li>例えば、**Yandex**。</li></ul> |
| カテゴリ | <ul><li>アイテムが属するカテゴリ。</li><li>カテゴリの階層は最大5レベルまでサポートしています。レベルを区切るには `/` 記号を使用します。</li><li>例えば、**衣類/男性用**、**衣類/Tシャツ**。</li></ul> |
| クーポン | <ul><li>アイテムに関連するプロモーションコード。</li><li>例えば、`PARTNER_SITE_15.`</li></ul> |
| 位置 | <ul><li>リスト内のアイテムの位置。</li><li>例えば、`2`。</li></ul> |
| 価格 | <ul><li>製品単位の価格。</li></ul> |
| 数量 | <ul><li>製品単位の数量。</li></ul> |
| バリアント | <ul><li>アイテムのバリエーション。</li><li>例えば、**赤**。</li></ul> |
| カスタムクエリパラメータ | <ul><li>追加のカスタムクエリパラメータ。</li></ul> |

### アドバンスドマッチングイベントを送信

#### パラメータ

| **パラメータ** | **説明** |
| --- | --- |
| トリガーオープンセッションコール | Yandex Metricaは、**アドバンスドマッチングイベントを送信**アクションをトリガーする前に、オープンセッションコールが必要です。 |
| ページURL | リファラルURL。空の場合、デフォルトのURLは `https://tealium.com` です。 |
| YandexクライアントID | 必須。Yandex MetricaクライアントID (`_ym_uid`)。 |
| MD5ハッシュ化 | 値がMD5ハッシュ化されている場合は選択します。 |
| メール | ユーザーのメールアドレス。 |
| 電話番号 | 国コードを含む電話番号を入力します。`+`記号とスペースは含めません。例えば、`70123456789`。 |
| 名 | ユーザーの名前。 |
| 姓 | ユーザーの姓。 |
| 通り | 通り。 |
| 市区町村 | 市区町村。 |
| 地域 | 地域。 |
| 郵便番号 | 任意の整数を受け入れます。 |
| 国 | 任意の文字列を受け入れます。 |
| カスタムクエリパラメータ | 追加のカスタムクエリパラメータ。 |
