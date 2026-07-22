---
title: About the data layer converter
description: The data layer converter lets you keep a nested data layer object and convert it to the flat format expected by iQ Tag Management.
url: https://docs.tealium.com/iq-tag-management/data-layer/data-layer-converter/about-data-layer-converter/
---
 The data layer converter takes a nested data object, such as `digitalData` (W3C) or `dataLayer` (Google Tag Manager), and flattens it into an object of strings or arrays of strings. There are different ways to implement a data layer on your website, some of which use nested objects and arrays. These formats can be helpful in representing complex data, but do not work well with iQ Tag Management. iQ Tag Management expects the data in `utag_data` to be flat, meaning that it contains only values of type strings, numbers, and arrays of strings or numbers.

## Example: digitalData

The following example shows a digitalData object with nested objects before using the data layer converter:

```json
{
    "page": {
        "pageInfo": {
            "effectiveDate": "2018-10-01",
            "expiryDate": "2020-12-18",
            "language": "en-US",
            "publishDate": "2018-10-01",
            "publisher": "Company",
            "version": "v1.0",
            "pageHeader": "Lorem ipsum dolor sit amet, consectetur adipisicing elit",
            "description": "sed do eiusmod tempor incididunt ut labore et dolore magna aliqua",
            "keywords": "TEST",
            "pageName": "Homepage"
        },
        "attribute": {
            "jQueryNativeVersion": "2.2.4"
        },
        "session": {
            "pageloadEpoch": 1488329663998,
            "uSessionID": "015a68b867ae0013994e512cb7a304078002307000c48-1488309121962",
            "uPageViewID": "6c595d7e22985ff86351edd694241cb7d0cf84a4195635b1d5392e1d31df1047"
        }
    },
    "user": {
        "userInfo": {
            "browser_lang": "en-us",
            "ipcinfo": "en-us",
            "signedin": false,
            "city": "del mar",
            "company_name": "tealium inc",
            "country": "us",
            "country_name": "united states",
            "employee_count": "n/a",
            "industry": "software & technology",
            "information_level": "detailed",
            "marketing_alias": "tealium",
            "phone": "858-779-1344",
            "registry_city": "san diego",
            "registry_country_code": "us",
            "registry_state": "ca",
            "state": "ca",
            "stock_ticker": "n/a",
            "sub_industry": "data & technical services",
            "web_site": "tealium.com"
        }
    }
}
```

## Example: Converted Object

After using the data layer converter, the flattened Tealium `utag_data` object looks like this:

```json
{
    "page.pageInfo.effectiveDate": "2018-10-01",
    "page.pageInfo.expiryDate": "2020-12-18",
    "page.pageInfo.language": "en-US",
    "page.pageInfo.publishDate": "2018-10-01",
    "page.pageInfo.publisher": "Company",
    "page.pageInfo.version": "v1.0",
    "page.pageInfo.pageHeader": "Lorem ipsum dolor sit amet, consectetur adipisicing elit",
    "page.pageInfo.description": "sed do eiusmod tempor incididunt ut labore et dolore magna aliqua",
    "page.pageInfo.keywords": "TEST",
    "page.pageInfo.pageName": "Homepage",
    "page.attribute.jQueryNativeVersion": "2.2.4",
    "page.session.pageloadEpoch": "1488329663998",
    "page.session.uSessionID": "015a68b867ae0013994e512cb7a304078002307000c48-1488309121962",
    "page.session.uPageViewID": "6c595d7e22985ff86351edd694241cb7d0cf84a4195635b1d5392e1d31df1047",
    "user.userInfo.browser_lang": "en-us",
    "user.userInfo.ipcinfo": "en-us",
    "user.userInfo.signedin": "false",
    "user.userInfo.city": "del mar",
    "user.userInfo.company_name": "tealium inc",
    "user.userInfo.country": "us",
    "user.userInfo.country_name": "united states",
    "user.userInfo.employee_count": "n/a",
    "user.userInfo.industry": "software & technology",
    "user.userInfo.information_level": "detailed",
    "user.userInfo.marketing_alias": "tealium",
    "user.userInfo.phone": "858-779-1344",
    "user.userInfo.registry_city": "san diego",
    "user.userInfo.registry_country_code": "us",
    "user.userInfo.registry_state": "ca",
    "user.userInfo.state": "ca",
    "user.userInfo.stock_ticker": "n/a",
    "user.userInfo.sub_industry": "data & technical services",
    "user.userInfo.web_site": "tealium.com"
}
```
