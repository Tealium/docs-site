---
title: 金融サービスデータレイヤー仕様
description: この記事では、銀行、クレジットカード、ローン、投資プラットフォームなどの金融サービスビジネスのためのデータレイヤー定義を提供します。
url: https://docs.tealium.com/ja/platforms/getting-started-web/data-layer/definitions/financial/
---
## データレイヤー属性


|変数| 説明| 例| タイプ|
|---| ---| ---| ---|
| `account_balance` | 現在の主要なアカウントの残高（数字と小数点のみの文字列） | `1543.27` | 文字列 |
| `account_currency_code` | アカウントの通貨コード | `EUR` | 文字列 |
| `account_id` | アカウントのユニークID | `ACC123456` | 文字列 |
| `account_masked_number` | マスクされたアカウントまたはカード番号 | `•••• •••• •••• 1234` | 文字列 |
| `account_status` | アカウントのステータス | `active` | 文字列 |
| `account_tenure` | アカウントの保有期間（月または年） | `3_years` | 文字列 |
| `account_type` | アカウントのタイプ | `checking` | 文字列 |
| `application_channel` | 製品申し込みが開始されるチャネル | `web` | 文字列 |
| `application_decision` | 申し込みの最終決定 | `approved` | 文字列 |
| `application_id` | 製品申し込みのユニークID | `APP987654` | 文字列 |
| `application_stage` | 申し込みフローの現在のステップ | `document_upload` | 文字列 |
| `application_status` | 申し込みのステータス | `in_review` | 文字列 |
| `customer_city` | 顧客の居住都市 | `Frankfurt` | 文字列 |
| `customer_country` | 顧客の居住国 | `Germany` | 文字列 |
| `customer_email` | 顧客のメールアドレス | `user@example.com` | 文字列 |
| `customer_first_name` | 顧客の名 | `John` | 文字列 |
| `customer_id` | 顧客のユニークID | `CUST8237572` | 文字列 |
| `customer_last_name` | 顧客の姓 | `Smith` | 文字列 |
| `customer_postal_code` | 顧客の郵便番号 | `60311` | 文字列 |
| `customer_segment` | 銀行が定義する顧客セグメント | `premium` | 文字列 |
| `customer_state` | 顧客の居住州/地域 | `HE` | 文字列 |
| `device_type` | サイトまたはアプリへのアクセスに使用されるデバイスタイプ | `mobile` | 文字列 |
| `event_name` | ユニークなイベントを識別するTealium変数 | `application_start` | 文字列 |
| `language_code` | 言語コード | `de` | 文字列 |
| `link_category` | クリック追跡イベント中にクリックされた要素のカテゴリ | `Header` | 文字列 |
| `link_name` | クリック追跡イベント中にクリックされた要素の名前 | `Login` | 文字列 |
| `login_method` | ログインに使用される方法 | `username_password` | 文字列 |
| `page_name` | ページ名を識別するTealium変数 | `Account Overview` | 文字列 |
| `page_type` | ページのタイプ | `account_overview` | 文字列 |
| `product_category` | 上位の金融製品グループ | `lending` | 文字列 |
| `product_id` | 金融製品の内部使用のための製品識別子 | `CC_GOLD_01` | 文字列 |
| `product_name` | 金融製品の表示名 | `Gold Credit Card` | 文字列 |
| `product_subcategory` | 金融製品のより詳細なグループ | `credit_card` | 文字列 |
| `referral_source` | 訪問を紹介したソースまたはパートナー | `partner_portal` | 文字列 |
| `risk_profile` | リスクプロファイルまたは適合性バンド（適用可能かつ遵守される場合） | `balanced` | 文字列 |
| `search_keyword` | サイト内検索で入力されたテキスト値 | `credit card` | 文字列 |
| `search_results` | 検索によって返された結果の数 | `23` | 文字列 |
| `session_id` | 現在のセッションのユニーク識別子 | `8f23c7e9-1234-5678` | 文字列 |
| `site_section` | サイトまたはアプリの上位セクション | `Retail Banking` | 文字列 |
| `transaction_amount` | 取引の金額（数字と小数点のみの文字列） | `250.00` | 文字列 |
| `transaction_category` | 取引のカテゴリ | `transfer` | 文字列 |
| `transaction_currency_code` | 取引の通貨コード | `EUR` | 文字列 |
| `transaction_date` | 取引日（ISO 8601形式） | `2026-02-11` | 文字列 |
| `transaction_id` | 取引のユニークID | `TXN567890` | 文字列 |
| `transaction_method` | 取引に使用される方法 | `wire` | 文字列 |
| `transaction_status` | 取引のステータス | `success` | 文字列 |
| `transaction_type` | 取引のタイプ | `outgoing` | 文字列 |
| `user_auth_state` | ユーザーが認証されているかどうかを示す | `authenticated` | 文字列 |
| `user_login_state` | ユーザーのログイン状態 | `logged_in` | 文字列 |
| `user_role` | ログインしているユーザーの役割（該当する場合） | `primary_holder` | 文字列 |

