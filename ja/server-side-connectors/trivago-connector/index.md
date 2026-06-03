---
title: Trivagoコネクタ構成ガイド
description: この記事では、Trivagoコネクタの構成方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/trivago-connector/
---
## API情報

このコネクタは、以下のベンダーAPIを使用します：

* API名：Trivago API
* APIエンドポイント：`https://secde.trivago.com/`
* ドキュメンテーション：[Trivago API](https://developer.trivago.com/conversiontracking/conversion-api.html)

## 構成

コネクタマーケットプレイスに移動し、新しいコネクタを追加します。コネクタの追加方法の一般的な指示については、[About Connectors]()を参照してください。

コネクタを追加した後、以下の構成を行います：
* **X-Trv-Ana-Key**  
  *   ユニバーサルにユニークな識別子。詳細については、Trivagoのテクニカルアカウントマネージャーにお問い合わせください。

## アクション

| アクション名 | AudienceStream | EventStream |
| --- | :---: | :---: |
| 予約確認の送信 | ✗ | ✓ |
| 予約確認の更新 | ✗ | ✓ |
| 予約確認の削除 | ✗ | ✓ |

アクションの名前を入力し、ドロップダウンメニューからアクションタイプを選択します。

次のセクションでは、各アクションのパラメータとオプションの構成方法について説明します。

### 予約確認の送信

#### パラメータ

必須パラメータ：

| **パラメータ** | **説明** |
| --- | --- |
| TRV Reference | URLの末尾で提供されるユニークなトラッキングパラメータ。 |
| Advertiser ID | Trivagoから広告主に通知される広告主のユニークなID。この値は、一つの広告主に対して常に同じです。 |
| Hotel | 予約されたホテルの広告主のユニークなホテルID。インベントリフィードで使用されるIDと同一でなければなりません。 |
| Arrival | 到着日（UNIXタイムスタンプ）。 |
| Departure | 出発日（UNIXタイムスタンプ）。 |
| Booking Date | 予約提出日（UNIXタイムスタンプ）。 |
| Volume | ステイごとの総予約価格（全ての部屋、全ての夜を含む）。総価格は、ネットレートプラス予約手数料、プラスVATです。 |
| Currency | `ISO 4217`コードの通貨。 |
| Booking ID | 広告主の予約参照。 |
| Locale | ユーザーが広告主のサイトにリダイレクトされる前にクリックしたTrivago `POS`を含みます。詳細については、[Trivago &gt; Supported locales and languages](https://developer.trivago.com/fastconnect/supported-locales.html)を参照してください。識別子をURLに追加する必要がある場合は、テクニカルアカウントマネージャーにお問い合わせください。 |
| Number of Rooms | 同じ**Booking ID**で予約された部屋の総数。 |
| Date Format | 到着日と出発日をUNIXタイムスタンプ形式で提供できない場合に必要です。例：`20181025`はYYYYMMDD形式です。推奨される形式はYYYYMMDDですが、[accepted formats](https://developer.trivago.com/conversiontracking/conversion-api.html#dateformat)に従ってセパレータを必要に応じて調整できます。可能な場合は、日付をUTC形式で共有する必要があります。それ以外の場合は、UTCベースのタイムスタンプを**Booking Date**と**Booking Date Format**の両方に含める必要があります。例：`booking_date_format`:&#34;YmdHisP&#34;, `booking_date`:&#34;`20200929123015&#43;07:00`&#34;。 |
| Booking Date Format | **Booking Date**をUNIXタイムスタンプ形式で提供できない場合に必要です。予約の時間（秒）も必要です。例：`20201025173002`。推奨される形式はYmdHisですが、[accepted formats](https://developer.trivago.com/conversiontracking/conversion-api.html#dateformat)に従ってセパレータを必要に応じて調整できます。可能な場合は、日付をUTC形式で共有する必要があります。それ以外の場合は、UTCベースのタイムスタンプを**Booking Date**と**Booking Date Format**の両方に含める必要があります。例：`booking_date_format`:&#34;YmdHisP&#34;, `booking_date`:&#34;`20200929123015&#43;07:00`&#34;。 |
| Margin | 予約金額の一部として受け取る手数料の割合。例：`15.8`。 |
| Margin Absolute | マージンをパーセンテージで提供できない場合、絶対値として提供することもできます（例：`60.30 USD`）。**Margin Absolute**の通貨は、ボリュームの通貨と一致している必要があります。 |

### 予約確認の更新

#### パラメータ

必須パラメータ：

| **パラメータ** | **説明** |
| --- | --- |
| TRV Reference | URLの末尾で提供されるユニークなトラッキングパラメータ。 |
| Advertiser ID | Trivagoから広告主に通知される広告主のユニークなID。この値は、一つの広告主に対して常に同じです。 |
| Hotel | 予約されたホテルの広告主のユニークなホテルID。インベントリフィードで使用されるIDと同一でなければなりません。 |
| Arrival | 到着日（UNIXタイムスタンプ）。 |
| Departure | 出発日（UNIXタイムスタンプ）。 |
| Booking Date | 予約提出日（UNIXタイムスタンプ）。 |
| Volume | ステイごとの総予約価格（全ての部屋、全ての夜を含む）。総価格は、ネットレートプラス予約手数料、プラスVATです。 |
| Currency | ISO 4217コードの通貨。 |
| Booking ID | 広告主の予約参照。 |
| Locale | ユーザーが広告主のサイトにリダイレクトされる前にクリックしたTrivago `POS`を含みます。詳細については、[Trivago &gt; Supported locales and languages](https://developer.trivago.com/fastconnect/supported-locales.html)を参照してください。識別子をURLに追加する必要がある場合は、テクニカルアカウントマネージャーにお問い合わせください。 |
| Number of Rooms | 同じ**Booking ID**で予約された部屋の総数。 |
| Date Format | 到着日と出発日をUNIXタイムスタンプ形式で提供できない場合に必要です。これらの日付は別の形式で提供することができます。例：`20181025`はYYYMMDD形式です。推奨される形式はYYMMDDですが、[accepted formats](https://developer.trivago.com/conversiontracking/conversion-api.html#dateformat)に従ってセパレータを必要に応じて調整できます。可能な場合は、日付をUTC形式で共有する必要があります。それ以外の場合は、UTCベースのタイムスタンプを**Booking Date**と**Booking Date Format**の両方に含める必要があります。例：`booking_date_format`:&#34;YmdHisP&#34;, `booking_date`:&#34;`20200929123015&#43;07:00`&#34;。 |
| Booking Date Format | **Booking Date**をUNIXタイムスタンプ形式で提供できない場合に必要です。予約の時間（秒）も必要です。例：`20201025173002`。推奨される形式はYmdHisですが、[accepted formats](https://developer.trivago.com/conversiontracking/conversion-api.html#dateformat)に従ってセパレータを必要に応じて調整できます。可能な場合は、日付をUTC形式で共有する必要があります。それ以外の場合は、UTCベースのタイムスタンプを**Booking Date**と**Booking Date Format**の両方に含める必要があります。例：`booking_date_format`:&#34;YmdHisP&#34;, `booking_date`:&#34;`20200929123015&#43;07:00`&#34;。 |
| Margin | 予約金額の一部として受け取る手数料の割合。例：`15.8`。 |
| Margin Absolute | マージンをパーセンテージで提供できない場合、絶対値として提供することもできます（例：`60.30 USD`）。**Margin Absolute**の通貨は、ボリュームの通貨と一致している必要があります。 |
| Update Date | 予約更新日。 |
| Update Date Format | **Update Date**をUNIXタイムスタンプ形式で提供できない場合に必要です。キャンセルの時間（秒）も必要です（例：`20201025173002`）。推奨される形式はYmdHisですが、[accepted formats](https://developer.trivago.com/conversiontracking/conversion-api.html#dateformat)に従ってセパレータを必要に応じて調整できます。可能な場合は、日付をUTC形式で共有する必要があります。それ以外の場合は、UTCベースのタイムスタンプを**Update Date**と**Update Date Format**の両方に含める必要があります（例：`update_date_format`:&#34;YmdHisP&#34;, `update_date`:&#34;`20200929123015&#43;07:00`&#34;）。 |
| Update Origin | PUTコールがユーザーの更新か広告主の更新に基づいているかを説明します。可能な値は`advertiser`または`user`です。 |

### 予約確認の削除

#### パラメータ
必須パラメータ：

| **パラメータ** | **説明** |
| --- | --- |
| TRV Reference | URLの末尾で提供されるユニークなトラッキングパラメータ。 |
| Advertiser ID | Trivagoが定義し、広告主に通知するTrivago Advertiser ID。この値は、一つの広告主に対して常に同じです。 |
| ホテル | 予約されたホテルの広告主固有のホテルID。在庫フィードで使用されるIDと同一でなければなりません。 |
| 到着 | 到着日（UNIXタイムスタンプ）。 |
| 出発 | 出発日（UNIXタイムスタンプ）。 |
| 予約日 | 予約提出日（UNIXタイムスタンプ）。 |
| ボリューム | 合計の総予約価格（全ての部屋、全ての夜を含む）。総価格は、ネットレートプラス予約料、プラスVATです。 |
| 通貨 | ISO 4217コードの通貨。 |
| 予約ID | 広告主の予約参照。 |
| ロケール | ユーザーが広告主のサイトにリダイレクトされる前にクリックしたTrivagoの`POS`を含みます。詳細は、[Trivago &gt; サポートされるロケールと言語](https://developer.trivago.com/fastconnect/supported-locales.html)を参照してください。URLに識別子を追加する必要がある場合は、テクニカルアカウントマネージャーに連絡してください。 |
| 部屋数 | 同じ**予約ID**で予約された部屋の合計数。 |
| 日付形式 | 到着日と出発日をUNIXタイムスタンプ形式で提供できない場合に必要です。例：`20181025`はYYYYMMDD形式です。推奨される形式はYYYYMMDDですが、[受け入れられる形式](https://developer.trivago.com/conversiontracking/conversion-api.html#dateformat)に従って、セパレータは必要に応じて調整できます。可能な場合は、日付はUTC形式で共有する必要があります。それ以外の場合は、UTCベースのタイムスタンプを**予約日**と**予約日形式**の両方に含める必要があります。例：`booking_date_format`:&#34;YmdHisP&#34;, `booking_date`:&#34;`20200929123015&#43;07:00`&#34;。 |
| 予約日形式 | **予約日**をUNIXタイムスタンプ形式で提供できない場合に必要です。予約の時間（秒）も必要です（例：`20201025173002`）。推奨される形式はYmdHisですが、[受け入れられる形式](https://developer.trivago.com/conversiontracking/conversion-api.html#dateformat)に従って、セパレータは必要に応じて調整できます。可能な場合は、日付はUTC形式で共有する必要があります。それ以外の場合は、UTCベースのタイムスタンプを**予約日**と**予約日形式**の両方に含める必要があります。例：`booking_date_format`:&#34;YmdHisP&#34;, `booking_date`:&#34;`20200929123015`&#43;07:`00`&#34;。 |
| マージン | 予約金額の一部として受け取る手数料の割合。例：`15.8`。 |
| マージン絶対値 | マージンをパーセンテージで提供できない場合、代わりに絶対値として提供できます。例：`60.30 USD`。**マージン絶対値**の通貨は、ボリュームの通貨と一致する必要があります。 |
| 払い戻し額 | 合計払い戻し額（全ての部屋、全ての夜、全ての料金を含む）。このパラメータは、**払い戻し比率**が提供されていても、`DELETE`コールに必要です。 |
| 払い戻し比率 | 払い戻されるボリュームのどのくらいを指定します。4桁の小数点以下で共有する必要があります。例：1.0000 = 100%, 0.0000 = 0.00%, 0.5052 = 50.52%。 |
| キャンセル日 | キャンセル提出日。 |
| キャンセル日形式 | **キャンセル日**をUNIXタイムスタンプ形式で提供できない場合に必要です。キャンセルの時間（秒）も必要です（例：`20201025173002`）。推奨される形式はYmdHisですが、[受け入れられる形式](https://developer.trivago.com/conversiontracking/conversion-api.html#dateformat)に従って、セパレータは必要に応じて調整できます。日付はUTCで共有する必要があります。それが不可能な場合は、UTCベースのタイムスタンプを**キャンセル日**と**キャンセル日形式**の両方に含める必要があります。例：`cancellation_date_format`:&#34;YmdHisP&#34;, `cancellation_date`:&#34;`20200929123015&#43;07:00`&#34;。 |