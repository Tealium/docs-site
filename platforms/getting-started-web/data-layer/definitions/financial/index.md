---
title: Financial services data layer specification
description: This article provides the data layer definition for financial services business, such as banking, credit cards, loans, and investment platforms.
url: https://docs.tealium.com/platforms/getting-started-web/data-layer/definitions/financial/
---
## Data layer attributes


|Variable| Description| Example| Type|
|---| ---| ---| ---|
| `account_balance` | Current balance of the primary account in view, as a string with only digits and decimal | `1543.27` | String |
| `account_currency_code` | Currency code of the account in view | `EUR` | String |
| `account_id` | Unique ID for the account in view | `ACC123456` | String |
| `account_masked_number` | Masked account or card number | `•••• •••• •••• 1234` | String |
| `account_status` | Status of the account | `active` | String |
| `account_tenure` | Tenure of the account in months or years | `3_years` | String |
| `account_type` | Type of account | `checking` | String |
| `application_channel` | Channel where the product application is initiated | `web` | String |
| `application_decision` | Final decision of the application | `approved` | String |
| `application_id` | Unique ID for the product application | `APP987654` | String |
| `application_stage` | Current step in the application flow | `document_upload` | String |
| `application_status` | Status of the application | `in_review` | String |
| `customer_city` | Customer’s city of residence | `Frankfurt` | String |
| `customer_country` | Customer’s country of residence | `Germany` | String |
| `customer_email` | Customer’s email address | `user@example.com` | String |
| `customer_first_name` | First name of the customer | `John` | String |
| `customer_id` | Unique customer ID | `CUST8237572` | String |
| `customer_last_name` | Last name of the customer | `Smith` | String |
| `customer_postal_code` | Customer’s postal code | `60311` | String |
| `customer_segment` | Bank-defined segment for the customer | `premium` | String |
| `customer_state` | Customer’s state/region of residence | `HE` | String |
| `device_type` | Device type used to access the site or app | `mobile` | String |
| `event_name` | Tealium variable to identify unique events | `application_start` | String |
| `language_code` | Language code | `de` | String |
| `link_category` | During click tracking events, the category of the element clicked | `Header` | String |
| `link_name` | During click tracking events, the name of the element clicked | `Login` | String |
| `login_method` | Method used to log in | `username_password` | String |
| `page_name` | Tealium variable to identify the page name | `Account Overview` | String |
| `page_type` | Type of page | `account_overview` | String |
| `product_category` | Higher-level financial product grouping | `lending` | String |
| `product_id` | Product identifier used internally for the financial product | `CC_GOLD_01` | String |
| `product_name` | Display name of the financial product | `Gold Credit Card` | String |
| `product_subcategory` | More granular grouping of the financial product | `credit_card` | String |
| `referral_source` | Source or partner that referred the visitor | `partner_portal` | String |
| `risk_profile` | Risk profile or suitability band (when applicable and compliant) | `balanced` | String |
| `search_keyword` | Text value entered in the on‑site search | `credit card` | String |
| `search_results` | Number of results returned by search | `23` | String |
| `session_id` | Unique identifier of the current session | `8f23c7e9-1234-5678` | String |
| `site_section` | High-level section of the site or app | `Retail Banking` | String |
| `transaction_amount` | Monetary amount of the transaction as a string with only digits and decimal | `250.00` | String |
| `transaction_category` | Category of the transaction | `transfer` | String |
| `transaction_currency_code` | Currency code for the transaction | `EUR` | String |
| `transaction_date` | Transaction date in ISO 8601 format | `2026-02-11` | String |
| `transaction_id` | Unique ID of the transaction | `TXN567890` | String |
| `transaction_method` | Method used for the transaction | `wire` | String |
| `transaction_status` | Status of the transaction | `success` | String |
| `transaction_type` | Type of transaction | `outgoing` | String |
| `user_auth_state` | Indicates whether the user is authenticated | `authenticated` | String |
| `user_login_state` | Login state of the user | `logged_in` | String |
| `user_role` | Role of the logged in user (if applicable) | `primary_holder` | String |

## Tracked pages

### Home Page

|Event Name|Description| Sample URL|
|---| ---| ---|
|`page_view`|The public landing page for the bank or financial institution.|`https://www.example.com/`|

Sample:
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

### Account Overview Page

|Event Name|Description| Sample URL|
|---| ---| ---|
|`page_view`|The authenticated account overview, listing key accounts and balances.|`https://www.example.com/online-banking/accounts/overview`|

Sample:
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

### Account Detail Page

