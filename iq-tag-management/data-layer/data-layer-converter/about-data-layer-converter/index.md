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
    &#34;page&#34;: {
        &#34;pageInfo&#34;: {
            &#34;effectiveDate&#34;: &#34;2018-10-01&#34;,
            &#34;expiryDate&#34;: &#34;2020-12-18&#34;,
            &#34;language&#34;: &#34;en-US&#34;,
            &#34;publishDate&#34;: &#34;2018-10-01&#34;,
            &#34;publisher&#34;: &#34;Company&#34;,
            &#34;version&#34;: &#34;v1.0&#34;,
            &#34;pageHeader&#34;: &#34;Lorem ipsum dolor sit amet, consectetur adipisicing elit&#34;,
            &#34;description&#34;: &#34;sed do eiusmod tempor incididunt ut labore et dolore magna aliqua&#34;,
            &#34;keywords&#34;: &#34;TEST&#34;,
            &#34;pageName&#34;: &#34;Homepage&#34;
        },
        &#34;attribute&#34;: {
            &#34;jQueryNativeVersion&#34;: &#34;2.2.4&#34;
        },
        &#34;session&#34;: {
            &#34;pageloadEpoch&#34;: 1488329663998,
            &#34;uSessionID&#34;: &#34;015a68b867ae0013994e512cb7a304078002307000c48-1488309121962&#34;,
            &#34;uPageViewID&#34;: &#34;6c595d7e22985ff86351edd694241cb7d0cf84a4195635b1d5392e1d31df1047&#34;
        }
    },
    &#34;user&#34;: {
        &#34;userInfo&#34;: {
            &#34;browser_lang&#34;: &#34;en-us&#34;,
            &#34;ipcinfo&#34;: &#34;en-us&#34;,
            &#34;signedin&#34;: false,
            &#34;city&#34;: &#34;del mar&#34;,
            &#34;company_name&#34;: &#34;tealium inc&#34;,
            &#34;country&#34;: &#34;us&#34;,
            &#34;country_name&#34;: &#34;united states&#34;,
            &#34;employee_count&#34;: &#34;n/a&#34;,
            &#34;industry&#34;: &#34;software &amp; technology&#34;,
            &#34;information_level&#34;: &#34;detailed&#34;,
            &#34;marketing_alias&#34;: &#34;tealium&#34;,
            &#34;phone&#34;: &#34;858-779-1344&#34;,
            &#34;registry_city&#34;: &#34;san diego&#34;,
            &#34;registry_country_code&#34;: &#34;us&#34;,
            &#34;registry_state&#34;: &#34;ca&#34;,
            &#34;state&#34;: &#34;ca&#34;,
            &#34;stock_ticker&#34;: &#34;n/a&#34;,
            &#34;sub_industry&#34;: &#34;data &amp; technical services&#34;,
            &#34;web_site&#34;: &#34;tealium.com&#34;
        }
    }
}
```

## Example: Converted Object

After using the data layer converter, the flattened Tealium `utag_data` object looks like this:

```json
{
    &#34;page.pageInfo.effectiveDate&#34;: &#34;2018-10-01&#34;,
    &#34;page.pageInfo.expiryDate&#34;: &#34;2020-12-18&#34;,
    &#34;page.pageInfo.language&#34;: &#34;en-US&#34;,
    &#34;page.pageInfo.publishDate&#34;: &#34;2018-10-01&#34;,
    &#34;page.pageInfo.publisher&#34;: &#34;Company&#34;,
    &#34;page.pageInfo.version&#34;: &#34;v1.0&#34;,
    &#34;page.pageInfo.pageHeader&#34;: &#34;Lorem ipsum dolor sit amet, consectetur adipisicing elit&#34;,
    &#34;page.pageInfo.description&#34;: &#34;sed do eiusmod tempor incididunt ut labore et dolore magna aliqua&#34;,
    &#34;page.pageInfo.keywords&#34;: &#34;TEST&#34;,
    &#34;page.pageInfo.pageName&#34;: &#34;Homepage&#34;,
    &#34;page.attribute.jQueryNativeVersion&#34;: &#34;2.2.4&#34;,
    &#34;page.session.pageloadEpoch&#34;: &#34;1488329663998&#34;,
    &#34;page.session.uSessionID&#34;: &#34;015a68b867ae0013994e512cb7a304078002307000c48-1488309121962&#34;,
    &#34;page.session.uPageViewID&#34;: &#34;6c595d7e22985ff86351edd694241cb7d0cf84a4195635b1d5392e1d31df1047&#34;,
    &#34;user.userInfo.browser_lang&#34;: &#34;en-us&#34;,
    &#34;user.userInfo.ipcinfo&#34;: &#34;en-us&#34;,
    &#34;user.userInfo.signedin&#34;: &#34;false&#34;,
    &#34;user.userInfo.city&#34;: &#34;del mar&#34;,
    &#34;user.userInfo.company_name&#34;: &#34;tealium inc&#34;,
    &#34;user.userInfo.country&#34;: &#34;us&#34;,
    &#34;user.userInfo.country_name&#34;: &#34;united states&#34;,
    &#34;user.userInfo.employee_count&#34;: &#34;n/a&#34;,
    &#34;user.userInfo.industry&#34;: &#34;software &amp; technology&#34;,
    &#34;user.userInfo.information_level&#34;: &#34;detailed&#34;,
    &#34;user.userInfo.marketing_alias&#34;: &#34;tealium&#34;,
    &#34;user.userInfo.phone&#34;: &#34;858-779-1344&#34;,
    &#34;user.userInfo.registry_city&#34;: &#34;san diego&#34;,
    &#34;user.userInfo.registry_country_code&#34;: &#34;us&#34;,
    &#34;user.userInfo.registry_state&#34;: &#34;ca&#34;,
    &#34;user.userInfo.state&#34;: &#34;ca&#34;,
    &#34;user.userInfo.stock_ticker&#34;: &#34;n/a&#34;,
    &#34;user.userInfo.sub_industry&#34;: &#34;data &amp; technical services&#34;,
    &#34;user.userInfo.web_site&#34;: &#34;tealium.com&#34;
}
```
