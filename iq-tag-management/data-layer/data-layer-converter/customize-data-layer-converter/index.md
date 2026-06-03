---
title: Customize the data layer converter
url: https://docs.tealium.com/iq-tag-management/data-layer/data-layer-converter/customize-data-layer-converter/
---
Customize the behavior of the converter using the following utility functions:

### `teal.ignore_keys`

Specify the strings of text that, if a key in the object starts with this text, that key will not be ingested. 

Example Object:  
```js
teal.ignore_keys = {
  &#34;user&#34; : 1,
  &#34;util&#34; : 1
};
```

This action will result in all keys from the source data object being skipped if they begin with the string &#34;user&#34; or &#34;util&#34;.

### `teal.prefix`

Set the string to use to prefix all key names that are converted. For example, If you are merging `utag_data` and `dataLayer`, you can set the converted variables with a prefix of `dl_`. Using the `dataLayer` example from above, the converted object would contain: 

```json
{
   &#34;dl_user.userInfo.sub_industry&#34; : &#34;data &amp; technical services&#34;,
   &#34;dl_user.userInfo.web_site&#34;     : &#34;tealium.com&#34;
}
```

### `teal.nested_delimiter`

Set the character used to delimit the subkey names in the converted names. The default delimiter is the period character (**.**).

### `teal.replace_keys`

Specify new names for converted keys. You can either replace a key name with a new name or remove the key.

Example:  
```js
teal.replace_keys = {
    &#34;pageInfo&#34; : &#34;&#34;
};
```

 The source object contains `pageInfo`, which you want to appear as `pi` in the converted object, for example, `digitalData.page.pageInfo.pageName` changes to `digitalData.page.pi.pageName`.

