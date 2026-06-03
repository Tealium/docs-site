---
title: Hybris Integration
description: This article describes how to configure the Hybris Integration Tag.
url: https://docs.tealium.com/client-side-tags/hybris-integration/
---
## Prerequisites

* A Tealium IQ account.
* hybris v5.0.1&#43; extracted and built, including the B2C Commerce Accelerator.

## Definitions

* Universal Data Object (UDO) = The Data Layer object of key-value pairs.   
 This object is generated in the page as the global JavaScript object `utag_data`. The Tealium `utag.js` uses `utag_data` as the base Data Layer for your tags.
* Tealium Account = The account assigned to your purchase of Tealium iQ.
* Tealium Profile = The specific web property name for your website.

## Installing Addon

**Github repo**: `https://github.com/Tealium/integration-hybris`

1. Place the `tealiumiqaddon` directory into `${HYBRIS_BIN}/custom`. This directory is in the `/hybris/bin/custom/` folder in the repo.
1. Add &amp;lt;extension dir=&#34;$\{HYBRIS_BIN\}/custom/tealiumiqaddon&#34;/\\&amp;gt; to your `config/localextensions.xml`.
1. Add `tealiumiqaddon` to `yacceleratorstorefront` by using:  
  - `sudo ant addoninstall -Daddonnames=&#34;tealiumiqaddon&#34;  `
  - `DaddonStorefront.yacceleratorstorefront=&#34;yacceleratorstorefront&#34;`
1. Update the following files:  
  * For `${HYBRIS_BIN\}/ext-template/yacceleratorstorefront/web/webroot/WEB-INF/tags/desktop/template/master.tag` by adding:&lt;br&gt;&amp;lt;%@ taglib prefix=&#34;tealiumiqaddon&#34; tagdir=&#34;/WEB-INF/tags/addons/tealiumiqaddon/shared/analytics&#34; %&amp;gt; at the top of the file.&lt;br&gt;&amp;lt;tealiumiqaddon:sync/&amp;gt; after the &amp;lt;head&amp;gt; tag&lt;br&gt;&amp;lt;tealiumiqaddon:tealium/&amp;gt; after the &amp;lt;body&amp;gt; tag
  * For `${HYBRIS_BIN}/custom/tealiumiqaddon/project.properties.template` by changing:  &lt;br&gt; **tealiumiqaddon.account**,**tealiumiqaddon.profile**, and **tealiumiqaddon.target** to your Tealium IQ account-specific information.&lt;br&gt;Modify `tealiumiqaddon.utagSyncEnabled = 1` if you want to enable `utag.sync.js` injection into the &amp;lt;head&amp;gt; of your HTML page. This feature is optional and disabled by default.

## Adding Custom Data

By default, the add on provides a comprehensive list of standard e-commerce variables. If these default values are not sufficient for your installation, you can extend the default page types as well as create new custom page types.

1. Create a new class implementing the interface `com.tealium.dataconnector.hybris.HybrisDataConverter.HybrisCustomDataConverter` and implement all methods of the interface.  
```
package com.tealium.dataconnector.hybris;
import com.tealium.dataconnector.hybris.HybrisDataConverter.HybrisCustomDataConverter;
import com.tealium.dataconnector.hybris.HybrisDataConverter.HybrisCustomPageTypeCustomData;
import com.tealium.util.udohelpers.UDO;
import com.tealium.util.udohelpers.exceptions.UDOUpdateException;
public class TealiumCustomData implements HybrisCustomDataConverter {
	// ... add unimplemented methods of interface.
}
```

1. If you are **NOT** adding values to any of the methods of the interface, make sure to return the `udo` object.
```
@Override
public UDO homePage(UDO udo) {
	return udo;
}
```

1. To add or modify values to a default page, add to the override method for that page.  
```
@Override
public UDO searchPage(UDO udo) {
	try {
		udo.setValue(&#34;page_name&#34;, &#34;new search page name&#34;);
		udo.setValue(&#34;custom_key&#34;, &#34;custom_value&#34;);
		} catch (UDOUpdateException e) {
			e.printStackTrace();
	    }
		return udo;
	 }
```