|Event Name|Description| Sample URL|
|---| ---| ---|
|`account_view`|A specific account detail page, usually showing recent transactions.|`https://www.example.com/online-banking/accounts/checking/ACC123456`|

Sample:
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

### Product Listing Page

|Event Name|Description| Sample URL|
|---| ---| ---|
|`page_view`|A product or offer listing page (for example, all credit cards).|`https://www.example.com/products/credit-cards/`|

Sample:
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

### Product Detail Page

|Event Name|Description| Sample URL|
|---| ---| ---|
|`product_view`|A financial product detail page.|`https://www.example.com/products/credit-cards/gold-card`|

Sample:
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

### Search Page

|Event Name|Description| Sample URL|
|---| ---| ---|
|`search`|An on-site search results page.|`https://www.example.com/search?query=credit+card`|

Sample:
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

### Login Page

|Event Name|Description| Sample URL|
|---| ---| ---|
|`page_view`|Online banking login page.|`https://www.example.com/online-banking/login`|

Sample:
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

### Application Flow Pages

|Event Name|Description| Sample URL|
|---|---| ---|
|`application_view`| A step in the product application journey (for example, viewing the personal details screen).|`https://www.example.com/apply/credit-card/personal-details`|

Sample:
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

### Application Complete Page

|Event Name|Description| Sample URL|
|---|---| ---|
|`application_complete`|Application confirmation page (for example, approval or submission received).|`https://www.example.com/apply/credit-card/confirmation`|

Sample:
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

### Profile / Settings Page

|Event Name|Description| Sample URL|
|---| ---| ---|
|`page_view`|User profile or settings pages (for example, contact details, security settings).|`https://www.example.com/online-banking/profile`|

Sample:
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

## Tracked events

### Login Success

|Event Name|Description|
|---|---|
|`login_success`|Upon successful authentication.|

Sample:
```javascript
{
  "customer_id"      : "CUST8237572",
  "user_auth_state"  : "authenticated",
  "login_method"     : "username_password",
  "device_type"      : "mobile",
  "tealium_event"    : "login_success"
}
```

### Login Failure

|Event Name|Description|
|---|---|
|`login_failure`|Upon an unsuccessful login attempt (no sensitive credentials captured).|

Sample:
```javascript
{
  "user_auth_state"  : "unauthenticated",
  "login_method"     : "username_password",
  "device_type"      : "desktop",
  "tealium_event"    : "login_failure"
}
```

### Transaction Initiated

|Event Name|Description|
|---|---|
|`transaction_initiated`|Upon a user submitting details to start a transaction (for example, transfer, payment).|

Sample:
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

### Transaction Success

|Event Name|Description|
|---|---|
|`transaction_success`|Upon a transaction being successfully completed.|

Sample:
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

### Transaction Failure

|Event Name|Description|
|---|---|
|`transaction_failure`|Upon a transaction failing (for example, insufficient funds, technical error).|

Sample:
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

### Application Start

|Event Name|Description|
|---|---|
|`application_start`|Upon a user starting a new product application.|

Sample:
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

### Application Step

|Event Name|Description|
|---|---|
|`application_step`|Upon each intermediate step of the application flow.|

Sample:
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

### Application Outcome

|Event Name|Description|
|---|---|
|`application_outcome`|When the application receives a decision.|

Sample:
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

### User Registration

|Event Name|Description|
|---|---|
|`user_register`|Upon successful new user registration.|

Sample:
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

### User Profile Update

|Event Name|Description|
|---|---|
|`user_update`|Upon successful update of profile information.|

Sample:
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

### Email Signup

|Event Name|Description|
|---|---|
|`email_signup`|Upon successful signup for newsletters or product updates.|

Sample:
```javascript
{
  "customer_email" : "john.smith@example.com",
  "customer_id"    : "CUST8237572",
  "tealium_event"  : "email_signup"
}
```

### Custom Click

|Event Name|Description|
|---|---|
|`custom_click`|Track specific click interactions with the page (for example, product CTAs, important disclosures).|

Sample:
```javascript
{
  "link_category" : "Hero Banner",
  "link_name"     : "Apply Now - Gold Credit Card",
  "page_type"     : "product_detail",
  "tealium_event" : "custom_click"
}
```

### Consent Preference Update (Optional)

|Event Name|Description|
|---|---|
|`consent_update`|When a user updates their consent or privacy preferences (actual structure must respect legal/regulatory requirements).|

Sample:
```javascript
{
  "customer_id"       : "CUST8237572",
  "tealium_event"     : "consent_update"
}
```