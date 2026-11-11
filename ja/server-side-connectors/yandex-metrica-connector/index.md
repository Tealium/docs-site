---
title: Yandex Metricaコネクタ構成ガイド
description: この記事では、Yandex Metricaコネクタの構成方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/yandex-metrica-connector/
---
## API情報

このコネクタは、次のベンダーAPIを使用します。

* API名：Yandex API
* APIバージョン：v1.0
* APIエンドポイント：`https://api-metrika.yandex.net/cdp/api/v1`
* ドキュメント：[Yandex API](https://yandex.com/dev/metrika/doc/api2/concept/about.html)

## バッチ制限
  
このコネクタは、ベンダーへの大量のデータ転送をサポートするため、リクエストをバッチ処理します。詳細については、[バッチアクション](https://docs.tealium.com/batched-actions/)を参照してください。次のいずれかのしきい値に達するか、プロファイルがパブリッシュされるまで、リクエストはキューに格納されます。

* リクエストの最大数：100,000
* 最も古いリクエストからの最大経過時間：5分
* リクエストの最大サイズ：2 MB

## アクション

| アクション名 | 訪問プロファイル | イベントデータ |
| --- | :---: | :---: |
| 注文イベントを送信 | ✗ | ✓ |
| 注文イベントを一括送信 | ✗ | ✓ |
| 連絡先をアップサート | ✓ | ✓ |
| 連絡先を一括アップサート | ✗ | ✓ |
| ページビューイベントを送信 | ✗ | ✓ |
| ゴールイベントを送信 | ✓ | ✓ |
| Eコマースイベントを送信 | ✗ | ✓ |
| 高度なマッチングイベントを送信 | ✓ | ✓ |

## 構成

コネクタマーケットプレイスに移動し、新しいコネクタを追加します。詳細については、[about-connectors](https://docs.tealium.com/about-connectors/)を参照してください。

コネクタを追加した後、次の構成を行います。

* **ベアラートークン**：
   * [Yandex OAuthサービス](https://oauth.yandex.ru/authorize?response_type=token&client_id=2d25c09a45cc4c7090d6edbb318e65f0)を使用してYandexアプリへのアクセス権をTealiumに付与し、ベアラートークンを生成します。
   * Yandexアプリでアクセス権を付与すると、トークンをコピーできるページにリダイレクトされます。
   * トークンをYandex Metricaコネクタに貼り付けます。
   * トークンの有効期間は1年間です。
* **カウンターID**：
    構成に使用するカウンターIDです。

コネクタを構成した後、**完了**をクリックします。

## アクション

次のセクションでは、各アクションでサポートされるパラメータを示します。

### 注文イベントを送信

#### パラメータ

| **パラメータ** | **説明** |
| --- | --- |
| 更新タイプ | <ul><li>保存 - 以前に送信されたすべての情報を新しい情報で完全に置き換えます。</li><li>更新 - 現在読み込んでいる情報のみを更新します。</li><li>追加 - 以前にダウンロードしたデータに新しい情報を追加します。</li></ul> |
| ID | <ul><li>（必須）注文ID。</li></ul> |
| クライアント固有ID | <ul><li>（必須）注文に関連付けられているCRM内の顧客ID。</li></ul> |
| 作成日時 | <ul><li>（必須）カウンターのタイムゾーンにおける注文の作成日時。この値は変更できません。</li><li>詳細については、[日付と時刻の形式](https://yandex.ru/dev/metrika/doc/api2/crm/date.html#orders)を参照してください。</li></ul> |
| 注文ステータス | <ul><li>（必須）注文ステータスID。</li><li>任意の文字列。</li><li>ステータスは変更できます。</li><li>詳細については、[注文ステータスの比較](https://yandex.ru/dev/metrika/doc/api2/crm/schema/maporderstatuses.html)を参照してください。</li><li>デフォルトで使用可能な値：**PAID**、**IN_PROGRESS**、**CANCELLED**、**SPAM**。</li><li>作成した追加の値も使用できます。</li></ul> |
| 更新日時 | <ul><li>カウンターのタイムゾーンにおける注文の更新日時。</li><li>パラメータを渡さなかった場合、値は自動的に構成されます。</li><li>詳細については、[日付と時刻の形式](https://yandex.ru/dev/metrika/doc/api2/crm/date.html#orders)を参照してください。</li></ul> |
| 完了日時 | <ul><li>カウンターのタイムゾーンにおける注文の完了日時。</li><li>詳細については、[日付と時刻の形式](https://yandex.ru/dev/metrika/doc/api2/crm/date.html#orders)を参照してください。</li></ul> |
| 収益 | <ul><li>収入 - 注文の合計金額。</li><li>10進数 - 注文による売上金額を渡します。</li><li>この値は、[エンドツーエンド分析](https://yandex.ru/dev/metrika/doc/api2/api_v1/presets/preset_crm_orders.html#preset_cdp_orders)レポートで広告チャネルからの収入を表示するために使用されます。</li><li>この値は**収益**指標に表示されます。</li></ul> |
| コスト | <ul><li>原価。</li><li>[エンドツーエンド分析](https://yandex.ru/dev/metrika/doc/api2/api_v1/presets/preset_crm_orders.html#preset_cdp_orders)レポートで利益を考慮するため、注文のコストを渡すことができます。</li><li>利益は次の式で計算されます：`Revenue - Cost`。 |
| 商品ID | <ul><li>（必須）商品識別子とその数量をオブジェクトで渡します。</li><li>商品リストを転送しない場合、Metricaでセグメントを作成するときに識別子を使用できます。</li><li>[商品リストを作成](https://yandex.ru/dev/metrika/doc/api2/crm/schema/createproducts.html)すると、それらのリストのデータをYandex Metricaで使用できるようになります。</li><li>例：`{"Product A" : 173, "Product B" : 146}`。</li></ul> |
| 商品数量 | <ul><li>（必須）商品の数量。</li></ul> |
| 属性値 | <ul><li>カスタマイズし、指定された順序で渡す属性。</li></ul> |

### 注文イベントを一括送信
#### パラメータ

| **パラメータ** | **説明** |
| --- | --- |
| 更新タイプ | <ul><li>Save - 以前に送信されたすべての情報を新しい情報で完全に置き換えます。</li><li>Update - 現在読み込んでいる情報のみを更新します。</li><li>Append - 以前にダウンロードされたデータに新しい情報を追加します。</li></ul> |
| ID | <ul><li>（必須）注文ID。</li></ul> |
| クライアント一意ID | <ul><li>（必須）注文に関連付けられているCRM内の顧客ID。</li></ul> |
| 作成日時 | <ul><li>（必須）カウンターのタイムゾーンにおける注文の作成日時。この値は変更できません。</li><li>詳細については、[日付と時刻の形式](https://yandex.ru/dev/metrika/doc/api2/crm/date.html#orders)を参照してください。</li><li>例：`2023-04-21 10:00:00`。</li></ul> |
| 注文ステータス | <ul><li>（必須）注文ステータスID。</li><li>任意の文字列。</li><li>ステータスは変更できます。</li><li>[idフィールドでステータスをマッピング](https://yandex.ru/dev/metrika/doc/api2/crm/schema/maporderstatuses.html)したときに渡した値を指定します。</li><li>デフォルトで指定可能な値：PAID、IN_PROGRESS、CANCELLED、SPAM。</li><li>ユーザーは追加の値を作成できるため、その他の値も受け入れる必要があります。</li></ul> |
| 更新日時 | <ul><li>カウンターのタイムゾーンにおける注文の更新日時。</li><li>パラメータを渡さなかった場合、値は自動的に構成されます。</li><li>詳細については、[日付と時刻の形式](https://yandex.ru/dev/metrika/doc/api2/crm/date.html#orders)を参照してください。</li></ul> |
| 完了日時 | <ul><li>カウンターのタイムゾーンにおける注文の完了日時。</li><li>詳細については、[日付と時刻の形式](https://yandex.ru/dev/metrika/doc/api2/crm/date.html#orders)を参照してください。</li></ul> |
| 収益 | <ul><li>収入 - 注文の合計金額。</li><li>10進数 - 注文による収益を渡します。</li><li>この値は、[エンドツーエンド分析](https://yandex.ru/dev/metrika/doc/api2/api_v1/presets/preset_crm_orders.html#preset_cdp_orders)レポートで広告チャネルからの収入を表示するために使用されます。</li><li>この値は収益指標に表示されます。</li></ul> |
| コスト | <ul><li>原価。</li><li>[エンドツーエンド分析](https://yandex.ru/dev/metrika/doc/api2/api_v1/presets/preset_crm_orders.html#preset_cdp_orders)レポートで利益を考慮するために、注文のコストを渡すことができます。</li><li>利益は次の式で計算されます：`Revenue - Cost`。</li></ul> |
| 商品ID | <ul><li>（必須）商品識別子とその数量をオブジェクトで渡します。</li><li>商品リストを転送しない場合、Metricaでセグメントを作成するときに識別子を使用できます。</li><li>[商品リストを作成する](https://yandex.ru/dev/metrika/doc/api2/crm/schema/createproducts.html)と、そのリストのデータをYandex Metricaで使用できるようになります。</li><li>例：`{"Product A" : 173, "Product B" : 146}`。</li></ul> |
| 商品数量 | <ul><li>（必須）商品の数量。</li></ul> |
| 属性値 | <ul><li>カスタマイズし、指定された順序で渡す属性。</li></ul> |

### 連絡先のアップサート

#### パラメータ

| **パラメータ** | **説明** |
| --- | --- |
| 更新タイプ | <ul><li>Save - 以前に送信されたすべての情報を新しい情報で完全に置き換えます。</li><li>Update - 現在読み込んでいる情報のみを更新します。</li><li>Append - 以前にダウンロードされたデータに新しい情報を追加します。</li></ul> |
| 一意ID | <ul><li>（必須）カスタムクライアントID。`customer_id`または`tealium_visitor_id`を指定できます。</li></ul> |
| クライアントID | <ul><li>Yandex MetrikaクライアントID（`_ym_uid`）。</li></ul> |
| 名前 | <ul><li>クライアント名。</li><li>姓、名、父称を指定すると、文字列は**John S**という形式に短縮されます。ここで、**S**は省略された姓です。</li></ul> |
| 作成日時 | <ul><li>カウンターのタイムゾーンにおける連絡先の作成日時。</li><li>この値は変更できません。</li><li>詳細については、[日付と時刻の形式](https://yandex.ru/dev/metrika/doc/api2/crm/date.html#orders)を参照してください。</li></ul> |
| 更新日時 | <ul><li>カウンターのタイムゾーンにおける連絡先の更新日時。</li><li>パラメータを渡さなかった場合、値は自動的に構成されます。</li><li>詳細については、[日付と時刻の形式](https://yandex.ru/dev/metrika/doc/api2/crm/date.html#orders)を参照してください。</li></ul> |
| クライアントID | <ul><li>クライアントIDのリスト。</li></ul> |
| メールアドレス | <ul><li>クライアントのメールアドレスのリスト。</li></ul> |
| 電話番号 | <ul><li>クライアントの電話番号のリスト。</li></ul> |
| メールアドレスのMD5 | <ul><li>[MD5形式でハッシュ化された](https://yandex.ru/dev/metrika/doc/api2/practice/crm/hashing.html#hashing)クライアントのメールアドレスのリスト。</li><li>ハッシュ化する前に、テキストを小文字に変換し、先頭と末尾のスペースおよびカンマを削除して、メールアドレスを正規化します。</li><li>Googleドメインのアドレスの場合、ユーザー名からピリオドを削除します。たとえば、`name.example@gmail.com`を`nameexample@gmail.com`に変換します。</li><li>Yandexドメインのアドレスの場合、ユーザー名のピリオドをハイフンに置き換えます。たとえば、`name.example@yandex.ru`を`name-example@yandex.ru`に変換します。</li><li>`@ya.ru`や`@yandex.com`など、複数あるYandexドメインのアドレスは、`@yandex.ru`に統一します。たとえば、`example@@ya.ru`を`example@yandex.ru`に変更します。</li><li>メールアドレスに`name+commercial@example.com`のような`+`記号が含まれている場合は、`+`より前の名前のみを残し、`name@example.com`とします。</li></ul> |
| 電話番号のMD5 | <ul><li>[MD5形式でハッシュ化された](https://yandex.ru/dev/metrika/doc/api2/practice/crm/hashing.html#hashing)顧客の電話番号のリスト。</li><li>`+`記号を除き、国番号を含めた番号を入力します。</li><li>ハッシュ化する前に電話番号を正規化します。</li><li>テキストを小文字に変換します。</li><li>先頭と末尾のスペースおよびカンマを削除します。</li><li>数字のみを使用します。</li><li>例：`70123456789`。</li></ul> |
| 属性値 | <ul><li>カスタマイズし、指定された順序で渡す属性。</li></ul> |

### 連絡先の一括アップサート
#### パラメータ

| **パラメータ** | **説明** |
| --- | --- |
| 更新タイプ | <ul><li>保存 - 以前に送信されたすべての情報を新しい情報で完全に置き換えます。</li><li>更新 - 現在読み込んでいる情報のみを更新します。</li><li>追加 - 以前にダウンロードされたデータに新しい情報を追加します。</li></ul> |
| 一意のID | <ul><li>（必須）カスタムクライアントID。`customer_id` または `tealium_visitor_id` を使用できます。</li></ul> |
| クライアントID | <ul><li>（必須）Yandex MetrikaクライアントID（`_ym_uid`）。</li></ul> |
| 名前 | <ul><li>クライアント名。</li><li>姓、名、父称を指定した場合、文字列は **John S** という形式に短縮されます。ここで、**S** は省略された姓です。</li></ul> |
| 作成日時 | <ul><li>カウンターのタイムゾーンで連絡先が作成された日時。</li><li>この値は変更できません。</li><li>詳細については、[日付と時刻の形式](https://yandex.ru/dev/metrika/doc/api2/crm/date.html#orders)を参照してください。</li></ul> |
| 更新日時 | <ul><li>カウンターのタイムゾーンで連絡先が更新された日時。</li><li>パラメータを渡さない場合、値が自動的に構成されます。</li><li>詳細については、[日付と時刻の形式](https://yandex.ru/dev/metrika/doc/api2/crm/date.html#orders)を参照してください。</li></ul> |
| クライアントID | <ul><li>クライアントIDのリスト。</li></ul> |
| メールアドレス | <ul><li>クライアントのメールアドレスのリスト。</li></ul> |
| 電話番号 | <ul><li>クライアントの電話番号のリスト。</li></ul> |
| メールアドレスのMD5 | <ul><li>[MD5形式でハッシュ化された](https://yandex.ru/dev/metrika/doc/api2/practice/crm/hashing.html#hashing)クライアントのメールアドレスのリスト。</li><li>ハッシュ化する前にメールアドレスを正規化してください。</li><li>テキストを小文字に変換します。</li><li>先頭と末尾のスペースおよびカンマを削除します。</li><li>Googleドメインのアドレスの場合、ユーザー名からピリオドを削除します。たとえば、`name.example@gmail.com` を `nameexample@gmail.com` に変換します。</li><li>Yandexドメインのアドレスの場合、ユーザー名のピリオドをハイフンに置き換えます。たとえば、`name.example@yandex.ru` を `name-example@yandex.ru` に変換します。</li><li>`@ya.ru` や `@yandex.com` など、複数のYandexドメインのアドレスは `@yandex.ru` に統一します。たとえば、`example@@ya.ru` を `example@yandex.ru` に変更します。</li><li>メールアドレスに `name+commercial@example.com` のような `+` 記号が含まれている場合、`+` より前の名前のみを残し、`name@example.com` とします。</li></ul> |
| 電話番号のMD5 | <ul><li>[MD5形式でハッシュ化された](https://yandex.ru/dev/metrika/doc/api2/practice/crm/hashing.html#hashing)顧客の電話番号のリスト。</li><li>`+` 記号を除き、国コードを含めて番号を入力します。</li><li>ハッシュ化する前に電話番号を正規化してください。</li><li>テキストを小文字に変換します。</li><li>先頭と末尾のスペースおよびカンマを削除します。</li><li>数字のみを使用します。</li><li>例：`70123456789`。</li></ul> |
| 属性値 | <ul><li>カスタマイズし、指定された順序で渡す属性。</li></ul> |

### ページビューイベントの送信

#### パラメータ

| **パラメータ** | **説明** |
| --- | --- |
| ページURL | <ul><li>現在のURL</li></ul> |
| YandexクライアントID | <ul><li>（必須）Yandex MetricaクライアントID（`_ym_uid`）。</li></ul> |
| ページ参照元 | <ul><li>参照元URL。空の場合、デフォルトURLは `https://tealium.com` です。</li></ul> |
| サイト情報 | <ul><li>カスタムオブジェクト。</li></ul> |
| カスタムクエリパラメータ | <ul><li>追加のカスタムクエリパラメータ。</li></ul> |

### 新しいセッションの作成

#### パラメータ

| **パラメータ** | **説明** |
| --- | --- |
| ページURL | <ul><li>現在のURL</li></ul> |
| YandexクライアントID | <ul><li>（必須）Yandex MetricaクライアントID（`_ym_uid`）。</li></ul> |
| ページ参照元 | <ul><li>参照元URL。空の場合、デフォルトURLは `https://tealium.com` です。</li></ul> |
| サイト情報 | <ul><li>カスタムオブジェクト。</li></ul> |
| カスタムクエリパラメータ | <ul><li>追加のカスタムクエリパラメータ。</li></ul> |

### ゴールイベントの送信

#### パラメータ

| **パラメータ** | **説明** |
| --- | --- |
| オープンセッション呼び出しのトリガー | <ul><li>Yandex Metricaでは、**ゴールイベントの送信**アクションをトリガーする前にオープンセッション呼び出しが必要です。</li></ul> |
| サイトドメイン | <ul><li>（必須）サイトのドメイン。</li></ul> |
| ゴールID | <ul><li>（必須）ゴール番号。</li></ul> |
| YandexクライアントID | <ul><li>（必須）Yandex MetricaクライアントID（`_ym_uid`）</li></ul> |
| ページ参照元 | <ul><li>参照元URL。空の場合、デフォルトURLは `https://tealium.com` です。</li></ul> |
| サイト情報 | <ul><li>カスタムオブジェクト。</li></ul> |
| カスタムクエリパラメータ | <ul><li>追加のカスタムクエリパラメータ。</li></ul> |

### Eコマースイベントの送信

#### パラメータ

| **パラメータ** | **説明** |
| --- | --- |
| オープンセッション呼び出しのトリガー | <ul><li>Yandex Metricaでは、**Eコマースイベントの送信**アクションをトリガーする前にオープンセッション呼び出しが必要です。</li></ul> |
| ページURL | <ul><li>参照元URL。空の場合、デフォルトURLは `https://tealium.com` です。</li></ul> |
| YandexクライアントID | <ul><li>（必須）Yandex MetricaクライアントID（`_ym_uid`）。</li></ul> |
| アクションタイプ | <ul><li>`actionType` に代わるフィールド名で、商品セットに対して実行されたアクションの識別子として機能します。</li><li>指定可能な値：</li><li>詳細：商品の詳細説明（商品カード）を表示します。</li><li>追加：商品をカートに追加します。</li><li>削除：商品をカートから削除します。</li><li>購入：商品を購入します。</li><li>商品の削除に関する情報がYandex Metricaに送信された場合、レポートに商品の数量が負の値として表示されることがあります（合計は、追加された商品の総数から削除された商品の数を差し引いて計算されます）。商品の価格が送信された場合、レポートで価格も負の値になることがあります。</li></ul> |
| 通貨コード | <ul><li>3文字の[ISO 4217通貨コード](https://www.six-group.com/en/products-services/financial-information/data-standards.html#scrollTo=currency-codes)。</li><li>異なる通貨を渡した場合、通貨と金額の代わりにnull値が送信されます。</li></ul> |
| ID | <ul><li>購入された商品のID。</li></ul> |
| クーポン | <ul><li>購入全体に関連付けられたプロモーションコード。</li></ul> |
| ゴールID | <ul><li>[ゴール](https://yandex.ru/support/metrica/general/goals.html)番号。</li><li>**Eコマースイベントの送信**[アクション](https://yandex.ru/support/metrica/ecommerce/data.html#about__action_type)がゴールである場合に指定します。</li><li>ゴールは[JavaScriptイベント](https://yandex.ru/support/metrica/general/goal-js-event.html)タイプとして構成する必要があります。</li><li>ゴール番号を確認するには、Yandex Metricaダッシュボードで**ゴール**タブに移動し、**構成**を選択します。</li></ul> |
| 収益 | <ul><li>得られた収益。</li><li>省略した場合、購入に関連付けられたすべての商品の価格の合計として自動的に計算されます。</li></ul> |
| ID | <ul><li>商品のID。</li><li>例：SKU。</li><li>**名前**または**ID**のいずれかを指定する必要があります。</li></ul> |
| 名前 | <ul><li>商品の名前。</li><li>例：**Tシャツ**。</li><li>**名前**または**ID**のいずれかを指定する必要があります。</li></ul> |
| ブランド | <ul><li>商品に関連付けられたブランドまたは商標。</li><li>例：**Yandex**。</li></ul> |
| カテゴリ | <ul><li>商品が属するカテゴリ。</li><li>カテゴリ階層では、最大5レベルのネストがサポートされます。レベルを区切るには `/` 記号を使用します。</li><li>例：**衣料品/メンズ**、**衣料品/Tシャツ**。</li></ul> |
| クーポン | <ul><li>商品に関連付けられたプロモーションコード。</li><li>例：`PARTNER_SITE_15.`</li></ul> |
| 位置 | <ul><li>リスト内での商品の位置。</li><li>例：`2`。</li></ul> |
| 価格 | <ul><li>商品1単位あたりの価格。</li></ul> |
| 数量 | <ul><li>商品の数量。</li></ul> |
| バリエーション | <ul><li>商品のバリエーション。</li><li>例：**赤**。</li></ul> |
| カスタムクエリパラメータ | <ul><li>追加のカスタムクエリパラメータ。</li></ul> |

### 高度なマッチングイベントの送信
#### パラメータ

| **パラメータ** | **説明** |
| --- | --- |
| オープンセッション呼び出しをトリガー | Yandex Metrica では、**高度なマッチングイベントを送信**アクションをトリガーする前に、オープンセッション呼び出しが必要です。 |
| ページURL | 参照元URL。空の場合、デフォルトURLは `https://tealium.com` です。 |
| YandexクライアントID | （必須）Yandex MetricaクライアントID（`_ym_uid`）。 |
| MD5ハッシュ化済み | 値がMD5でハッシュ化されている場合に選択します。 |
| メールアドレス | ユーザーのメールアドレス。 |
| 電話番号 | 国番号を含む電話番号を、`+` 記号とスペースを除いて入力します。例：`70123456789`。 |
| 名 | ユーザーの名。 |
| 姓 | ユーザーの姓。 |
| 番地 | 番地。 |
| 市区町村 | 市区町村。 |
| 地域 | 地域。 |
| 郵便番号 | 任意の整数を指定できます。 |
| 国 | 任意の文字列を指定できます。 |
| カスタムクエリパラメータ | 追加のカスタムクエリパラメータ。 |