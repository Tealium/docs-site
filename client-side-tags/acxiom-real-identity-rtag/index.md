---
title: Acxiom Real Identity rTag Setup Guide
description: This article describes how to set up the Acxiom Real Identity rTag tag in your Tag Management account.
url: https://docs.tealium.com/client-side-tags/acxiom-real-identity-rtag/
---
rTAG provides the ability to flexibly instrument digital channels with data collection capabilities, identity generation and association, privacy governance and containers for managing invocation of partner tags.

## Tag tips

* Use mappings to override or dynamically set the tag configurations.

## Tag configuration

Go to the tag marketplace to add a new tag. For more information, see [About tags](https://docs.tealium.com/about-tags/).

When adding the tag, configure the following settings:

* **Domain Name**: A subdomain of the client’s domain name with a CNAME that much be changed to rTAG.
* **ESI toggle**: (Optional) Top level directory indicates whether ESI is enabled.   
  * **1** — Indicates files are processed for ESI directly.  
  * **2** — Indicates that ESI files are gzipped and cached after being generated.
* **Logging Mode**: Logging mode based on the logging requirements of the client.
* **Tag Type**: The filename of the object to be received.

## Load rules

Load the tag on all pages or set conditions for when your tag will load. For more information about load rules, see the [Load Rules](https://docs.tealium.com/about-load-rules/) documentation.

## Data mappings

Data mappings send values from data layer variables to the corresponding variables in the vendor tag. For more information, see [About data mappings](https://docs.tealium.com/about-data-mappings/).

The available categories are:

### Tag configuration

| Variable                      | Description |
|:------------------------------|:------------|
| Domain name (`domain_name`)   | [String]    |
| ESI toggle (`esi_toggle`)     | [String]    |
| Logging mode (`logging_mode`) | [String]    |
| Tag type (`tag_type`)         | [String]    |

### Standard

| Variable                                                                                                        | Description |
|:----------------------------------------------------------------------------------------------------------------|:------------|
| Cache buster, typically set to a random number or timestamp (`r`)                                               | [String]    |
| Encoded URL destination for a 302-redirect directive (`ru`)                                                     | [String]    |
| Event ID (`evid`)                                                                                               | [String]    |
| Session ID (`s`)                                                                                                | [String]    |
| Domain (`dmn`)                                                                                                  | [String]    |
| Path with filename (`pn`)                                                                                       | [String]    |
| Query string of the URL (`qs`)                                                                                  | [String]    |
| Domain of the referring page (`rdn`)                                                                            | [String]    |
| Path with filename of referring page (`rpn`)                                                                    | [String]    |
| Query string of the URL of referring page (`rqs`)                                                               | [String]    |
| Unique user agent/user/browser identifier, which can be from a cookie, a statistical ID, or other source (`uu`) | [String]    |
| Statistical id (`suu`)                                                                                          | [String]    |
| The specific class tag configuration to be used (`cls`)                                                         | [String]    |
| Publisher or site identifier (`pubid`)                                                                          | [String]    |
| Partner unique identifier (`puu`)                                                                               | [String]    |
| Payload passed by client in clientObject (`payload`)                                                            | [String]    |
| Advertising agency identifier (`ag`)                                                                            | [String]    |
| Advertiser or marketer identifier (`adv`)                                                                       | [String]    |
| Campaign identifier (`ca`)                                                                                      | [String]    |
| Creative identifier (`cr`)                                                                                      | [String]    |
| List of user segments (`sg`)                                                                                    | [String]    |
| Comma separated list of entity types (`aqet`)                                                                   | [String]    |
| Client-determined variable 0 (`v0`)                                                                             | [String]    |
| Client-determined variable 1 (`v1`)                                                                             | [String]    |
| Client-determined variable 2 (`v2`)                                                                             | [String]    |
| Client-determined variable 3 (`v3`)                                                                             | [String]    |
| Client-determined variable 4 (`v4`)                                                                             | [String]    |
| Client-determined variable 5 (`v5`)                                                                             | [String]    |
| Client-determined variable 6 (`v6`)                                                                             | [String]    |
| Client-determined variable 7 (`v7`)                                                                             | [String]    |
| Client-determined variable 8 (`v8`)                                                                             | [String]    |
| Client-determined variable 9 (`v9`)                                                                             | [String]    |
