---
title: 公開者データレイヤー仕様
description: この記事では、公開者のためのデータレイヤー定義を提供します。
url: https://docs.tealium.com/ja/platforms/getting-started-web/data-layer/definitions/publisher/
---## データレイヤー属性

|変数| 説明| 例| タイプ|
|---| ---| ---| ---|
|`click_category`| クリック追跡イベント時のクリックされた要素のカテゴリ| `footer`| 文字列|
|`click_label`| クリック追跡イベント時のクリックされた要素の名前| `Submit`| 文字列|
|`click_type`| クリック追跡イベント時に異なる要素がクリックされたことを区別| `button`| 文字列|
|`content_author`| コンテンツの著者名| `John Smith`| 文字列|
|`content_id`| ページコンテンツの一意のID| `38121`| 文字列|
|`content_publish_date`| ページコンテンツの公開日、形式 YYYY/MM/DD| `2015/02/09`| 文字列|
|`content_title`| ページ上のコンテンツのタイトル| `Top 7 Outdoor Sleeping Bags`| 文字列|
|`country_code`| サイトの2文字国コード| `us`| 文字列|
|`customer_city`| 顧客の居住都市| `San Diego`| 文字列|
|`customer_country`| 顧客の居住国| `United States`| 文字列|
|`customer_email`| 顧客のメールアドレス| `johnsmith@example.com`| 文字列|
|`customer_first_name`| 顧客の名| `John`| 文字列|
|`customer_id`| 一意の顧客ID（`customer_email`以外の場合）| `8237572`| 文字列|
|`customer_is_logged_in`| 現在のユーザーがログインしているかどうかを示すフラグ| `1`| 文字列|
|`customer_last_name`| 顧客の姓| `Smith`| 文字列|
|`customer_postal_code`| 顧客の郵便番号| `92101`| 文字列|
|`customer_state`| 顧客の居住州/省| `CA`| 文字列|
|`customer_type`| 登録ユーザーとゲストを区別| `guest`| 文字列|
|`language_code`| サイトの2文字言語コード| `en`| 文字列|
|`page_friendly_url`| ページの正規URL、ブラウザのロケーションバーのURLと異なる場合がある| `/travel/national_parks`| 文字列|
|`page_name`| ページのユーザーフレンドリーな名前| `Homepage`| 文字列|
|`page_number`| ページネーションされたコンテンツやギャラリーの場合、表示中の現在のページ番号| `2`| 文字列|
|`page_type`| ページまたはテンプレートの種類を識別するTealium変数| `content`| 文字列|
|`search_keyword`| ユーザーが入力した検索テキスト| `Napa valley`| 文字列|
|`search_results`| 返された検索結果の数| `42`| 文字列|
|`site_display_format`| 表示中のサイトの表示形式| `mobile`| 文字列|
|`site_section`| サイトのトップレベルセクション| `Travel`| 文字列|
|`site_subsection1`| ページ階層の第1レベルカテゴリ| `National Parks`| 文字列|
|`site_subsection2`| ページ階層の第2レベルカテゴリ| `California`| 文字列|
|`site_subsection3`| ページ階層の第3レベルカテゴリ| `Yosemite`| 文字列|
|`site_subsection4`| ページ階層の第4レベルカテゴリ| `Camping`| 文字列|
|`slide_title`| ギャラリーページで、表示中の現在のスライドのタイトル| `#2 Yellowstone`| 文字列|
|`social_network`| ソーシャル共有イベント中に使用されたソーシャルネットワークの名前| `facebook`| 文字列|

## 追跡されるページ

### ホームページ

|イベント名|説明|サンプルURL|
|---|---|---|
| `page_view`| ホームページ。| `http://www.example.com/`|

サンプル:  
```javascript
{
    "country_code"           : "us",
    "customer_email"         : "johnsmith@example.com",
    "customer_first_name"    : "John",
    "customer_id"            : "8237572",
    "customer_is_logged_in"  : "1",
    "customer_last_name"     : "Smith",
    "customer_type"          : "registered",
    "language_code"          : "en",
    "page_friendly_url"      : "/home",
    "page_name"              : "Homepage",
    "page_type"              : "home",
    "site_display_format"    : "desktop",
    "site_section"           : "Home",
    "tealium_event"          : "page_view"
}
```

