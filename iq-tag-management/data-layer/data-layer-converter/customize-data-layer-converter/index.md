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
  "user" : 1,
  "util" : 1
};
```

This action will result in all keys from the source data object being skipped if they begin with the string "user" or "util".

### `teal.prefix`

Set the string to use to prefix all key names that are converted. For example, If you are merging `utag_data` and `dataLayer`, you can set the converted variables with a prefix of `dl_`. Using the `dataLayer` example from above, the converted object would contain: 

```json
{
   "dl_user.userInfo.sub_industry" : "data & technical services",
   "dl_user.userInfo.web_site"     : "tealium.com"
}
```

### `teal.nested_delimiter`

Set the character used to delimit the subkey names in the converted names. The default delimiter is the period character (**.**).

### `teal.replace_keys`

Specify new names for converted keys. You can either replace a key name with a new name or remove the key.

Example:  
```js
teal.replace_keys = {
    "pageInfo" : ""
};
```

 The source object contains `pageInfo`, which you want to appear as `pi` in the converted object, for example, `digitalData.page.pageInfo.pageName` changes to `digitalData.page.pi.pageName`.

