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
  "country_code"       : "de",
  "language_code"      : "de",
  "page_name"          : "Homepage",
  "page_type"          : "home",
  "site_section"       : "Public",
  "user_auth_state"    : "unauthenticated",
  "tealium_event"      : "page_view"
}
```

### アカウント概要ページ

|イベント名|説明| サンプルURL|
|---| ---| ---|
|`page_view`|認証されたアカウント概要ページで、主要なアカウントと残高が表示されます。|`https://www.example.com/online-banking/accounts/overview`|

サンプル:
```javascript
{
  "country_code"           : "de",
  "language_code"          : "de",
  "page_name"              : "Account Overview",
  "page_type"              : "account_overview",
  "site_section"           : "Retail Banking",
  "user_auth_state"        : "authenticated",
  "customer_id"            : "CUST8237572",
  "customer_segment"       : "premium",
  "account_id"             : "ACC123456",
  "account_type"           : "checking",
  "account_currency_code"  : "EUR",
  "account_balance"        : "1543.27",
  "tealium_event"          : "page_view"
}
```

### アカウント詳細ページ

|イベント名|説明| サンプルURL|
|---| ---| ---|
|`account_view`|特定のアカウント詳細ページで、通常は最近の取引が表示されます。|`https://www.example.com/online-banking/accounts/checking/ACC123456`|

サンプル:
```javascript
{
  "country_code"           : "de",
  "language_code"          : "de",
  "page_name"              : "Checking Account Detail",
  "page_type"              : "account_detail",
  "site_section"           : "Retail Banking",
  "user_auth_state"        : "authenticated",
  "customer_id"            : "CUST8237572",
  "account_id"             : "ACC123456",
  "account_type"           : "checking",
  "account_currency_code"  : "EUR",
  "account_balance"        : "1543.27",
  "tealium_event"          : "account_view"
}
```

### 製品リストページ

|イベント名|説明| サンプルURL|
|---| ---| ---|
|`page_view`|製品またはオファーのリストページ（例えば、すべてのクレジットカード）。|`https://www.example.com/products/credit-cards/`|

サンプル:
```javascript
{
  "country_code"      : "de",
  "language_code"     : "de",
  "page_name"         : "Credit Cards Overview",
  "page_type"         : "product_listing",
  "site_section"      : "Products",
  "product_category"  : "lending",
  "product_subcategory": "credit_card",
  "tealium_event"     : "page_view"
}
```

### 製品詳細ページ

|イベント名|説明| サンプルURL|
|---| ---| ---|
|`product_view`|金融製品の詳細ページ。|`https://www.example.com/products/credit-cards/gold-card`|

サンプル:
```javascript
{
  "country_code"        : "de",
  "language_code"       : "de",
  "page_name"           : "Gold Credit Card",
  "page_type"           : "product_detail",
  "site_section"        : "Products",
  "product_id"          : "CC_GOLD_01",
  "product_name"        : "Gold Credit Card",
  "product_category"    : "lending",
  "product_subcategory" : "credit_card",
  "tealium_event"       : "product_view"
}
```
### 検索ページ

|イベント名|説明| サンプルURL|
|---| ---| ---|
|`search`|サイト内検索結果ページ。|`https://www.example.com/search?query=credit+card`|

サンプル:
```javascript
{
  "country_code"     : "de",
  "language_code"    : "de",
  "page_name"        : "Search Results",
  "page_type"        : "search",
  "site_section"     : "Public",
  "search_keyword"   : "credit card",
  "search_results"   : "23",
  "tealium_event"    : "search"
}
```

### ログインページ

|イベント名|説明| サンプルURL|
|---| ---| ---|
|`page_view`|オンラインバンキングのログインページ。|`https://www.example.com/online-banking/login`|

サンプル:
```javascript
{
  "country_code"     : "de",
  "language_code"    : "de",
  "page_name"        : "Online Banking Login",
  "page_type"        : "login",
  "site_section"     : "Retail Banking",
  "user_auth_state"  : "unauthenticated",
  "tealium_event"    : "page_view"
}
```