### セクションページ

|イベント名|説明|サンプルURL|
|---|---|---|
| `page_view`| 親カテゴリまたはトップレベルセクションページ。| `http://www.example.com/top-level/`|

サンプル:  
```javascript
{
    "country_code"           : "us",
    "customer_email"         : "johnsmith@example.com",
    "customer_first_name"    : "John",
    "customer_id"            : "8237572",
    "customer_is_logged_in"  : "1",
    "customer_last_name"     : "Smith",
    "customer_type"          : "registered",
    "language_code"          : "en",
    "page_friendly_url"      : "/travel",
    "page_name"              : "Travel Home",
    "page_type"              : "section",
    "site_display_format"    : "desktop",
    "site_section"           : "Travel",
    "tealium_event"          : "page_view"
}
```

### カテゴリページ

|イベント名|説明|サンプルURL|
|---|---|---|
| `category_view`| 通常、製品リストが表示されるカテゴリページ。| `http://www.example.com/top-level/sub-level/`|

サンプル:  
```javascript
{
    "country_code"           : "us",
    "customer_email"         : "johnsmith@example.com",
    "customer_first_name"    : "John",
    "customer_id"            : "8237572",
    "customer_is_logged_in"  : "1",
    "customer_last_name"     : "Smith",
    "customer_type"          : "registered",
    "language_code"          : "en",
    "page_friendly_url"      : "/travel/national_parks/yosemite_camping",
    "page_name"              : "Homepage",
    "page_number"            : "2",
    "page_type"              : "category",
    "site_display_format"    : "desktop",
    "site_section"           : "Travel",
    "site_subsection1"       : "National Parks",
    "site_subsection2"       : "California",
    "site_subsection3"       : "Yosemite",
    "site_subsection4"       : "Camping",
    "tealium_event"          : "category_view"
}
```

### コンテンツページ

|イベント名|説明|サンプルURL|
|---|---|---|
| `content_view`| コンテンツページ。| `http://www.example.com/section/category/content.html`|

サンプル:  
```javascript
{
    "content_author"         : "Sue Smith",
    "content_id"             : "38121",
    "content_publish_date"   : "2015/02/09",
    "content_title"          : "Top 7 Outdoor Sleeping Bags",
    "country_code"           : "us",
    "customer_email"         : "johnsmith@example.com",
    "customer_first_name"    : "John",
    "customer_id"            : "8237572",
    "customer_is_logged_in"  : "1",
    "customer_last_name"     : "Smith",
    "customer_type"          : "registered",
    "language_code"          : "en",
    "page_friendly_url"      : "/travel/parks/ca/gear/bags.html",
    "page_name"              : "Camping Gear: Top Sleeping Bags",
    "page_type"              : "content",
    "site_display_format"    : "desktop",
    "site_section"           : "Travel",
    "site_subsection1"       : "National Parks",
    "site_subsection2"       : "California",
    "site_subsection3"       : "Yosemite",
    "site_subsection4"       : "Camping",
    "tealium_event"          : "content_view"
}
```
### ギャラリーページ

|イベント名|説明|サンプルURL|
|---|---|---|
| `content_view`| スライドのギャラリーとして表示されるコンテンツページ。| `http://www.example.com/section/category/gallery.html`|

サンプル:  
```javascript
{
    "country_code"           : "us",
    "customer_email"         : "johnsmith@example.com",
    "customer_first_name"    : "John",
    "customer_id"            : "8237572",
    "customer_is_logged_in"  : "1",
    "customer_last_name"     : "Smith",
    "customer_type"          : "registered",
    "language_code"          : "en",
    "page_friendly_url"      : "/travel/national_parks",
    "page_name"              : "Top Parks Gallery",
    "page_number"            : "2",
    "page_type"              : "gallery",
    "site_display_format"    : "desktop",
    "site_section"           : "Travel",
    "site_subsection1"       : "National Parks",
    "slide_title"            : "#2 Yellowstone",
    "tealium_event"          : "content_view"
}
```

