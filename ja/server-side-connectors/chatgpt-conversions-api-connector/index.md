---
title: OpenAI Eventsコネクタ構成ガイド
description: この記事では、OpenAI Eventsコネクタの構成方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/chatgpt-conversions-api-connector/
---
## API情報

このコネクタは、次のベンダーAPIを使用します。

* API名：OpenAI Events API
* APIバージョン：v1
* APIエンドポイント：`https://bzr.openai.com`

## 構成

コネクタマーケットプレイスに移動し、新しいコネクタを追加します。詳細については、[about-connectors](https://docs.tealium.com/about-connectors/)を参照してください。

コネクタを追加したら、次の構成を構成します。

* **OpenAI Events APIキー**：必須。OpenAI Events APIへのリクエストの認証に使用するBearerトークンです。このキーは、AuthorizationヘッダーでBearerトークンとして送信されます。この値はOpenAIのアカウントチームから提供を受けることができます。
* **ピクセルID**：必須。OpenAIピクセルID（`pid`）です。この値は、クエリパラメータとしてAPIエンドポイントに追加されます。ピクセルIDは、**OpenAI Ads > Settings > Conversions**で確認できます。送信する各コンバージョンイベント（`page_viewed`、`items_added`、`order_created`など）は、ライブイベントがレポートに計上されるようにするため、そのピクセルについて同画面で登録する必要があります。
* **デフォルトのアクションソース**：コンバージョンイベントのデフォルトソースを選択します。デフォルトは**Web**です。アクションソースパラメータを使用すると、アクションごとにこの構成を上書きできます。
* **ベースURLの上書き**：デフォルトは`https://bzr.openai.com`です。サンドボックス環境またはステージング環境向けにOpenAIから指示された場合にのみ上書きしてください。

コネクタを構成したら、**完了**をクリックします。

## コネクタアクション

| アクション名 | 訪問プロファイル | イベントデータ |
| ----------- | :------------: | :---------: |
| イベントを送信（リアルタイム） | ✓ | ✓ |
| イベントを送信（バッチ） | ✓ | ✓ |

### イベントを送信（リアルタイム）

#### パラメータ

**イベントタイプ**

必須。OpenAIに送信するイベントのタイプを選択します。各値は、OpenAI Events APIの`type`フィールドにマッピングされます。サポートされる値は次のとおりです。

* `appointment_scheduled`
* `attribution_appended`
* `checkout_started`
* `contents_viewed`
* `custom`
* `items_added`
* `lead_created`
* `order_created`
* `page_viewed`
* `registration_completed`
* `subscription_created`
* `trial_started`

各イベントタイプは、`contents`、`customer_action`、`plan_enrollment`、`custom`、`attribution`の5つのデータタイプオブジェクトのいずれかにマッピングされます。`attribution_appended`のフィールドについては、[元のイベントデータ](#original-event-data)および[アトリビューションデータ](#attribution-data)を参照してください。

`attribution_appended`は、以前のコンバージョンを参照する個別のアトリビューションレポートを送信します。**イベントデータ**では、**イベントID**がアトリビューションレポートIDです。このIDは一意である必要があり、まったく同じ再試行では再利用する必要があります。**タイムスタンプ**はレポート生成時刻であり、デフォルトは送信時刻です。


<blockquote>
`attribution_appended`は、OpenAIがお客様の広告主ピクセルに対して有効にした後にのみ使用できます。本番環境で使用する前に、OpenAIのアカウントチームに連絡して利用可能かどうかを確認してください。
</blockquote>


**カスタムイベント名**

イベントタイプが**カスタム**の場合は必須です。イベントのカスタム名を指定します。この値は、その他すべてのイベントタイプでは無視されます。

**OPPRef**

任意。OpenAIのアトリビューション識別子です。元の値を変更せずにマッピングしてください。この値は`events[].oppref`として送信され、イベントデータには含まれません。

#### イベントデータ

Tealium属性をOpenAIのトップレベルイベントフィールドにマッピングします。


<blockquote>
**アトリビューション追加**イベントでは、**イベントID**、**タイムスタンプ**、**アクションソース**、**ソースURL**、および**OPPRef**のみが送信されます。**イベントID**はアトリビューションレポートIDです。このIDは一意である必要があり、まったく同じ再試行では再利用する必要があります。**タイムスタンプ**はレポート生成時刻であり、マッピングされていない場合はデフォルトで送信時刻になります。
</blockquote>


| パラメータ | 説明 |
| --- | --- |
| イベントID | 必須。重複排除に使用される、イベントの一意の識別子です。 |
| タイムスタンプ | 必須。ミリ秒単位のイベントタイムスタンプです。過去7日以内、または未来10分以内である必要があります。 |
| ソースURL | アクションソースが`web`の場合は必須です。イベントが発生したページのURLです。 |
| アクションソース | コンバージョンイベントのソースです。サポートされる値：`web`、`mobile_app`、`offline`、`physical_store`、`phone_call`、`email`、`other`。 |
| オプトアウト | イベントがパーソナライゼーションをオプトアウトしていることを示すには、`true`に構成します。 |

#### ユーザーデータ


<blockquote>
ユーザーデータは、**アトリビューション追加**イベントでは送信されません。
</blockquote>


* アトリビューションの精度を高めるため、該当するユーザー識別子をマッピングします。各PIIフィールドについて、値を事前にハッシュ化するか、コネクタでハッシュ化するかを選択できます。
* ハッシュ化可能なフィールドには、コネクタで正規化およびハッシュ化する未加工値用の列（SHA256ハッシュを適用）と、すでにハッシュ化済みの値用の列（SHA256ハッシュ化済み）があります。
* サポートされるPIIキー（ハッシュ化必須）：`email_address`、`phone_number`、`external_id`、`country`、`city`、`zip_code`。
* ハッシュ化せずに送信されるフィールド：`ip_address`、`user_agent`。

| パラメータ | 説明 |
| --- | --- |
| メールアドレス（SHA256ハッシュを適用） | 小文字のプレーンテキスト形式のメールアドレスを指定すると、コネクタがOpenAIで想定される形式にこの値をハッシュ化します。空またはnullの値は無視されます。 |
| メールアドレス（SHA256ハッシュ化済み） | SHA256でハッシュ化されたメールアドレスを指定します。 |
| 電話番号（SHA256ハッシュを適用） | 小文字のプレーンテキスト形式の電話番号を指定すると、コネクタがOpenAIで想定される形式にこの値をハッシュ化します。空またはnullの値は無視されます。 |
| 電話番号（SHA256ハッシュ化済み） | SHA256でハッシュ化された電話番号を指定します。 |
| 外部ID（SHA256ハッシュを適用） | ロイヤルティカードIDやその他の識別子など、プレーンテキスト形式の外部IDを指定すると、コネクタがOpenAIで想定される形式にこの値をハッシュ化します。 |
| 外部ID（SHA256ハッシュ化済み） | SHA256でハッシュ化された外部IDを指定します。 |
| 国（SHA256ハッシュを適用） | イベントに関連付けられた国を指定すると、コネクタがOpenAIで想定される形式にこの値をハッシュ化します。 |
| 国（SHA256ハッシュ化済み） | SHA256でハッシュ化された国の値を指定します。 |
| 市区町村（SHA256ハッシュを適用） | コンバージョンに関連付けられた市区町村を小文字で指定すると、コネクタがOpenAIで想定される形式にこの値をハッシュ化します。 |
| 市区町村（SHA256ハッシュ化済み） | SHA256でハッシュ化された市区町村の値を指定します。 |
| 郵便番号（SHA256ハッシュを適用） | 郵便番号を小文字で指定すると、コネクタがOpenAIで想定される形式にこの値をハッシュ化します。 |
| 郵便番号（SHA256ハッシュ化済み） | SHA256でハッシュ化された郵便番号を指定します。 |
| 外部ID（未加工） | ロイヤルティカードIDやその他の識別子などの一意のIDです。コネクタは送信前にこの値をSHA256でハッシュ化します。 |
| IPアドレス | デバイスのIPアドレスです。 |
| ユーザーエージェント | ユーザーのWebブラウザーのユーザーエージェント文字列です。 |

#### 元のイベントデータ

これらのフィールドは、**イベントタイプ**が`attribution_appended`に構成されている場合にのみ適用されます。このアトリビューションレポートが参照する元のコンバージョンイベントにマッピングしてください。

| パラメータ | 説明 |
| --- | --- |
| イベントID | 必須。元のコンバージョンイベントの`event_id`です。この値を正確にコピーしてください。再生成しないでください。 |
| イベントタイプ | 必須。元のコンバージョンイベントの`type`値です。サポートされる値：`app_installed`、`app_opened`、`appointment_scheduled`、`checkout_started`、`contents_viewed`、`custom`、`items_added`、`lead_created`、`order_created`、`page_viewed`、`registration_completed`、`subscription_created`、`trial_started`。 |
| タイムスタンプ（ミリ秒） | 必須。Unixミリ秒単位の元のコンバージョンイベントのタイムスタンプです。7日より前の値も使用できます。 |
| カスタムイベント名 | 元のイベントタイプが`custom`の場合は必須です。その他すべてのイベントタイプでは省略してください。 |
| 注文ID | 任意。元の注文に対するメタデータ参照です。**イベントID**の代わりにはなりません。 |
#### アトリビューションデータ

これらのフィールドは、**Event Type** が `attribution_appended` に構成されている場合にのみ適用されます。元のコンバージョンへの貢献が認められた OpenAI 広告のタッチポイントを記述するものであり、Tealium によって自動マッピングまたは生成されることはありません。

必須のアトリビューションフィールドが欠けている場合、コネクタはイベントを送信しません。検証エラーが Trace とコネクタログに表示されます。

| パラメータ | 説明 |
| --- | --- |
| Ad ID | 必須。貢献が認められる OpenAI 広告（`ad_id`）。 |
| Touchpoint Timestamp (ms) | 必須。広告タッチポイントのタイムスタンプ（Unix ミリ秒）。7 日より前の値も指定できます。 |
| Touchpoint Type | 必須。タッチポイントのタイプ（例：`ad_click`）。 |
| Attribution Share | 必須。0 以上 1 以下の数値。 |
| Attributed Amount | 必須。通貨の補助単位で表した整数（例：`6500` = $65.00）。 |
| Attribution Model | 必須。サポートされる値：`customized_multi_touch`、`data_driven`、`first_click`、`first_touch`、`last_click`、`last_touch`、`linear`、`position_based`、`time_decay`。 |
| Total Credit | 任意。貢献度の合計値を表す数値。 |
| Attribution Window (days) | 任意。アトリビューション期間の日数を表す負でない整数。 |

#### E コマース

Customer Action イベント（**Appointment Scheduled**、**Lead Created**、**Registration Completed**）では、注文概要フィールドのみが受け付けられます。OpenAI は、その他すべての E コマースフィールドを送信ペイロードから除外します。

**Attribution Appended** イベントでは、**Currency**、**Amount**、**Amount - convert to minor units**、**Minor Unit Factor**、**Data Content Type**、**Customer Segmentation** のみが受け付けられます。E コマースの自動マッピングは適用されません。

金額には次の 2 つの指定方法があります。

* **変換済みの値**：補助単位ですでに表されている値（例：29.90 USD の場合は `2990`）を、**Amount** または **Content Amount (per unit)** にマッピングします。
* **送信時に変換**：主要単位の小数値（例：`29.90`）を **Amount - convert to minor units** または **Content Amount (per unit) - convert to minor units** にマッピングし、**Minor Unit Factor** に通貨に適した乗数を構成します（例：USD/EUR/GBP は `100`、JPY/KRW は `1`、KWD/BHD/OMR は `1000`）。

同じフィールドに両方の形式がマッピングされている場合は、変換済みの値が優先されます。

| パラメータ | 説明 |
| --- | --- |
| Amount | 補助単位ですでに表されている整数（例：29.90 USD の場合は `2990`）。指定する場合は Currency が必須です。Attribution Appended イベントでは、元のコンバージョン値になります。**Amount** と **Amount - convert to minor units** の両方がマッピングされている場合は、この値が優先されます。 |
| Amount - convert to minor units | 主要単位の小数値（例：`29.90`）。コネクタはこの値に **Minor Unit Factor** を乗算し、その結果を四捨五入して整数にしてから送信します。指定する場合は Currency が必須です。係数が構成されていない場合、コネクタは乗算せずに値を最も近い整数に丸めます。 |
| Minor Unit Factor | 補助単位への変換形式を使用するときに適用する乗数。USD、EUR、GBP には `100`、JPY、KRW には `1`、KWD、BHD、OMR には `1000` を使用します。正の数である必要があります。この値は OpenAI には送信されません。 |
| Currency | **Amount** または **Amount - convert to minor units** を指定する場合は必須です。Attribution Appended イベントでも必須です。ISO 4217 形式の通貨コード（例：`USD`）。 |
| Content Amount (per unit) | 補助単位ですでに表されている整数。明細項目のコンテンツごとの単価です。**Content Amount (per unit)** と **Content Amount (per unit) - convert to minor units** の両方がマッピングされている場合は、この値が優先されます。 |
| Content Amount (per unit) - convert to minor units | 項目ごとの主要単位の小数価格。コネクタはこの値に **Minor Unit Factor** を乗算し、その結果を四捨五入して整数にしてから送信します。係数が構成されていない場合、コネクタは乗算せずに値を最も近い整数に丸めます。 |
| Data Content Type | Attribution Appended イベントのみ。任意。 |
| Customer Segmentation | Attribution Appended イベントのみ。任意。 |

#### E コマースの自動マッピングを無効化

* オンにすると、このアクションに対する Tealium から OpenAI へのデフォルトの E コマース自動マッピングが無効になります。対象は、`timestamp_ms`（Tealium のイベント時刻から取得）、`source_url`（標準 URL 属性から取得）、およびリテール拡張属性 `_csubtotal`、`_ccurrency`、`_csku`、`_cprodname`、`_ccat`、`_cquan`、`_cprice` です。
* 明示的なフィールドマッピングが常に優先されます。オフにした場合は、空のフィールドのみが補完されます。
* **Minor Unit Factor** がマッピングされている場合、コネクタは自動マッピングされた `_csubtotal` と `_cprice` の値にも係数を乗算してから送信します。
* ID の自動マッピング（IP Address と User Agent）は、**Disable Identity Automapping** チェックボックスによって個別に制御されます。


<blockquote>
以前の **Disable Automapping** チェックボックスを有効にして、IP アドレスとユーザーエージェントが自動マッピングされないようにしていた場合は、**Disable Identity Automapping** も有効にする必要があります。以前のチェックボックスは、現在では E コマースフィールドの自動マッピングのみを制御します。
</blockquote>


#### ID の自動マッピングを無効化

* オンにすると、コネクタは IP Address と User Agent を自動的にマッピングしません。ID メタデータを完全に手動で管理する場合や、プライバシー上の理由からこれらのフィールドを除外する必要がある場合に使用します。
* オフ（デフォルト）の場合、コネクタは `ip_address`（Tealium の標準 IP 属性から取得）と `user_agent`（Tealium の標準 User Agent 属性から取得）を自動的にマッピングします。

#### デバッグモード

有効にすると、コネクタは `validate_only: true` を指定してイベントを送信します。これにより、OpenAI はイベントを保存せずにペイロードを検証し、エラーがあれば返します。トラブルシューティングやドライランに使用してください。本番トラフィックでは無効のままにしてください。

#### Pixel ID の上書き

任意。このアクションについて、コネクタレベルの Pixel ID を上書きします。指定した場合、コネクタはコネクタ構成で構成された Pixel ID の代わりにこの値を使用します。

#### API キーの上書き

任意。このアクションについて、コネクタレベルの API Key を上書きします。指定した場合、コネクタはコネクタ構成で構成された API Key の代わりにこの値を使用します。

### イベントの送信（バッチ）

#### バッチ制限

このアクションでは、ベンダーへの大量のデータ転送をサポートするためにバッチリクエストを使用します。並列処理により、イベントが順不同でベンダーに到達する場合があります。順序が重要な場合は、イベントにシーケンス値を追加してください。詳細については、[バッチアクション](https://docs.tealium.com/batched-actions/)を参照してください。次のいずれかのしきい値に達するか、プロファイルがパブリッシュされるまで、リクエストはキューに保持されます。

* リクエストの最大数：1,000
* 最も古いリクエストからの最大経過時間：5 分
* リクエストの最大サイズ：1 MB

このアクションでは、**Send Event (Real-Time)** アクションと同じパラメータおよびマッピングオプションを使用します。詳細については、[イベントの送信（リアルタイム）](#send-event-real-time)を参照してください。


<blockquote>
`attribution_appended` イベントタイプのバッチ配信は、まだサポートされていません。アトリビューションイベントには **Send Event (Real-Time)** アクションを使用してください。
</blockquote>