### アプリケーションフローページ

|イベント名|説明| サンプルURL|
|---|---| ---|
|`application_view`|製品申請プロセスのステップ（例：個人情報画面の表示）。|`https://www.example.com/apply/credit-card/personal-details`|

サンプル:
```javascript
{
  "country_code"        : "de",
  "language_code"       : "de",
  "page_name"           : "Credit Card Application - Personal Details",
  "page_type"           : "application",
  "site_section"        : "Applications",
  "product_id"          : "CC_GOLD_01",
  "product_name"        : "Gold Credit Card",
  "product_category"    : "lending",
  "product_subcategory" : "credit_card",
  "application_id"      : "APP987654",
  "application_stage"   : "personal_details",
  "application_status"  : "in_progress",
  "tealium_event"       : "application_view"
}
```

### アプリケーション完了ページ

|イベント名|説明| サンプルURL|
|---|---| ---|
|`application_complete`|アプリケーション確認ページ（例：承認または提出受領）。|`https://www.example.com/apply/credit-card/confirmation`|

サンプル:
```javascript
{
  "country_code"        : "de",
  "language_code"       : "de",
  "page_name"           : "Credit Card Application - Confirmation",
  "page_type"           : "application_confirmation",
  "site_section"        : "Applications",
  "product_id"          : "CC_GOLD_01",
  "product_name"        : "Gold Credit Card",
  "application_id"      : "APP987654",
  "application_stage"   : "confirmation",
  "application_status"  : "completed",
  "application_decision": "approved",
  "tealium_event"       : "application_complete"
}
```

### プロファイル／構成ページ

|イベント名|説明| サンプルURL|
|---| ---| ---|
|`page_view`|ユーザープロファイルまたは構成ページ（例：連絡先詳細、セキュリティ構成）。|`https://www.example.com/online-banking/profile`|

サンプル:
```javascript
{
  "country_code"      : "de",
  "language_code"     : "de",
  "page_name"         : "Profile Settings",
  "page_type"         : "account",
  "site_section"      : "Profile",
  "user_auth_state"   : "authenticated",
  "customer_id"       : "CUST8237572",
  "tealium_event"     : "page_view"
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
  "customer_id"      : "CUST8237572",
  "user_auth_state"  : "authenticated",
  "login_method"     : "username_password",
  "device_type"      : "mobile",
  "tealium_event"    : "login_success"
}
```

### ログイン失敗

|イベント名|説明|
|---|---|
|`login_failure`|ログイン試行に失敗した際（機密情報はキャプチャされません）。|

サンプル:
```javascript
{
  "user_auth_state"  : "unauthenticated",
  "login_method"     : "username_password",
  "device_type"      : "desktop",
  "tealium_event"    : "login_failure"
}
```

### トランザクション開始

|イベント名|説明|
|---|---|
|`transaction_initiated`|ユーザーがトランザクションの詳細を提出し始めた際（例：振込、支払い）。|

サンプル:
```javascript
{
  "customer_id"               : "CUST8237572",
  "account_id"                : "ACC123456",
  "transaction_id"            : "TXN567890",
  "transaction_type"          : "outgoing",
  "transaction_category"      : "transfer",
  "transaction_currency_code" : "EUR",
  "transaction_amount"        : "250.00",
  "transaction_status"        : "initiated",
  "tealium_event"             : "transaction_initiated"
}
```

### トランザクション成功

|イベント名|説明|
|---|---|
|`transaction_success`|トランザクションが成功裏に完了した際。|

サンプル:
```javascript
{
  "customer_id"               : "CUST8237572",
  "account_id"                : "ACC123456",
  "transaction_id"            : "TXN567890",
  "transaction_type"          : "outgoing",
  "transaction_category"      : "transfer",
  "transaction_currency_code" : "EUR",
  "transaction_amount"        : "250.00",
  "transaction_status"        : "success",
  "tealium_event"             : "transaction_success"
}
```

### トランザクション失敗

|イベント名|説明|
|---|---|
|`transaction_failure`|トランザクションが失敗した際（例：残高不足、技術的エラー）。|

