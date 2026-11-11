---
title: Google SA360 拡張コンバージョンコネクタ構成ガイド
description: この記事では、Google SA360 拡張コンバージョンコネクタの構成方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/google-sa360-enhanced-conversions-connector/
---
Google SA360 拡張コンバージョンコネクタを使用すると、コンバージョン測定の精度を高め、より強力な入札機能を利用できます。ウェブサイトからハッシュ化されたファーストパーティのコンバージョンデータを、プライバシーに配慮した方法で Google に送信することで、既存のクライアント側コンバージョンタグを補完します。

コンバージョンは、クライアント側の [Floodlight（`gtag.js`）タグ](https://docs.tealium.com/floodlight-gtagjs-tag/)を通じて記録され、Google によってインデックス化されます。Google SA360 拡張コンバージョンコネクタでは、サーバー間 API 呼び出しを使用して、個人を特定できる情報（PII）によりこれらのコンバージョンを補完できます。

## 要件

このコネクタには、以下が必要です。

* コネクタ構成で使用するプロファイル ID を取得するには、Google Campaign Manager 360 アカウントに `api@tealium.com` ユーザーを追加します。このユーザーには、オフラインコンバージョンの更新権限が必要です。
* このコネクタでタグのペイロードを PII データにより更新するには、[Floodlight `gtag.js` タグ](https://docs.tealium.com/floodlight-gtagjs-tag/)が必要です。
* Floodlight `gtag.js` タグを最新バージョンに更新します。
* `tealium_random` などの一意の値を含む属性を、タグの `match_id` 変数にマッピングします。Google が補完対象のコンバージョンを識別できるように、コネクタでも同じ値を使用します。
* 購入以外のコンバージョンでは、Floodlight `gtag.js` タグで、一意の値を含む属性を `ordinal` にマッピングします。例：`tealium_random`。

### 権限

* 任意のソース（バルクシート、Search Ads 360 API、Campaign Manager 360 API など）からコンバージョンをアップロードするには、コンバージョンのアップロード先となるサブマネージャーアカウントへの編集アクセス権が必要です。詳細については、[Google：ロールの割り当てによるユーザー権限について](https://support.google.com/searchads/answer/1409946)を参照してください。
* 共有 Floodlight 構成では、コンバージョンをアップロードする各子サブマネージャーアカウントへの編集アクセス権が必要です。親サブマネージャーや、コンバージョンをアップロードしない子サブマネージャーへのアクセス権は必要ありません。詳細については、[Google：Floodlight 構成を編集する](https://support.google.com/sa360/answer/13400844)を参照してください。
* クリック ID を使用してコンバージョンをトラッキングする場合は、そのクリック ID を生成したサブマネージャーへの編集アクセス権が必要です。編集できないサブマネージャーのクリック ID を使用すると、アップロードは失敗します。詳細については、[Google：ダウンロードしたバルクシートを編集する](https://support.google.com/sa360/answer/13607450)を参照してください。

## API 情報

このコネクタでは、以下のベンダー API を使用します。

* API 名：Google Campaign Manager 360 API
* API バージョン：v5
* API エンドポイント：`https://dfareporting.googleapis.com/dfareporting`
* ドキュメント：[Google：Campaign Manager 360 API - 拡張コンバージョン](https://developers.google.com/doubleclick-advertisers/guides/conversions_ec)

## バッチ制限

このコネクタでは、ベンダーへの大量のデータ転送に対応するため、バッチリクエストを使用します。並列処理により、イベントが順不同でベンダーに到達する場合があります。順序が重要な場合は、イベントにシーケンス値を追加してください。詳細については、[バッチアクション](https://docs.tealium.com/batched-actions/)を参照してください。以下のいずれかのしきい値に達するか、プロファイルがパブリッシュされるまで、リクエストはキューに保持されます。

* リクエストの最大数：1000
* 最も古いリクエストからの最大経過時間：60 分
* リクエストの最大サイズ：1 MB

さらに、Google がクライアント側のコンバージョンをインデックス化できるように、コネクタは 2 時間の遅延後にコンバージョンをバッチ送信します。

## Trace

Tealium の [Trace](https://docs.tealium.com/about-trace/) 機能は、構成されたバッチ処理と遅延をバイパスし、リアルタイムのデバッグを可能にします。Google によるクライアント側コンバージョンのインデックス化は即時には行われないため、このコネクタで Trace を使用すると `404 Not Found` エラーが発生します。

## PII マッピングの制限

このコネクタで Floodlight（`gtag.js`）タグを使用する場合は、PII データに関する以下の制限を遵守してください。

* コネクタを動作させるには、PII データを送信する必要があります。Google への接続時にコネクタデータに PII が含まれていない場合、コネクタは PII 欠落エラーを生成し、Google にデータを送信しません。PII データには、以下のうち少なくとも 1 つを含める必要があります。
    * メールアドレス
    * 電話番号
    * すべての住所情報（名、姓、住所、市区町村、都道府県、郵便番号、国コード）
* PII データは、Floodlight（`gtag.js`）タグまたは Google SA360 拡張コンバージョンコネクタのいずれか一方を通じて送信し、両方からは送信しないでください。両方で PII をマッピングすると、コネクタで `conversion already enhanced` エラーが発生します。
* コネクタエラーを回避するため、PII を必須とする条件をイベントフィードまたはイベント仕様に追加して、PII のないコンバージョンを除外することをお勧めします。

## 構成

コネクタマーケットプレイスに移動し、新しいコネクタを追加します。詳細については、[about-connectors](https://docs.tealium.com/about-connectors/)を参照してください。


<blockquote>
このコネクタを追加する際は、ベンダーのデータプラットフォームポリシーに同意する必要があります。
</blockquote>


コネクタを追加した後、以下を構成します。

* **Floodlight プロファイル ID**：Campaign Manager 360 アカウントに `api@tealium.com` ユーザーを追加した後に、Campaign Manager 360 から提供される Floodlight プロファイル ID。

コネクタの構成が完了したら、**完了**をクリックします。

## アクション

| **アクション名** | **訪問プロファイル** | **イベントデータ** |
| --- | --- | --- |
| コンバージョンを送信 | ✓ | ✓ |

**続行**をクリックして、コネクタアクションを構成します。アクションの名前を入力し、アクションタイプを選択します。

以下のセクションでは、各アクションのパラメータとオプションを構成する方法について説明します。

### コンバージョンを送信
#### コンバージョンデータ

必須パラメータ：

| パラメータ | 説明 |
| --- | --- |
| Floodlight Configuration ID | （必須）このコンバージョンの Floodlight 構成 ID。 |
| Floodlight Activity ID | （必須）このコンバージョンの Floodlight アクティビティ ID。 |
| Match ID | （必須）コネクタによる拡張コンバージョン呼び出しとクライアント側の Floodlight イベントを照合するために Google が使用する、広告主が作成した一意のイベント識別子。このコネクタと Floodlight `gtag.js` タグの両方で、同じ属性値を使用します。 |
| Ordinal |（必須）コンバージョンの序数。このパラメータでは、イベントごとに同じ値（例：`1`）を渡すことで、同じユーザーおよび同じ日に発生したコンバージョンの重複を排除できます。重複排除を無効にするには、購入イベントの場合は `order_id`、購入以外のイベントの場合は `tealium_random` など、一意の値を使用します。このコネクタと Floodlight `gtag.js` タグの両方で、同じ属性値を使用します。タグでトランザクション ID を使用している場合は、その値を含む属性をマッピングします。 |
| Timestamp Micros | Unix エポックからの経過時間をマイクロ秒単位で表したコンバージョンのタイムスタンプ。指定しない場合、コネクタが自動的に生成します。Tealium の日付属性（ミリ秒単位で保存）をマッピングすると、コネクタは Google に送信する前に値をマイクロ秒に変換します。この値は、クライアント側コンバージョンについて Google が記録したタイムスタンプの前後 1 分以内にする必要があります。 |
| Quantity | （必須）コンバージョンの数量。配列をマッピングすると、コネクタは配列内の値を合計します。値を更新する場合を除き、このコネクタと Floodlight `gtag.js` タグの両方で同じ属性値を使用します。 |
| Value | （必須）コンバージョンの値。値を更新する場合を除き、このコネクタと Floodlight `gtag.js` タグの両方で同じ属性値を使用します。|
| Profile ID | コネクタの構成タブで定義されている値を上書きします。 |

| パラメータ | 説明 |
| --- | --- |
| Email Address (already SHA256 hashed) | 空白の除去、小文字への変換、および SHA256 ハッシュ化がすでに行われているメールアドレスを指定します。 |
| Email Address (apply SHA256 hash) | プレーンテキストのメールアドレスを指定すると、コネクタが空白を除去し、小文字に変換して、SHA256 でハッシュ化します。 |
| Phone Number (already SHA256 hashed) | 空白の除去および SHA256 ハッシュ化がすでに行われている電話番号を指定します。 |
| Phone Number (apply SHA256 hash) | プレーンテキストの電話番号を指定すると、コネクタが空白を除去し、SHA256 でハッシュ化します。 |
| Address Info: First Name (already SHA256 hashed) | 空白の除去、小文字への変換、および SHA256 ハッシュ化がすでに行われている名を指定します。 |
| Address Info: First Name (apply SHA256 hash) | プレーンテキストの名を指定すると、コネクタが空白を除去し、小文字に変換して、SHA256 でハッシュ化します。 |
| Address Info: Last Name (already SHA256 hashed) | 空白の除去、小文字への変換、および SHA256 ハッシュ化がすでに行われている姓を指定します。 |
| Address Info: Last Name (apply SHA256 hash) | プレーンテキストの姓を指定すると、コネクタが空白を除去し、小文字に変換して、SHA256 でハッシュ化します。 |
| Address Info: Street Address (already SHA256 hashed) | 特殊文字が含まれず、空白の除去、小文字への変換、および SHA256 ハッシュ化がすでに行われている番地を指定します。 |
| Address Info: Street Address (apply SHA256 hash) | プレーンテキストの番地を指定すると、コネクタがすべての特殊文字と空白を除去し、小文字に変換して、SHA256 でハッシュ化します。 |
| Address Info: City | ユーザーの住所の市区町村。 |
| Address Info: State | ユーザーの住所の州コード。 |
| Address Info: Postal Code | ユーザーの住所の郵便番号。 |
| Address Info: Country Code | ISO 3166-1 alpha-2 形式による、ユーザーの住所の 2 文字の国コード。 |

#### カスタム変数

| パラメータ | 説明 |
|---| ---|
|Custom Variable Values|  <ul><li>カスタム値の配列。</li><li>各値は 50 文字以内である必要があります。</li></ul> |
|Custom Variable Types|  <ul><li>「U1」から「U100」までのパターンに一致する文字列の配列。このパターンに一致しない文字列は除外されます。</li></ul> |

## トラブルシューティング

### Google 属性の特定

このコネクタに必要な属性を特定するには、以下の Google SA360 の **アクティビティ**画面の画像を参照してください。

![](https://docs.tealium.com/images/server-side-connectors/google-sa360-ui.png)

この図は、このコネクタと Floodlight（gtag.js）タグに必要な以下の属性の場所を示しています。

| | Google SA360 拡張コンバージョンコネクタ | Floodlight（gtag.js）タグ |
|---|:---:|:---:|
|構成 ID | ✓  | ✓ |
|アクティビティ ID |✓ | |
|アクティビティタグ文字列 | | ✓ | 
|グループタグ文字列  | | ✓ |
|カウント方法| |✓  |

### エラーメッセージ

このコネクタで発生する可能性があるエラーメッセージは次のとおりです。

|エラーメッセージ| 説明|
|---| ---|
| `NOT_FOUND` | 「MatchId `{matchId}` が見つかりません。」Google は、クライアント側タグからの ping に一致するコンバージョンを検出できませんでした。これはコネクタの問題ではありませんが、タグ管理のタグ構成を調査する必要がある可能性があります。また、[Google Consent Mode タグ](https://docs.tealium.com/google-consent-mode-tag/)を使用していて、タグへの同意が拒否された一方で、コンバージョン拡張データがコネクタ経由で送信された場合にも、このエラーが発生する可能性があります。 |
| `NOT_FOUND` | 「指定されたコンバージョンは存在しません。」コンバージョンはクライアント側タグから受信されましたが、拡張処理の対象として Google によるインデックス作成がまだ完了していません。Tealium はこれらの呼び出しを最大 3 回再試行します。|