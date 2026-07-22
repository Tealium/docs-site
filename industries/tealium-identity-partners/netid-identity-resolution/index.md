---
title: netID Implementation Guide
description: This article describes how to implement netID as a Tealium Identity Partner.
url: https://docs.tealium.com/industries/tealium-identity-partners/netid-identity-resolution/
---
First-party data, such as a netID, is crucial for accurate retargeting and personalization. The Tealium real-time first-party data platform helps activate these identifiers across channels, enhancing the effectiveness of advertising campaigns.

## Prerequisites

* A request to the netID browser-based JavaScript API
* Tealium EventStream or AudienceStream 

## How it works

When integrating netID’s Single Sign-On (SSO) and consent management solutions, netID partners must implement a request to the netID browser-based JavaScript API. The properties returned from the API must be persisted in the browser session as first-party cookies, in `localStorage`, or in `sessionStorage`.

NetID properties like `tpid` can be used with client-side tags in Tealium iQ to integrate with advertising technologies on your webpage.

Additionally, the same netID properties are collected by the Tealium Collect tag and made available as attributes in EventStream and AudienceStream. With netID saved as a visitor attribute, the visitor profiles can then be activated through real-time connectors to advertising vendors.

For more information about the netID browser-based JavaScript API, see the following:

* [netID: The data points returned from the API](https://developerzone.netid.dev/1.6/cmp/browser-based/#response)
* [netID: Response properties descriptions](https://developerzone.netid.dev/1.6/cmp/browser-based/#response-properties)

## Tealium iQ

netID properties that have been stored in the browser can be fetched as part of the data layer (UDO object). This data can then be used in Tealium iQ load rules and tag data mappings where relevant.

For example, if you’ve persisted the netID `tpid` parameter in a first-party cookie, add a new variable of type **First-Party Cookie** in the data layer, and set the value for **Source** to the cookie’s name (for example, `netid_tpid`).

![](https://docs.tealium.com/images/industries/netid-add-variable.png)

As a netID partner, use one of the following methods to include netID’s properties as key-value pairs in the Tealium Data Layer:

* **First-Party-Cookie**: Persist the netID `tpid` as a [first-party-cookie](https://docs.tealium.com/platforms/javascript/data-layer/#cookies) named `netid_tpid` in the browser, and it will appear in the data layer with the `cp.` prefix alongside Tealium standard cookies:

  ```
  {
    ...,
    "cp.netid_tpid": "Bst040QDNr1nB9JM6sWH0I9__70JEvRyIiKvvd7G0MQLQ",
    ...
  }
  ```

* **Universal Data Object (UDO)**: Use a [UDO variable](https://docs.tealium.com/iq-tag-management/data-layer/data-layer-variables/#udo-variable) to explicitly persist the netID property in `utag_data`. For example, add the netID identity property as `netid_tpid` to the UDO of your pages:

  ```js
  <script type="text/javascript">
    var utag_data={
        "tealium_event" : "page_view",
        "page_name"     : "product_page",
        "product_id"    : "423543",
        "netid_tpid"    : "12345"
      };
  </script>
  ```

* **Track an event**: Use [`utag.link()`](https://docs.tealium.com/platforms/javascript/track/#track-events) to track a successful netID authentication and response from the browser-based JavaScript API, and include the netID `tpid` as `netid_tpid` in the payload:

  ```json
  utag.link({
    "tealium_event"     : "netid_login",
    "netid_tpid"        : "12345",
    ...
  });
  ```

## EventStream API

After the Tealium Collect Tag captures netID properties from the browser’s data layer, this data is processed as event attributes.

To do this, create an event attribute to capture the `netid_tpid` value. In the following example, the attribute is set to the value of the first-party cookie:

![](https://docs.tealium.com/images//industries/netid-es-add-attribute.png)

netID's identifier (`tpid`) can be activated as a first-party (Advertiser) ID to an advertising platform using their connector, such as:

* [Adform](https://docs.tealium.com/server-side-connectors/adform-segments-connector/)
* [The Trade Desk](https://docs.tealium.com/server-side-connectors/the-trade-desk-first-party-data-connector/)

### Example

If you use Adform, map the `netid_tpid` event attribute to Adform’s First-Party ID attribute:

![](https://docs.tealium.com/images//industries/netid-es-attribute-mapping.png)

## AudienceStream CDP

This data is processed as event attributes and can be stored as visitor attributes on the real-time visitor profile.

To do this, set a visitor string attribute on the visitor profile to the `netid_tpid` event attribute value. In the following example, the attribute is set to the value of the first-party cookie:

![](https://docs.tealium.com/images//industries/netid-as-add-attribute.png)

The visitor ID can then be used to create audiences for visitors using netID as their authentication method.

![](https://docs.tealium.com/images//industries/netid-as-new-audience.png)

For real-time activation to advertising platforms such as Adform and The Trade Desk, use their Tealium connectors:

* [Adform](https://docs.tealium.com/server-side-connectors/adform-segments-connector/)
* [The Trade Desk](https://docs.tealium.com/server-side-connectors/the-trade-desk-first-party-data-connector/)

## References

* [netID: Browser-Based JavaScript API](https://developerzone.netid.dev/1.6/cmp/browser-based/)
* [Adform: Segments Connector](https://docs.tealium.com/server-side-connectors/adform-segments-connector/)
* [Adform: Using First Party IDs](https://www.adformhelp.com/hc/en-us/articles/9740579323153-Use-First-Party-IDs-for-Site-Tracking)
* [The Trade Desk First Party Data Connector](https://docs.tealium.com/server-side-connectors/the-trade-desk-first-party-data-connector/)
* [Tealium Data Layer](https://docs.tealium.com/iq-tag-management/data-layer/about-the-data-layer/)