サンプル:
```javascript
{
  "customer_id"               : "CUST8237572",
  "account_id"                : "ACC123456",
  "transaction_id"            : "TXN567890",
  "transaction_type"          : "outgoing",
  "transaction_category"      : "transfer",
  "transaction_currency_code" : "EUR",
  "transaction_amount"        : "250.00",
  "transaction_status"        : "failed",
  "tealium_event"             : "transaction_failure"
}
```

### アプリケーション開始

|イベント名|説明|
|---|---|
|`application_start`|ユーザーが新しい製品申請を開始した際。|

サンプル:
```javascript
{
  "customer_id"         : "CUST8237572",
  "product_id"          : "CC_GOLD_01",
  "product_name"        : "Gold Credit Card",
  "product_category"    : "lending",
  "product_subcategory" : "credit_card",
  "application_id"      : "APP987654",
  "application_channel" : "web",
  "application_stage"   : "start",
  "application_status"  : "in_progress",
  "tealium_event"       : "application_start"
}
```

### アプリケーションステップ

|イベント名|説明|
|---|---|
|`application_step`|アプリケーションフローの各中間ステップで。|

サンプル:
```javascript
{
  "customer_id"         : "CUST8237572",
  "product_id"          : "CC_GOLD_01",
  "application_id"      : "APP987654",
  "application_stage"   : "income_details",
  "application_status"  : "in_progress",
  "tealium_event"       : "application_step"
}
```

### アプリケーション結果

|イベント名|説明|
|---|---|
|`application_outcome`|アプリケーションが決定を受けた際。|

サンプル:
```javascript
{
  "customer_id"          : "CUST8237572",
  "product_id"           : "CC_GOLD_01",
  "application_id"       : "APP987654",
  "application_stage"    : "decision",
  "application_status"   : "completed",
  "application_decision" : "approved",
  "tealium_event"        : "application_outcome"
}
```

### ユーザー登録

|イベント名|説明|
|---|---|
|`user_register`|新しいユーザー登録が成功した際。|

サンプル:
```javascript
{
  "customer_city"        : "Frankfurt",
  "customer_country"     : "Germany",
  "customer_email"       : "john.smith@example.com",
  "customer_first_name"  : "John",
  "customer_id"          : "CUST8237572",
  "customer_last_name"   : "Smith",
  "customer_postal_code" : "60311",
  "customer_state"       : "HE",
  "tealium_event"        : "user_register"
}
```

### ユーザープロファイル更新

|イベント名|説明|
|---|---|
|`user_update`|プロファイル情報の更新が成功した際。|

サンプル:
```javascript
{
  "customer_city"        : "Frankfurt",
  "customer_country"     : "Germany",
  "customer_email"       : "john.smith@example.com",
  "customer_first_name"  : "John",
  "customer_id"          : "CUST8237572",
  "customer_last_name"   : "Smith",
  "customer_postal_code" : "60311",
  "customer_state"       : "HE",
  "tealium_event"        : "user_update"
}
```
### メールサインアップ

|イベント名|説明|
|---|---|
|`email_signup`|ニュースレターや製品更新のためのサインアップが成功した時。|

サンプル:
```javascript
{
  "customer_email" : "john.smith@example.com",
  "customer_id"    : "CUST8237572",
  "tealium_event"  : "email_signup"
}
```

### カスタムクリック

|イベント名|説明|
|---|---|
|`custom_click`|ページ内の特定のクリックインタラクションを追跡する（例：製品CTA、重要な開示事項など）。|

サンプル:
```javascript
{
  "link_category" : "Hero Banner",
  "link_name"     : "Apply Now - Gold Credit Card",
  "page_type"     : "product_detail",
  "tealium_event" : "custom_click"
}
```

### 同意構成更新（オプション）

|イベント名|説明|
|---|---|
|`consent_update`|ユーザーが同意またはプライバシー構成を更新した時（実際の構造は法的・規制要件を尊重する必要がある）。|

サンプル:
```javascript
{
  "customer_id"       : "CUST8237572",
  "tealium_event"     : "consent_update"
}
```