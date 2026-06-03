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
    &#34;country_code&#34;           : &#34;us&#34;,
    &#34;customer_email&#34;         : &#34;johnsmith@example.com&#34;,
    &#34;customer_first_name&#34;    : &#34;John&#34;,
    &#34;customer_id&#34;            : &#34;8237572&#34;,
    &#34;customer_is_logged_in&#34;  : &#34;1&#34;,
    &#34;customer_last_name&#34;     : &#34;Smith&#34;,
    &#34;customer_type&#34;          : &#34;registered&#34;,
    &#34;language_code&#34;          : &#34;en&#34;,
    &#34;page_friendly_url&#34;      : &#34;/home&#34;,
    &#34;page_name&#34;              : &#34;Homepage&#34;,
    &#34;page_type&#34;              : &#34;home&#34;,
    &#34;site_display_format&#34;    : &#34;desktop&#34;,
    &#34;site_section&#34;           : &#34;Home&#34;,
    &#34;tealium_event&#34;          : &#34;page_view&#34;
}
```

### セクションページ

|イベント名|説明|サンプルURL|
|---|---|---|
| `page_view`| 親カテゴリまたはトップレベルセクションページ。| `http://www.example.com/top-level/`|

サンプル:  
```javascript
{
    &#34;country_code&#34;           : &#34;us&#34;,
    &#34;customer_email&#34;         : &#34;johnsmith@example.com&#34;,
    &#34;customer_first_name&#34;    : &#34;John&#34;,
    &#34;customer_id&#34;            : &#34;8237572&#34;,
    &#34;customer_is_logged_in&#34;  : &#34;1&#34;,
    &#34;customer_last_name&#34;     : &#34;Smith&#34;,
    &#34;customer_type&#34;          : &#34;registered&#34;,
    &#34;language_code&#34;          : &#34;en&#34;,
    &#34;page_friendly_url&#34;      : &#34;/travel&#34;,
    &#34;page_name&#34;              : &#34;Travel Home&#34;,
    &#34;page_type&#34;              : &#34;section&#34;,
    &#34;site_display_format&#34;    : &#34;desktop&#34;,
    &#34;site_section&#34;           : &#34;Travel&#34;,
    &#34;tealium_event&#34;          : &#34;page_view&#34;
}
```

### カテゴリページ

|イベント名|説明|サンプルURL|
|---|---|---|
| `category_view`| 通常、製品リストが表示されるカテゴリページ。| `http://www.example.com/top-level/sub-level/`|

サンプル:  
```javascript
{
    &#34;country_code&#34;           : &#34;us&#34;,
    &#34;customer_email&#34;         : &#34;johnsmith@example.com&#34;,
    &#34;customer_first_name&#34;    : &#34;John&#34;,
    &#34;customer_id&#34;            : &#34;8237572&#34;,
    &#34;customer_is_logged_in&#34;  : &#34;1&#34;,
    &#34;customer_last_name&#34;     : &#34;Smith&#34;,
    &#34;customer_type&#34;          : &#34;registered&#34;,
    &#34;language_code&#34;          : &#34;en&#34;,
    &#34;page_friendly_url&#34;      : &#34;/travel/national_parks/yosemite_camping&#34;,
    &#34;page_name&#34;              : &#34;Homepage&#34;,
    &#34;page_number&#34;            : &#34;2&#34;,
    &#34;page_type&#34;              : &#34;category&#34;,
    &#34;site_display_format&#34;    : &#34;desktop&#34;,
    &#34;site_section&#34;           : &#34;Travel&#34;,
    &#34;site_subsection1&#34;       : &#34;National Parks&#34;,
    &#34;site_subsection2&#34;       : &#34;California&#34;,
    &#34;site_subsection3&#34;       : &#34;Yosemite&#34;,
    &#34;site_subsection4&#34;       : &#34;Camping&#34;,
    &#34;tealium_event&#34;          : &#34;category_view&#34;
}
```

### コンテンツページ

|イベント名|説明|サンプルURL|
|---|---|---|
| `content_view`| コンテンツページ。| `http://www.example.com/section/category/content.html`|