## 追跡されるページ

### ホームページ

|イベント名|説明| サンプルURL|
|---| ---| ---|
|`page_view`|銀行または金融機関の公開ランディングページ。|`https://www.example.com/`|

サンプル:
```javascript
{
  &#34;country_code&#34;       : &#34;de&#34;,
  &#34;language_code&#34;      : &#34;de&#34;,
  &#34;page_name&#34;          : &#34;Homepage&#34;,
  &#34;page_type&#34;          : &#34;home&#34;,
  &#34;site_section&#34;       : &#34;Public&#34;,
  &#34;user_auth_state&#34;    : &#34;unauthenticated&#34;,
  &#34;tealium_event&#34;      : &#34;page_view&#34;
}
```

### アカウント概要ページ

|イベント名|説明| サンプルURL|
|---| ---| ---|
|`page_view`|認証されたアカウント概要ページで、主要なアカウントと残高が表示されます。|`https://www.example.com/online-banking/accounts/overview`|

サンプル:
```javascript
{
  &#34;country_code&#34;           : &#34;de&#34;,
  &#34;language_code&#34;          : &#34;de&#34;,
  &#34;page_name&#34;              : &#34;Account Overview&#34;,
  &#34;page_type&#34;              : &#34;account_overview&#34;,
  &#34;site_section&#34;           : &#34;Retail Banking&#34;,
  &#34;user_auth_state&#34;        : &#34;authenticated&#34;,
  &#34;customer_id&#34;            : &#34;CUST8237572&#34;,
  &#34;customer_segment&#34;       : &#34;premium&#34;,
  &#34;account_id&#34;             : &#34;ACC123456&#34;,
  &#34;account_type&#34;           : &#34;checking&#34;,
  &#34;account_currency_code&#34;  : &#34;EUR&#34;,
  &#34;account_balance&#34;        : &#34;1543.27&#34;,
  &#34;tealium_event&#34;          : &#34;page_view&#34;
}
```

### アカウント詳細ページ

|イベント名|説明| サンプルURL|
|---| ---| ---|
|`account_view`|特定のアカウント詳細ページで、通常は最近の取引が表示されます。|`https://www.example.com/online-banking/accounts/checking/ACC123456`|

サンプル:
```javascript
{
  &#34;country_code&#34;           : &#34;de&#34;,
  &#34;language_code&#34;          : &#34;de&#34;,
  &#34;page_name&#34;              : &#34;Checking Account Detail&#34;,
  &#34;page_type&#34;              : &#34;account_detail&#34;,
  &#34;site_section&#34;           : &#34;Retail Banking&#34;,
  &#34;user_auth_state&#34;        : &#34;authenticated&#34;,
  &#34;customer_id&#34;            : &#34;CUST8237572&#34;,
  &#34;account_id&#34;             : &#34;ACC123456&#34;,
  &#34;account_type&#34;           : &#34;checking&#34;,
  &#34;account_currency_code&#34;  : &#34;EUR&#34;,
  &#34;account_balance&#34;        : &#34;1543.27&#34;,
  &#34;tealium_event&#34;          : &#34;account_view&#34;
}
```