### 検索ページ

|イベント名|説明|サンプルURL|
|---|---|---|
| `search`| 検索結果ページ。| `http://www.example.com/search?query=term`|

サンプル:  
```javascript
{
    "country_code"           : "us",
    "customer_email"         : "johnsmith@example.com",
    "customer_first_name"    : "John",
    "customer_id"            : "8237572",
    "customer_is_logged_in"  : "1",
    "customer_last_name"     : "Smith",
    "customer_type"          : "registered",
    "language_code"          : "en",
    "page_friendly_url"      : "/search/napa_valley/",
    "page_name"              : "Search results for: napa valley",
    "page_number"            : "1",
    "page_type"              : "search",
    "search_keyword"         : "napa valley",
    "search_results"         : "42",
    "site_display_format"    : "desktop",
    "site_section"           : "Travel",
    "tealium_event"          : "search"
}
```

## 追跡イベント

### ユーザーログイン

|イベント名|説明|
|---|---|
| `user_login`| ユーザーログイン成功時。|

サンプル:  
```javascript
{
    "customer_city"         : "San Diego",
    "customer_country"      : "United States",
    "customer_email"        : "john.smith@example.com",
    "customer_first_name"   : "John",
    "customer_id"           : "8237572",
    "customer_last_name"    : "Smith",
    "customer_postal_code"  : "92101",
    "customer_state"        : "CA",
    "tealium_event"         : "user_login"
}
```

### ユーザーログアウト

|イベント名|説明|
|---|---|
| `user_logout`| ユーザーログアウト成功時。|

サンプル:  
```javascript
{
    "customer_city"         : "San Diego",
    "customer_country"      : "United States",
    "customer_email"        : "john.smith@example.com",
    "customer_first_name"   : "John",
    "customer_id"           : "8237572",
    "customer_last_name"    : "Smith",
    "customer_postal_code"  : "92101",
    "customer_state"        : "CA",
    "tealium_event"         : "user_logout"
}
```

### ユーザー登録

|イベント名|説明|
|---|---|
| `user_register`| ユーザー登録成功時。|

サンプル:  
```javascript
{
    "customer_city"         : "San Diego",
    "customer_country"      : "United States",
    "customer_email"        : "john.smith@example.com",
    "customer_first_name"   : "John",
    "customer_id"           : "8237572",
    "customer_last_name"    : "Smith",
    "customer_postal_code"  : "92101",
    "customer_state"        : "CA",
    "tealium_event"         : "user_register"
}
```
### ユーザー情報更新

|イベント名|説明|
|---|---|
| `user_update`| ユーザープロファイル情報の更新成功時。|

サンプル:  
```javascript
{
    "customer_city"         : "San Diego",
    "customer_country"      : "United States",
    "customer_email"        : "john.smith@example.com",
    "customer_first_name"   : "John",
    "customer_id"           : "8237572",
    "customer_last_name"    : "Smith",
    "customer_postal_code"  : "92101",
    "customer_state"        : "CA",
    "tealium_event"         : "user_update"
}
```
### メールサインアップ

|イベント名|説明|
|---|---|
| `email_signup`| メールニュースレターへのサインアップ成功時。|

サンプル:  
```javascript
{
    "customer_email"  : "john.smith@example.com",
    "tealium_event"   : "email_signup"
}
```

### カスタムクリック

|イベント名|説明|
|---|---|
| `custom_click`| ページ内の特定のクリックインタラクションの追跡。|

サンプル:  
```javascript
{
    "link_category"  : "Header",
    "link_name"      : "Login",
    "tealium_event"  : "custom_click"
}
```
### ソーシャルシェア

|イベント名|説明|
|---|---|
| `social_share`| ソーシャルメディアの共有アクションの追跡。|

サンプル:  
```javascript
{
    "content_id"        : "38121",
    "page_friendly_url" : "/travel/national_parks",
    "page_name"         : "Travel: National Parks",
    "social_network"    : "facebook",
    "tealium_event"     : "social_share"
}
```