サンプル:  
```javascript
{
    &#34;content_author&#34;         : &#34;Sue Smith&#34;,
    &#34;content_id&#34;             : &#34;38121&#34;,
    &#34;content_publish_date&#34;   : &#34;2015/02/09&#34;,
    &#34;content_title&#34;          : &#34;Top 7 Outdoor Sleeping Bags&#34;,
    &#34;country_code&#34;           : &#34;us&#34;,
    &#34;customer_email&#34;         : &#34;johnsmith@example.com&#34;,
    &#34;customer_first_name&#34;    : &#34;John&#34;,
    &#34;customer_id&#34;            : &#34;8237572&#34;,
    &#34;customer_is_logged_in&#34;  : &#34;1&#34;,
    &#34;customer_last_name&#34;     : &#34;Smith&#34;,
    &#34;customer_type&#34;          : &#34;registered&#34;,
    &#34;language_code&#34;          : &#34;en&#34;,
    &#34;page_friendly_url&#34;      : &#34;/travel/parks/ca/gear/bags.html&#34;,
    &#34;page_name&#34;              : &#34;Camping Gear: Top Sleeping Bags&#34;,
    &#34;page_type&#34;              : &#34;content&#34;,
    &#34;site_display_format&#34;    : &#34;desktop&#34;,
    &#34;site_section&#34;           : &#34;Travel&#34;,
    &#34;site_subsection1&#34;       : &#34;National Parks&#34;,
    &#34;site_subsection2&#34;       : &#34;California&#34;,
    &#34;site_subsection3&#34;       : &#34;Yosemite&#34;,
    &#34;site_subsection4&#34;       : &#34;Camping&#34;,
    &#34;tealium_event&#34;          : &#34;content_view&#34;
}
```
### ギャラリーページ

|イベント名|説明|サンプルURL|
|---|---|---|
| `content_view`| スライドのギャラリーとして表示されるコンテンツページ。| `http://www.example.com/section/category/gallery.html`|

サンプル:  
```javascript
{
    &#34;country_code&#34;           : &#34;us&#34;,
    &#34;customer_email&#34;         : &#34;johnsmith@example.com&#34;,
    &#34;customer_first_name&#34;    : &#34;John&#34;,
    &#34;customer_id&#34;            : &#34;8237572&#34;,
    &#34;customer_is_logged_in&#34;  : &#34;1&#34;,
    &#34;customer_last_name&#34;     : &#34;Smith&#34;,
    &#34;customer_type&#34;          : &#34;registered&#34;,
    &#34;language_code&#34;          : &#34;en&#34;,
    &#34;page_friendly_url&#34;      : &#34;/travel/national_parks&#34;,
    &#34;page_name&#34;              : &#34;Top Parks Gallery&#34;,
    &#34;page_number&#34;            : &#34;2&#34;,
    &#34;page_type&#34;              : &#34;gallery&#34;,
    &#34;site_display_format&#34;    : &#34;desktop&#34;,
    &#34;site_section&#34;           : &#34;Travel&#34;,
    &#34;site_subsection1&#34;       : &#34;National Parks&#34;,
    &#34;slide_title&#34;            : &#34;#2 Yellowstone&#34;,
    &#34;tealium_event&#34;          : &#34;content_view&#34;
}
```

### 検索ページ

|イベント名|説明|サンプルURL|
|---|---|---|
| `search`| 検索結果ページ。| `http://www.example.com/search?query=term`|

サンプル:  
```javascript
{
    &#34;country_code&#34;           : &#34;us&#34;,
    &#34;customer_email&#34;         : &#34;johnsmith@example.com&#34;,
    &#34;customer_first_name&#34;    : &#34;John&#34;,
    &#34;customer_id&#34;            : &#34;8237572&#34;,
    &#34;customer_is_logged_in&#34;  : &#34;1&#34;,
    &#34;customer_last_name&#34;     : &#34;Smith&#34;,
    &#34;customer_type&#34;          : &#34;registered&#34;,
    &#34;language_code&#34;          : &#34;en&#34;,
    &#34;page_friendly_url&#34;      : &#34;/search/napa_valley/&#34;,
    &#34;page_name&#34;              : &#34;Search results for: napa valley&#34;,
    &#34;page_number&#34;            : &#34;1&#34;,
    &#34;page_type&#34;              : &#34;search&#34;,
    &#34;search_keyword&#34;         : &#34;napa valley&#34;,
    &#34;search_results&#34;         : &#34;42&#34;,
    &#34;site_display_format&#34;    : &#34;desktop&#34;,
    &#34;site_section&#34;           : &#34;Travel&#34;,
    &#34;tealium_event&#34;          : &#34;search&#34;
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
    &#34;customer_city&#34;         : &#34;San Diego&#34;,
    &#34;customer_country&#34;      : &#34;United States&#34;,
    &#34;customer_email&#34;        : &#34;john.smith@example.com&#34;,
    &#34;customer_first_name&#34;   : &#34;John&#34;,
    &#34;customer_id&#34;           : &#34;8237572&#34;,
    &#34;customer_last_name&#34;    : &#34;Smith&#34;,
    &#34;customer_postal_code&#34;  : &#34;92101&#34;,
    &#34;customer_state&#34;        : &#34;CA&#34;,
    &#34;tealium_event&#34;         : &#34;user_login&#34;
}
```

