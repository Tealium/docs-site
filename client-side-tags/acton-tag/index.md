---
title: ActOn Tag Setup Guide
description: This article describes how to set up the ActOn tag in your Tealium iQ Tag Management account.
url: https://docs.tealium.com/client-side-tags/acton-tag/
---
## Website

[www.act-on.com](https://www.act-on.com)

## Sample code snippet

```javascript
&lt;script type=&#34;text/javascript&#34;&gt;
    /* &lt;![CDATA[ */
    document.write (
        &#39;&lt;img src=&#34;http://www.tealium.com/acton/bn/1234/visitor.gif?ts=&#39;&#43;new Date().getTime()&#43;&#39;&amp;ref=&#39;&#43;escape(document.referrer) &#43; &#39;&#34;&gt;&#39;
    );
    /* ]]&gt; */
 &lt;/script&gt; 
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
 