### 製品リストページ

|イベント名|説明| サンプルURL|
|---| ---| ---|
|`page_view`|製品またはオファーのリストページ（例えば、すべてのクレジットカード）。|`https://www.example.com/products/credit-cards/`|

サンプル:
```javascript
{
  &#34;country_code&#34;      : &#34;de&#34;,
  &#34;language_code&#34;     : &#34;de&#34;,
  &#34;page_name&#34;         : &#34;Credit Cards Overview&#34;,
  &#34;page_type&#34;         : &#34;product_listing&#34;,
  &#34;site_section&#34;      : &#34;Products&#34;,
  &#34;product_category&#34;  : &#34;lending&#34;,
  &#34;product_subcategory&#34;: &#34;credit_card&#34;,
  &#34;tealium_event&#34;     : &#34;page_view&#34;
}
```

### 製品詳細ページ

|イベント名|説明| サンプルURL|
|---| ---| ---|
|`product_view`|金融製品の詳細ページ。|`https://www.example.com/products/credit-cards/gold-card`|

サンプル:
```javascript
{
  &#34;country_code&#34;        : &#34;de&#34;,
  &#34;language_code&#34;       : &#34;de&#34;,
  &#34;page_name&#34;           : &#34;Gold Credit Card&#34;,
  &#34;page_type&#34;           : &#34;product_detail&#34;,
  &#34;site_section&#34;        : &#34;Products&#34;,
  &#34;product_id&#34;          : &#34;CC_GOLD_01&#34;,
  &#34;product_name&#34;        : &#34;Gold Credit Card&#34;,
  &#34;product_category&#34;    : &#34;lending&#34;,
  &#34;product_subcategory&#34; : &#34;credit_card&#34;,
  &#34;tealium_event&#34;       : &#34;product_view&#34;
}
```
### 検索ページ

|イベント名|説明| サンプルURL|
|---| ---| ---|
|`search`|サイト内検索結果ページ。|`https://www.example.com/search?query=credit&#43;card`|

サンプル:
```javascript
{
  &#34;country_code&#34;     : &#34;de&#34;,
  &#34;language_code&#34;    : &#34;de&#34;,
  &#34;page_name&#34;        : &#34;Search Results&#34;,
  &#34;page_type&#34;        : &#34;search&#34;,
  &#34;site_section&#34;     : &#34;Public&#34;,
  &#34;search_keyword&#34;   : &#34;credit card&#34;,
  &#34;search_results&#34;   : &#34;23&#34;,
  &#34;tealium_event&#34;    : &#34;search&#34;
}
```

### ログインページ

|イベント名|説明| サンプルURL|
|---| ---| ---|
|`page_view`|オンラインバンキングのログインページ。|`https://www.example.com/online-banking/login`|

サンプル:
```javascript
{
  &#34;country_code&#34;     : &#34;de&#34;,
  &#34;language_code&#34;    : &#34;de&#34;,
  &#34;page_name&#34;        : &#34;Online Banking Login&#34;,
  &#34;page_type&#34;        : &#34;login&#34;,
  &#34;site_section&#34;     : &#34;Retail Banking&#34;,
  &#34;user_auth_state&#34;  : &#34;unauthenticated&#34;,
  &#34;tealium_event&#34;    : &#34;page_view&#34;
}
```

### アプリケーションフローページ

|イベント名|説明| サンプルURL|
|---|---| ---|
|`application_view`|製品申請プロセスのステップ（例：個人情報画面の表示）。|`https://www.example.com/apply/credit-card/personal-details`|

