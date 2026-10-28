---
title: How your account is organized
description: Learn how your Tealium account organizes tag management and server-side configuration into profiles, and how saved changes become live.
url: https://docs.tealium.com/get-started/how-your-account-is-organized/
---
Your organization has one Tealium account. Inside the account, profiles hold your configuration. Tag management and server-side features use separate profiles, and each type has its own versions and publishing.

## Profiles store your configuration

An account profile is the configuration for a website, a mobile application, a region, or a brand within your account.


![](https://docs.tealium.com/images/icons/icon-users.svg)

#### Account organization

Learn how accounts, profiles, and versions fit together.


## Server-side profiles

A server-side profile receives events from all your data sources, including websites, mobile apps, servers, and files. Several tag management profiles can send data to one server-side profile, so all your websites and apps build one set of visitor profiles. The server-side profile holds your data sources, attributes, audiences, connectors, and functions.


![](https://docs.tealium.com/images/icons/icon-sitemap-light.svg)

#### Server-side overview

Learn how server-side profiles collect, enrich, and activate customer data.



![](https://docs.tealium.com/images/icons/icon-cubes-check.svg)

#### Save and publish

Save versions of a server-side profile and publish them to production.


## Tag management profiles

A tag management profile usually corresponds to one website, a group of websites with the same tagging needs, or one mobile app. The profile holds the tags and the data layer for that website or app.

When you save changes to a tag management profile, Tealium creates a new version. Publishing a version regenerates the profile files and makes your changes available in an environment. Each profile has three default environments: Dev, QA, and Prod. Test changes in Dev or QA before you publish to Prod.


![](https://docs.tealium.com/images/icons/icon-cubes.svg)

#### Tag management profiles

Learn how tag management profiles map to your websites and mobile apps.



![](https://docs.tealium.com/images/icons/icon-cubes-check.svg)

#### Publishing

Publish a profile version to make your tag management changes live.


