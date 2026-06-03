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
  &#34;country_code&#34;       : &#34;de&#34;,
  &#34;language_code&#34;      : &#34;de&#34;,
  &#34;page_name&#34;          : &#34;Homepage&#34;,
  &#34;page_type&#34;          : &#34;home&#34;,
  &#34;site_section&#34;       : &#34;Public&#34;,
  &#34;user_auth_state&#34;    : &#34;unauthenticated&#34;,
  &#34;tealium_event&#34;      : &#34;page_view&#34;
}
```

### Account Overview Page

|Event Name|Description| Sample URL|
|---| ---| ---|
|`page_view`|The authenticated account overview, listing key accounts and balances.|`https://www.example.com/online-banking/accounts/overview`|

Sample:
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

### Account Detail Page

|Event Name|Description| Sample URL|
|---| ---| ---|
|`account_view`|A specific account detail page, usually showing recent transactions.|`https://www.example.com/online-banking/accounts/checking/ACC123456`|

Sample:
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

### Product Listing Page

|Event Name|Description| Sample URL|
|---| ---| ---|
|`page_view`|A product or offer listing page (for example, all credit cards).|`https://www.example.com/products/credit-cards/`|

Sample:
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

### Product Detail Page

|Event Name|Description| Sample URL|
|---| ---| ---|
|`product_view`|A financial product detail page.|`https://www.example.com/products/credit-cards/gold-card`|

Sample:
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

### Search Page

|Event Name|Description| Sample URL|
|---| ---| ---|
|`search`|An on-site search results page.|`https://www.example.com/search?query=credit&#43;card`|

Sample:
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

### Login Page

|Event Name|Description| Sample URL|
|---| ---| ---|
|`page_view`|Online banking login page.|`https://www.example.com/online-banking/login`|

Sample:
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

### Application Flow Pages

|Event Name|Description| Sample URL|
|---|---| ---|
|`application_view`| A step in the product application journey (for example, viewing the personal details screen).|`https://www.example.com/apply/credit-card/personal-details`|

Sample:
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

### Application Complete Page

|Event Name|Description| Sample URL|
|---|---| ---|
|`application_complete`|Application confirmation page (for example, approval or submission received).|`https://www.example.com/apply/credit-card/confirmation`|

Sample:
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

### Profile / Settings Page

|Event Name|Description| Sample URL|
|---| ---| ---|
|`page_view`|User profile or settings pages (for example, contact details, security settings).|`https://www.example.com/online-banking/profile`|

Sample:
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

## Tracked events

### Login Success

|Event Name|Description|
|---|---|
|`login_success`|Upon successful authentication.|

Sample:
```javascript
{
  &#34;customer_id&#34;      : &#34;CUST8237572&#34;,
  &#34;user_auth_state&#34;  : &#34;authenticated&#34;,
  &#34;login_method&#34;     : &#34;username_password&#34;,
  &#34;device_type&#34;      : &#34;mobile&#34;,
  &#34;tealium_event&#34;    : &#34;login_success&#34;
}
```

### Login Failure

|Event Name|Description|
|---|---|
|`login_failure`|Upon an unsuccessful login attempt (no sensitive credentials captured).|

Sample:
```javascript
{
  &#34;user_auth_state&#34;  : &#34;unauthenticated&#34;,
  &#34;login_method&#34;     : &#34;username_password&#34;,
  &#34;device_type&#34;      : &#34;desktop&#34;,
  &#34;tealium_event&#34;    : &#34;login_failure&#34;
}
```

### Transaction Initiated

|Event Name|Description|
|---|---|
|`transaction_initiated`|Upon a user submitting details to start a transaction (for example, transfer, payment).|

Sample:
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

### Transaction Success

|Event Name|Description|
|---|---|
|`transaction_success`|Upon a transaction being successfully completed.|

Sample:
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

### Transaction Failure

|Event Name|Description|
|---|---|
|`transaction_failure`|Upon a transaction failing (for example, insufficient funds, technical error).|

Sample:
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

### Application Start

|Event Name|Description|
|---|---|
|`application_start`|Upon a user starting a new product application.|

Sample:
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

### Application Step

|Event Name|Description|
|---|---|
|`application_step`|Upon each intermediate step of the application flow.|

Sample:
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

### Application Outcome

|Event Name|Description|
|---|---|
|`application_outcome`|When the application receives a decision.|

Sample:
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

### User Registration

|Event Name|Description|
|---|---|
|`user_register`|Upon successful new user registration.|

Sample:
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

### User Profile Update

|Event Name|Description|
|---|---|
|`user_update`|Upon successful update of profile information.|

Sample:
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

### Email Signup

|Event Name|Description|
|---|---|
|`email_signup`|Upon successful signup for newsletters or product updates.|

Sample:
```javascript
{
  &#34;customer_email&#34; : &#34;john.smith@example.com&#34;,
  &#34;customer_id&#34;    : &#34;CUST8237572&#34;,
  &#34;tealium_event&#34;  : &#34;email_signup&#34;
}
```

### Custom Click

|Event Name|Description|
|---|---|
|`custom_click`|Track specific click interactions with the page (for example, product CTAs, important disclosures).|

Sample:
```javascript
{
  &#34;link_category&#34; : &#34;Hero Banner&#34;,
  &#34;link_name&#34;     : &#34;Apply Now - Gold Credit Card&#34;,
  &#34;page_type&#34;     : &#34;product_detail&#34;,
  &#34;tealium_event&#34; : &#34;custom_click&#34;
}
```

### Consent Preference Update (Optional)

|Event Name|Description|
|---|---|
|`consent_update`|When a user updates their consent or privacy preferences (actual structure must respect legal/regulatory requirements).|

Sample:
```javascript
{
  &#34;customer_id&#34;       : &#34;CUST8237572&#34;,
  &#34;tealium_event&#34;     : &#34;consent_update&#34;
}
```