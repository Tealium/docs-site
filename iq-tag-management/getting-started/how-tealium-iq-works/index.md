---
title: How Tealium iQ works
url: https://docs.tealium.com/iq-tag-management/getting-started/how-tealium-iq-works/
---

* Client-side technology that leverages the speed and reliability of web browsers and the JavaScript language.
* Globally-scaled server infrastructure to ensure the fastest delivery of files.
* Tag vendor integrations.

## Client-side approach

Tealium iQ Tag Management distinguishes itself from other solutions as being a client-side solution. Most tag managers rely on an application server to facilitate the execution of tags in their system. An application server determines which tags to load and how to run them, then sends this configuration back to the browser on every page load. A more scalable and optimized approach is to bypass the application server and provide all the tag configuration logic from a static JavaScript file that can be processed solely by the browser.

In iQ Tag Management, your vendor tag configuration and business logic is represented in JavaScript code that resides inside the main client-side library called `utag.js`. As visitors browse your site, this file is loaded and, within the browser itself (the client-side), determines which additional vendor tags to load and how to send their data. Once these files have been retrieved by the browser, they are cached for subsequent page views to optimize network traffic and page performance.

## Content delivery network (CDN)

A CDN is a collection of servers spread across the globe designed to serve content from locations in close proximity to users.  Tealium has optimized its infrastructure to ensure that our files are served as fast as possible.

### Tag vendor integrations

We have looked at countless tag vendor solutions and developed turn-key integrations in iQ Tag Management that make it simple to add and set up tags. Most tags generally have three types of requirements:

* settings and options
* data mappings
* load rules

Each time you add a tag, you will go through these same three configuration steps. Behind the scenes of the user interface, our integrations will take care of the complicated specifics of each vendor's tagging code to ensure it runs as expected. This means you are free to focus on the high-level details of when and where to load tags and what data they should receive while the tag handles the technical details of the vendor's requirements.

## Data privacy and tracking

The Tealium Universal Tag (`utag.js`) is a container tag for  loading other JavaScript files or running custom JavaScript code. The `tags.tiqcdn.com` domain does not collect the IP address or any data about the users of the sites where it is loaded.


<blockquote>
Users that block requests to `tags.tiqcdn.com` might experience broken site functionality.
</blockquote>


Only clients who have also implemented the [Tealium Collect tag](https://docs.tealium.com/tealium-collect-tag/) will cause data to be collected by Tealium. To block data collection by Tealium, add a filter to block outgoing requests to `//collect*.tealiumiq.com`.

To block data collection by third-party vendors, add a filter specific to the data collection endpoint for that service.