サンプル:
```javascript
{
  &#34;country_code&#34;        : &#34;de&#34;,
  &#34;language_code&#34;       : &#34;de&#34;,
  &#34;page_name&#34;           : &#34;Credit Card Application - Personal Details&#34;,
  &#34;page_type&#34;           : &#34;application&#34;,
  &#34;site_section&#34;        : &#34;Applications&#34;,
  &#34;product_id&#34;          : &#34;CC_GOLD_01&#34;,
  &#34;product_name&#34;        : &#34;Gold Credit Card&#34;,
  &#34;product_category&#34;    : &#34;lending&#34;,
  &#34;product_subcategory&#34; : &#34;credit_card&#34;,
  &#34;application_id&#34;      : &#34;APP987654&#34;,
  &#34;application_stage&#34;   : &#34;personal_details&#34;,
  &#34;application_status&#34;  : &#34;in_progress&#34;,
  &#34;tealium_event&#34;       : &#34;application_view&#34;
}
```

### アプリケーション完了ページ

|イベント名|説明| サンプルURL|
|---|---| ---|
|`application_complete`|アプリケーション確認ページ（例：承認または提出受領）。|`https://www.example.com/apply/credit-card/confirmation`|

サンプル:
```javascript
{
  &#34;country_code&#34;        : &#34;de&#34;,
  &#34;language_code&#34;       : &#34;de&#34;,
  &#34;page_name&#34;           : &#34;Credit Card Application - Confirmation&#34;,
  &#34;page_type&#34;           : &#34;application_confirmation&#34;,
  &#34;site_section&#34;        : &#34;Applications&#34;,
  &#34;product_id&#34;          : &#34;CC_GOLD_01&#34;,
  &#34;product_name&#34;        : &#34;Gold Credit Card&#34;,
  &#34;application_id&#34;      : &#34;APP987654&#34;,
  &#34;application_stage&#34;   : &#34;confirmation&#34;,
  &#34;application_status&#34;  : &#34;completed&#34;,
  &#34;application_decision&#34;: &#34;approved&#34;,
  &#34;tealium_event&#34;       : &#34;application_complete&#34;
}
```

### プロファイル／構成ページ

|イベント名|説明| サンプルURL|
|---| ---| ---|
|`page_view`|ユーザープロファイルまたは構成ページ（例：連絡先詳細、セキュリティ構成）。|`https://www.example.com/online-banking/profile`|

サンプル:
```javascript
{
  &#34;country_code&#34;      : &#34;de&#34;,
  &#34;language_code&#34;     : &#34;de&#34;,
  &#34;page_name&#34;         : &#34;Profile Settings&#34;,
  &#34;page_type&#34;         : &#34;account&#34;,
  &#34;site_section&#34;      : &#34;Profile&#34;,
  &#34;user_auth_state&#34;   : &#34;authenticated&#34;,
  &#34;customer_id&#34;       : &#34;CUST8237572&#34;,
  &#34;tealium_event&#34;     : &#34;page_view&#34;
}
```

## 追跡イベント

### ログイン成功

|イベント名|説明|
|---|---|
|`login_success`|認証に成功した際。|

サンプル:
```javascript
{
  &#34;customer_id&#34;      : &#34;CUST8237572&#34;,
  &#34;user_auth_state&#34;  : &#34;authenticated&#34;,
  &#34;login_method&#34;     : &#34;username_password&#34;,
  &#34;device_type&#34;      : &#34;mobile&#34;,
  &#34;tealium_event&#34;    : &#34;login_success&#34;
}
```

### ログイン失敗

|イベント名|説明|
|---|---|
|`login_failure`|ログイン試行に失敗した際（機密情報はキャプチャされません）。|

サンプル:
```javascript
{
  &#34;user_auth_state&#34;  : &#34;unauthenticated&#34;,
  &#34;login_method&#34;     : &#34;username_password&#34;,
  &#34;device_type&#34;      : &#34;desktop&#34;,
  &#34;tealium_event&#34;    : &#34;login_failure&#34;
}
```

### トランザクション開始

