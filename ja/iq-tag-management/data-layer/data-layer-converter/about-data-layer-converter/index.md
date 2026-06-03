---
title: データレイヤーコンバーターについて
description: データレイヤーコンバーターを使用すると、ネストされたデータレイヤーオブジェクトを保持し、それをiQタグ管理が期待するフラットフォーマットに変換することができます。
url: https://docs.tealium.com/ja/iq-tag-management/data-layer/data-layer-converter/about-data-layer-converter/
---
データレイヤーコンバーターは、`digitalData`（W3C）や`dataLayer`（Google Tag Manager）のようなネストされたデータオブジェクトを取り、それを文字列または文字列の配列のオブジェクトにフラット化します。ウェブサイトにデータレイヤーを実装する方法はいくつかあり、その中にはネストされたオブジェクトや配列を使用するものもあります。これらの形式は複雑なデータを表現するのに役立つことがありますが、iQタグ管理とはうまく機能しません。iQタグ管理は、`utag_data`内のデータがフラットであることを期待しています。つまり、それは文字列、数値、および文字列または数値の配列のみを含むことを意味します。

## 例：digitalData

以下の例は、データレイヤーコンバーターを使用する前のネストされたオブジェクトを持つdigitalDataオブジェクトを示しています：

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

## 例：変換されたオブジェクト

データレイヤーコンバーターを使用した後、フラット化されたTealiumの`utag_data`オブジェクトは次のようになります：

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