### ユーザーログアウト

|イベント名|説明|
|---|---|
| `user_logout`| ユーザーログアウト成功時。|

サンプル:  
```javascript
{
    &#34;customer_city&#34;         : &#34;San Diego&#34;,
    &#34;customer_country&#34;      : &#34;United States&#34;,
    &#34;customer_email&#34;        : &#34;john.smith@example.com&#34;,
    &#34;customer_first_name&#34;   : &#34;John&#34;,
    &#34;customer_id&#34;           : &#34;8237572&#34;,
    &#34;customer_last_name&#34;    : &#34;Smith&#34;,
    &#34;customer_postal_code&#34;  : &#34;92101&#34;,
    &#34;customer_state&#34;        : &#34;CA&#34;,
    &#34;tealium_event&#34;         : &#34;user_logout&#34;
}
```

### ユーザー登録

|イベント名|説明|
|---|---|
| `user_register`| ユーザー登録成功時。|

サンプル:  
```javascript
{
    &#34;customer_city&#34;         : &#34;San Diego&#34;,
    &#34;customer_country&#34;      : &#34;United States&#34;,
    &#34;customer_email&#34;        : &#34;john.smith@example.com&#34;,
    &#34;customer_first_name&#34;   : &#34;John&#34;,
    &#34;customer_id&#34;           : &#34;8237572&#34;,
    &#34;customer_last_name&#34;    : &#34;Smith&#34;,
    &#34;customer_postal_code&#34;  : &#34;92101&#34;,
    &#34;customer_state&#34;        : &#34;CA&#34;,
    &#34;tealium_event&#34;         : &#34;user_register&#34;
}
```
### ユーザー情報更新

|イベント名|説明|
|---|---|
| `user_update`| ユーザープロファイル情報の更新成功時。|

サンプル:  
```javascript
{
    &#34;customer_city&#34;         : &#34;San Diego&#34;,
    &#34;customer_country&#34;      : &#34;United States&#34;,
    &#34;customer_email&#34;        : &#34;john.smith@example.com&#34;,
    &#34;customer_first_name&#34;   : &#34;John&#34;,
    &#34;customer_id&#34;           : &#34;8237572&#34;,
    &#34;customer_last_name&#34;    : &#34;Smith&#34;,
    &#34;customer_postal_code&#34;  : &#34;92101&#34;,
    &#34;customer_state&#34;        : &#34;CA&#34;,
    &#34;tealium_event&#34;         : &#34;user_update&#34;
}
```
### メールサインアップ

|イベント名|説明|
|---|---|
| `email_signup`| メールニュースレターへのサインアップ成功時。|

サンプル:  
```javascript
{
    &#34;customer_email&#34;  : &#34;john.smith@example.com&#34;,
    &#34;tealium_event&#34;   : &#34;email_signup&#34;
}
```

### カスタムクリック

|イベント名|説明|
|---|---|
| `custom_click`| ページ内の特定のクリックインタラクションの追跡。|

サンプル:  
```javascript
{
    &#34;link_category&#34;  : &#34;Header&#34;,
    &#34;link_name&#34;      : &#34;Login&#34;,
    &#34;tealium_event&#34;  : &#34;custom_click&#34;
}
```
### ソーシャルシェア

|イベント名|説明|
|---|---|
| `social_share`| ソーシャルメディアの共有アクションの追跡。|

サンプル:  
```javascript
{
    &#34;content_id&#34;        : &#34;38121&#34;,
    &#34;page_friendly_url&#34; : &#34;/travel/national_parks&#34;,
    &#34;page_name&#34;         : &#34;Travel: National Parks&#34;,
    &#34;social_network&#34;    : &#34;facebook&#34;,
    &#34;tealium_event&#34;     : &#34;social_share&#34;
}
```