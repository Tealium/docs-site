---
title: Content Security Policy
description: This article lists the domains you need to add to your Content Security Policy (CSP).
url: https://docs.tealium.com/server-side/settings/tealium-content-security-policies-reference-guide/
---
## How it works

CSP (Content Security Policy) is a security feature that helps prevent malicious attacks like cross-site scripting (XSS). It does this by controlling the resources, such as scripts and images, that can be loaded and executed on a web page. To enforce these restrictions, CSP defines rules in HTTP headers or meta tags, limiting content sources and enhancing security.

For example, consider the following CSP directive:

```
Content-Security-Policy: default-src 'self'; script-src 'self' tealium.com;
```

* `default-src` instructs the visitor's browser to only load resources from the same origin as the document unless additional directives set different policies for specific resource types.
* `script-src` instructs the visitor’s browser to load scripts only from the same origin as the document. It also allows scripts from `tealium.com`.

For each Tealium product or service you use, add its data center domains to your CSP. This ensures that your site visitors can load the necessary scripts. Also, add the domains of any vendors loaded through Tealium iQ Tag Management.


<blockquote>
Each list includes all data center domains that may be used in the future.
</blockquote>


For more information about CSP, see [MDN: Content Security Policy](https://developer.mozilla.org/en-US/docs/Web/HTTP/CSP).

## Tealium iQ Tag Management

Add the following iQ Tag Management data center domains to your CSP:

```
tags.tiqcdn.com
tags.tiqcdn.cn
tags-eu.tiqcdn.com
```

## Tealium Collect Tag, AudienceStream and EventStream

Add the following Tealium Collect Tag, Tealium AudienceStream and Tealium EventStream data center domains to your CSP:

```
collect-ap-east-1.tealiumiq.com 
collect-ap-northeast-1.tealiumiq.com 
collect-ap-northeast-2.tealiumiq.com 
collect-ap-northeast-3.tealiumiq.com 
collect-ap-southeast-1.tealiumiq.com 
collect-ap-southeast-2.tealiumiq.com 
collect-ap-south-1.tealiumiq.com 
collect-ca-central-1.tealiumiq.com 
collect-eu-central-1.tealiumiq.com 
collect-eu-west-1.tealiumiq.com 
collect-eu-west-2.tealiumiq.com 
collect-eu-west-3.tealiumiq.com 
collect-sa-east-1.tealiumiq.com 
collect-us-east-1.tealiumiq.com 
collect-us-east-2.tealiumiq.com 
collect-us-west-1.tealiumiq.com 
collect-us-west-2.tealiumiq.com
collect.tealiumiq.com
```

### Private cloud environments

If you use a private cloud environment, be sure to add that site to your CSP. For example, to add the PC HMT Collect environment, add the following domain to your CSP:

```
pc-hmt-collect.tealiumiq.com
```

## Data layer enrichment

Add the following Tealium Data Layer Enrichment data center domains to your CSP:

```
visitor-service-ap-east-1.tealiumiq.com
visitor-service-ap-northeast-1.tealiumiq.com 
visitor-service-ap-northeast-2.tealiumiq.com 
visitor-service-ap-northeast-3.tealiumiq.com 
visitor-service-ap-southeast-1.tealiumiq.com 
visitor-service-ap-southeast-2.tealiumiq.com 
visitor-service-ap-south-1.tealiumiq.com 
visitor-service-ca-central-1.tealiumiq.com 
visitor-service-eu-central-1.tealiumiq.com 
visitor-service-eu-west-1.tealiumiq.com 
visitor-service-eu-west-2.tealiumiq.com 
visitor-service-eu-west-3.tealiumiq.com 
visitor-service-sa-east-1.tealiumiq.com
visitor-service-us-east-1.tealiumiq.com 
visitor-service-us-east-2.tealiumiq.com 
visitor-service-us-west-1.tealiumiq.com 
visitor-service-us-west-2.tealiumiq.com
visitor-service.tealiumiq.com
```

## Tealium API

Add the following Tealium API data center domain to your CSP:

```
api.tealiumiq.com
```