|イベント名|説明|
|---|---|
|`transaction_initiated`|ユーザーがトランザクションの詳細を提出し始めた際（例：振込、支払い）。|

サンプル:
```javascript
{
  &#34;customer_id&#34;               : &#34;CUST8237572&#34;,
  &#34;account_id&#34;                : &#34;ACC123456&#34;,
  &#34;transaction_id&#34;            : &#34;TXN567890&#34;,
  &#34;transaction_type&#34;          : &#34;outgoing&#34;,
  &#34;transaction_category&#34;      : &#34;transfer&#34;,
  &#34;transaction_currency_code&#34; : &#34;EUR&#34;,
  &#34;transaction_amount&#34;        : &#34;250.00&#34;,
  &#34;transaction_status&#34;        : &#34;initiated&#34;,
  &#34;tealium_event&#34;             : &#34;transaction_initiated&#34;
}
```

### トランザクション成功

|イベント名|説明|
|---|---|
|`transaction_success`|トランザクションが成功裏に完了した際。|

サンプル:
```javascript
{
  &#34;customer_id&#34;               : &#34;CUST8237572&#34;,
  &#34;account_id&#34;                : &#34;ACC123456&#34;,
  &#34;transaction_id&#34;            : &#34;TXN567890&#34;,
  &#34;transaction_type&#34;          : &#34;outgoing&#34;,
  &#34;transaction_category&#34;      : &#34;transfer&#34;,
  &#34;transaction_currency_code&#34; : &#34;EUR&#34;,
  &#34;transaction_amount&#34;        : &#34;250.00&#34;,
  &#34;transaction_status&#34;        : &#34;success&#34;,
  &#34;tealium_event&#34;             : &#34;transaction_success&#34;
}
```

### トランザクション失敗

|イベント名|説明|
|---|---|
|`transaction_failure`|トランザクションが失敗した際（例：残高不足、技術的エラー）。|

サンプル:
```javascript
{
  &#34;customer_id&#34;               : &#34;CUST8237572&#34;,
  &#34;account_id&#34;                : &#34;ACC123456&#34;,
  &#34;transaction_id&#34;            : &#34;TXN567890&#34;,
  &#34;transaction_type&#34;          : &#34;outgoing&#34;,
  &#34;transaction_category&#34;      : &#34;transfer&#34;,
  &#34;transaction_currency_code&#34; : &#34;EUR&#34;,
  &#34;transaction_amount&#34;        : &#34;250.00&#34;,
  &#34;transaction_status&#34;        : &#34;failed&#34;,
  &#34;tealium_event&#34;             : &#34;transaction_failure&#34;
}
```

### アプリケーション開始

|イベント名|説明|
|---|---|
|`application_start`|ユーザーが新しい製品申請を開始した際。|

サンプル:
```javascript
{
  &#34;customer_id&#34;         : &#34;CUST8237572&#34;,
  &#34;product_id&#34;          : &#34;CC_GOLD_01&#34;,
  &#34;product_name&#34;        : &#34;Gold Credit Card&#34;,
  &#34;product_category&#34;    : &#34;lending&#34;,
  &#34;product_subcategory&#34; : &#34;credit_card&#34;,
  &#34;application_id&#34;      : &#34;APP987654&#34;,
  &#34;application_channel&#34; : &#34;web&#34;,
  &#34;application_stage&#34;   : &#34;start&#34;,
  &#34;application_status&#34;  : &#34;in_progress&#34;,
  &#34;tealium_event&#34;       : &#34;application_start&#34;
}
```

### アプリケーションステップ

|イベント名|説明|
|---|---|
|`application_step`|アプリケーションフローの各中間ステップで。|

サンプル:
```javascript
{
  &#34;customer_id&#34;         : &#34;CUST8237572&#34;,
  &#34;product_id&#34;          : &#34;CC_GOLD_01&#34;,
  &#34;application_id&#34;      : &#34;APP987654&#34;,
  &#34;application_stage&#34;   : &#34;income_details&#34;,
  &#34;application_status&#34;  : &#34;in_progress&#34;,
  &#34;tealium_event&#34;       : &#34;application_step&#34;
}
```