1. To add a new page type with values, add a static variable to your class and add new pages to the `addCustomPages` method:
```
public class TealiumCustomData implements HybrisCustomDataConverter {
private static Map&lt;String, HybrisCustomPageTypeCustomData&gt; customPagesMap;
@Override
public Map&lt;String, HybrisCustomPageTypeCustomData&gt; getHybrisCustomPageTypes() {
	return customPagesMap;
}
//... other methods
@Override
public void addCustomPages() {
	if (customPagesMap == null){
	    customPagesMap = new HashMap&lt;&gt;();
	}
		customPagesMap.put(&#34;custom_one&#34;, new HybrisCustomPageTypeCustomData(){
	@Override
	public UDO getCustomDataUdo(UDO udo) {
		try {
		     udo.setValue(&#34;page_name&#34;, &#34;custom page 1&#34;);
		     udo.setValue(&#34;custom_page1_key&#34;, &#34;custom value&#34;);
		    } catch (UDOUpdateException e) {
			e.printStackTrace();
		    }
		    return udo;
	        }
	});
	customPagesMap.put(&#34;custom_two&#34;, new HybrisCustomPageTypeCustomData(){
	@Override
	public UDO getCustomDataUdo(UDO udo) {
		try {
			udo.setValue(&#34;page_name&#34;, &#34;custom page 2&#34;);
			udo.setValue(&#34;custom_page2_key&#34;, &#34;custom value&#34;);
		    } catch (UDOUpdateException e) {
			e.printStackTrace();
		    }
		return udo;
		}
	});
	}
}
```

1. Modify:   
 `${HYBRIS_BIN\}/custom/tealiumiqaddonweb/webroot/WEB-INF/tags/addons/tealiumiqaddon/shared/analytics/data.tag`
  * Replace `CLASS_NAME` with your class name (for instance, `TealiumCustomData`)
  * Add your new class: &amp;lt;%@ tag import=&#34;com.tealium.dataconnector.hybris. CLASS_NAME &#34;%&amp;gt;
  * Register the new class with HybrisDataConverter: &amp;lt;%HybrisDataConverter.registerCustomDataClass(&#34;ID&#34;, new CLASS_NAME ()); %&amp;gt;

## Finish

Rebuild and restart hybris.

* `sudo ant all`
* `sudo ./hybrisserver.sh`

## Default data sources

### All Pages

|Source| Description|
|---| ---|
|`page_name`| Contains a user-friendly page name|
|`site_region`| Includes values for region or localized version, for example, `en_US`|
|`site_currency`| Contains the currency shown on site, for example, `USD`|
|`page_type`| Contains a user-friendly page type, for example, cart page|

### Search Page

|Source| Description|
|---| ---|
|`search_results`| Contains the number of results returned with a search query|
|`search_keyword`| Contains the search query conducted by user|

### Category Pages

|Source| Description|
|---| ---|
|`page_category_name`| Contains a user-friendly category name, for example, appliances|

### Product Page

|Source| Description|
|---| ---|
|`product_id`| Contains product ID(s); multiple values should be comma-separated|
|`product_sku`| Contains product SKU(s); multiple values should be comma-separated|
|`product_name`| Contains product name(s); multiple values should be comma-separated|
|`product_brand`| Contains product brand(s); multiple values should be comma-separated|
|`product_category`| Contains product category(s); multiple values should be comma-separated|
|`product_subcategory`| Contains product subcategory(s); multiple values should be comma-separated|
|`product_unit_price`| Contains product unit price(s); multiple values should be comma-separated|

### Cart Page

|Source| Description|
|---| ---|
|`product_id`| Contains product ID(s); multiple values should be comma-separated|
|`product_sku`| Contains product SKU(s); multiple values should be comma-separated|
|`product_name`| Contains product name(s); multiple values should be comma-separated|
|`product_brand`| Contains product brand(s); multiple values should be comma-separated|
|`product_category`| Contains product category(s); multiple values should be comma-separated|
|`product_subcategory`| Contains product subcategory(s); multiple values should be comma-separated|
|`product_unit_price`| Contains product unit price(s); multiple values should be comma-separated|
|`product_quantity`| Contains product quantity(s); multiple values should be comma-separated|

### Order Confirmation

|Source| Description|
|---| ---|
|`order_id`| Contains the order or transaction ID|
|`order_subtotal`| Contains the order payment type|
|`order_payment_type`| Contains the order payment type|
|`order_total`| Contains the order total value|
|`order_discount`| Contains the order discount (if any)|
|`order_shipping`| Contains the order shipping value|
|`order_tax`| Contains the order tax amount|
|`order_currency`| Contains the currency associated with the transaction, for example, USD&#39;|
|`order_coupon_code`| Contains the order coupon code|
|`order_type`| Contains the order/cart|
|`product_id`| Contains product ID(s); multiple values should be comma-separated|
|`product_sku`| Contains product SKU(s); multiple values should be comma-separated|
|`product_name`| Contains product name(s); multiple values should be comma-separated|
|`product_brand`| Contains product brand(s); multiple values should be comma-separated|
|`product_category`| Contains product category(s); multiple values should be comma-separated|
|`product_subcategory`| Contains product subcategory(s); multiple values should be comma-separated|
|`product_unit_price`| Contains product unit price(s); multiple values should be comma-separated|
|`product_quantity`| Contains product quantity(s); multiple values should be comma-separated|
|`customer_email`| Contains the customer email|

### Customer Info Page

|Source| Description|
|---| ---|
|`customer_name`| Contains the customer username|
|`customer_email`| Contains the customer email|
|`gender`| Contains the customer gender based on salutation|