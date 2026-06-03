---
title: Publisher data layer specification
description: This article provides the data layer definition for publishers.
url: https://docs.tealium.com/platforms/getting-started-web/data-layer/definitions/publisher/
---## Data layer attributes


|Variable| Description| Example| Type|
|---| ---| ---| ---|
|`click_category`| During click tracking events, the category of the element clicked| `footer`| String|
|`click_label`| During click tracking events, the name of the element clicked| `Submit`| String|
|`click_type`| During click tracking events, distinguish between different elements clicked| `button`| String|
|`content_author`| The name of the author of the content| `John Smith`| String|
|`content_id`| The unique ID of the page content| `38121`| String|
|`content_publish_date`| The publish date of the page content, in format YYYY/MM/DD| `2015/02/09`| String|
|`content_title`| The title of the content on the page| `Top 7 Outdoor Sleeping Bags`| String|
|`country_code`| The two-character country code of the site| `us`| String|
|`customer_city`| The customer&#39;s city of residence| `San Diego`| String|
|`customer_country`| The customer&#39;s country of residence| `United States`| String|
|`customer_email`| The customer&#39;s email address| `johnsmith@example.com`| String|
|`customer_first_name`| The first name of the customer| `John`| String|
|`customer_id`| The unique customer ID (if not `customer_email`)| `8237572`| String|
|`customer_is_logged_in`| A flag to indicate if the current user is logged in| `1`| String|
|`customer_last_name`| The last name of the customer| `Smith`| String|
|`customer_postal_code`| The customer&#39;s postal code| `92101`| String|
|`customer_state`| The customer&#39;s state/province of residence| `CA`| String|
|`customer_type`| Distinguishes between registered users and guests| `guest`| String|
|`language_code`| The two-character language code of the site| `en`| String|
|`page_friendly_url`| The canonical URL of the page, might be different than the URL in the browser location bar| `/travel/national_parks`| String|
|`page_name`| The user-friendly name of the page| `Homepage`| String|
|`page_number`| For paginated content or galleries, the current page number in view| `2`| String|
|`page_type`| The Tealium variable to identify the type of page or template| `content`| String|
|`search_keyword`| The search text entered by the user| `Napa valley`| String|
|`search_results`| The number of search results returned| `42`| String|
|`site_display_format`| The display format of the site in view| `mobile`| String|
|`site_section`| The top-level section of your site| `Travel`| String|
|`site_subsection1`| The first level category of the page hierarchy| `National Parks`| String|
|`site_subsection2`| The second level category of the page hierarchy| `California`| String|
|`site_subsection3`| The third level category of the page hierarchy| `Yosemite`| String|
|`site_subsection4`| The fourth level category of the page hierarchy| `Camping`| String|
|`slide_title`| On a gallery page, the title of the current slide in view| `#2 Yellowstone`| String|
|`social_network`| During social share events, the name of the social network used| `facebook`| String|

## Tracked pages

### Home Page

|Event Name|Description|Sample URL|
|---|---|---|
| `page_view`| The home page.| `http://www.example.com/`|

Sample:  
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

### Section Page

|Event Name|Description|Sample URL|
|---|---|---|
| `page_view`| A parent-category or top-level section page.| `http://www.example.com/top-level/`|

Sample:  
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

### Category Page

|Event Name|Description|Sample URL|
|---|---|---|
| `category_view`| A category page, usually displaying a list of products.| `http://www.example.com/top-level/sub-level/`|

Sample:  
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

### Content Page

|Event Name|Description|Sample URL|
|---|---|---|
| `content_view`| A content page.| `http://www.example.com/section/category/content.html`|

Sample:  
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

### Gallery Page

|Event Name|Description|Sample URL|
|---|---|---|
| `content_view`| A page of content displayed as a gallery of slides.| `http://www.example.com/section/category/gallery.html`|

Sample:  
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

### Search Page

|Event Name|Description|Sample URL|
|---|---|---|
| `search`| A search results page.| `http://www.example.com/search?query=term`|

Sample:  
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

## Tracked events

### User Login

|Event Name|Description|
|---|---|
| `user_login`| Upon successful user login.|

Sample:  
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

### User Logout

|Event Name|Description|
|---|---|
| `user_logout`| Upon successful user logout.|

Sample:  
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

### User Registration

|Event Name|Description|
|---|---|
| `user_register`| Upon successful user registration.|

Sample:  
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
### User Update

|Event Name|Description|
|---|---|
| `user_update`| Upon successful update of user profile information.|

Sample:  
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
### Email Signup

|Event Name|Description|
|---|---|
| `email_signup`| Upon successful signup for email newsletter.|

Sample:  
```javascript
{
    &#34;customer_email&#34;  : &#34;john.smith@example.com&#34;,
    &#34;tealium_event&#34;   : &#34;email_signup&#34;
}
```

### Custom Click

|Event Name|Description|
|---|---|
| `custom_click`| Tracking of specific click interactions with the page.|

Sample:  
```javascript
{
    &#34;link_category&#34;  : &#34;Header&#34;,
    &#34;link_name&#34;      : &#34;Login&#34;,
    &#34;tealium_event&#34;  : &#34;custom_click&#34;
}
```
### Social Share

|Event Name|Description|
|---|---|
| `social_share`| Tracking of social media sharing actions.|

Sample:  
```javascript
{
    &#34;content_id&#34;        : &#34;38121&#34;,
    &#34;page_friendly_url&#34; : &#34;/travel/national_parks&#34;,
    &#34;page_name&#34;         : &#34;Travel: National Parks&#34;,
    &#34;social_network&#34;    : &#34;facebook&#34;,
    &#34;tealium_event&#34;     : &#34;social_share&#34;
}
```
