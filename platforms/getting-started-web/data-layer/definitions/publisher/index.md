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
|`customer_city`| The customer's city of residence| `San Diego`| String|
|`customer_country`| The customer's country of residence| `United States`| String|
|`customer_email`| The customer's email address| `johnsmith@example.com`| String|
|`customer_first_name`| The first name of the customer| `John`| String|
|`customer_id`| The unique customer ID (if not `customer_email`)| `8237572`| String|
|`customer_is_logged_in`| A flag to indicate if the current user is logged in| `1`| String|
|`customer_last_name`| The last name of the customer| `Smith`| String|
|`customer_postal_code`| The customer's postal code| `92101`| String|
|`customer_state`| The customer's state/province of residence| `CA`| String|
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

### Section Page

|Event Name|Description|Sample URL|
|---|---|---|
| `page_view`| A parent-category or top-level section page.| `http://www.example.com/top-level/`|

Sample:  
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

### Category Page

|Event Name|Description|Sample URL|
|---|---|---|
| `category_view`| A category page, usually displaying a list of products.| `http://www.example.com/top-level/sub-level/`|

Sample:  
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

### Content Page

|Event Name|Description|Sample URL|
|---|---|---|
| `content_view`| A content page.| `http://www.example.com/section/category/content.html`|

Sample:  
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

### Gallery Page

|Event Name|Description|Sample URL|
|---|---|---|
| `content_view`| A page of content displayed as a gallery of slides.| `http://www.example.com/section/category/gallery.html`|

Sample:  
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

### Search Page

|Event Name|Description|Sample URL|
|---|---|---|
| `search`| A search results page.| `http://www.example.com/search?query=term`|

Sample:  
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

## Tracked events

### User Login

|Event Name|Description|
|---|---|
| `user_login`| Upon successful user login.|

Sample:  
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

### User Logout

|Event Name|Description|
|---|---|
| `user_logout`| Upon successful user logout.|

Sample:  
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

### User Registration

|Event Name|Description|
|---|---|
| `user_register`| Upon successful user registration.|

Sample:  
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
### User Update

|Event Name|Description|
|---|---|
| `user_update`| Upon successful update of user profile information.|

Sample:  
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
### Email Signup

|Event Name|Description|
|---|---|
| `email_signup`| Upon successful signup for email newsletter.|

Sample:  
```javascript
{
    "customer_email"  : "john.smith@example.com",
    "tealium_event"   : "email_signup"
}
```

### Custom Click

|Event Name|Description|
|---|---|
| `custom_click`| Tracking of specific click interactions with the page.|

Sample:  
```javascript
{
    "link_category"  : "Header",
    "link_name"      : "Login",
    "tealium_event"  : "custom_click"
}
```
### Social Share

|Event Name|Description|
|---|---|
| `social_share`| Tracking of social media sharing actions.|

Sample:  
```javascript
{
    "content_id"        : "38121",
    "page_friendly_url" : "/travel/national_parks",
    "page_name"         : "Travel: National Parks",
    "social_network"    : "facebook",
    "tealium_event"     : "social_share"
}
```
