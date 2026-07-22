---
title: ActOn Tag Setup Guide
description: This article describes how to set up the ActOn tag in your Tealium iQ Tag Management account.
url: https://docs.tealium.com/client-side-tags/acton-tag/
---
## Website

[www.act-on.com](https://www.act-on.com)

## Sample code snippet

```javascript
<script type="text/javascript">
    /* <![CDATA[ */
    document.write (
        '<img src="http://www.tealium.com/acton/bn/1234/visitor.gif?ts='+new Date().getTime()+'&ref='+escape(document.referrer) + '">'
    );
    /* ]]> */
 </script> 
```

## Tealium iQ Configuration

The ActOn tag requires little in the way of configuration.

1. Navigate to the Tags tab, and click **Add Tag**.
1. Search for **Act On**.
1. Add the ActOn tag by clicking the **Add** button
1. In the **Tag Configuration Wizard**, give the new Act On tag a title that is meaningful to you.
1. Enter your Account ID.
1. Enter the Path (the URL path leading to your account id, for example, `http:www/tealium.com/acton/bn/1234/visitor.gif?`).
1. Click **Next** to assign a specific Load Rule to the tag or click **Finish** to apply the default load rule to this tag.
 