### アプリケーション結果

|イベント名|説明|
|---|---|
|`application_outcome`|アプリケーションが決定を受けた際。|

サンプル:
```javascript
{
  &#34;customer_id&#34;          : &#34;CUST8237572&#34;,
  &#34;product_id&#34;           : &#34;CC_GOLD_01&#34;,
  &#34;application_id&#34;       : &#34;APP987654&#34;,
  &#34;application_stage&#34;    : &#34;decision&#34;,
  &#34;application_status&#34;   : &#34;completed&#34;,
  &#34;application_decision&#34; : &#34;approved&#34;,
  &#34;tealium_event&#34;        : &#34;application_outcome&#34;
}
```

### ユーザー登録

|イベント名|説明|
|---|---|
|`user_register`|新しいユーザー登録が成功した際。|

サンプル:
```javascript
{
  &#34;customer_city&#34;        : &#34;Frankfurt&#34;,
  &#34;customer_country&#34;     : &#34;Germany&#34;,
  &#34;customer_email&#34;       : &#34;john.smith@example.com&#34;,
  &#34;customer_first_name&#34;  : &#34;John&#34;,
  &#34;customer_id&#34;          : &#34;CUST8237572&#34;,
  &#34;customer_last_name&#34;   : &#34;Smith&#34;,
  &#34;customer_postal_code&#34; : &#34;60311&#34;,
  &#34;customer_state&#34;       : &#34;HE&#34;,
  &#34;tealium_event&#34;        : &#34;user_register&#34;
}
```

### ユーザープロファイル更新

|イベント名|説明|
|---|---|
|`user_update`|プロファイル情報の更新が成功した際。|

サンプル:
```javascript
{
  &#34;customer_city&#34;        : &#34;Frankfurt&#34;,
  &#34;customer_country&#34;     : &#34;Germany&#34;,
  &#34;customer_email&#34;       : &#34;john.smith@example.com&#34;,
  &#34;customer_first_name&#34;  : &#34;John&#34;,
  &#34;customer_id&#34;          : &#34;CUST8237572&#34;,
  &#34;customer_last_name&#34;   : &#34;Smith&#34;,
  &#34;customer_postal_code&#34; : &#34;60311&#34;,
  &#34;customer_state&#34;       : &#34;HE&#34;,
  &#34;tealium_event&#34;        : &#34;user_update&#34;
}
```
### メールサインアップ

|イベント名|説明|
|---|---|
|`email_signup`|ニュースレターや製品更新のためのサインアップが成功した時。|

サンプル:
```javascript
{
  &#34;customer_email&#34; : &#34;john.smith@example.com&#34;,
  &#34;customer_id&#34;    : &#34;CUST8237572&#34;,
  &#34;tealium_event&#34;  : &#34;email_signup&#34;
}
```

### カスタムクリック

|イベント名|説明|
|---|---|
|`custom_click`|ページ内の特定のクリックインタラクションを追跡する（例：製品CTA、重要な開示事項など）。|

サンプル:
```javascript
{
  &#34;link_category&#34; : &#34;Hero Banner&#34;,
  &#34;link_name&#34;     : &#34;Apply Now - Gold Credit Card&#34;,
  &#34;page_type&#34;     : &#34;product_detail&#34;,
  &#34;tealium_event&#34; : &#34;custom_click&#34;
}
```

### 同意構成更新（オプション）

|イベント名|説明|
|---|---|
|`consent_update`|ユーザーが同意またはプライバシー構成を更新した時（実際の構造は法的・規制要件を尊重する必要がある）。|

サンプル:
```javascript
{
  &#34;customer_id&#34;       : &#34;CUST8237572&#34;,
  &#34;tealium_event&#34;     : &#34;consent_update&#34;
}
```