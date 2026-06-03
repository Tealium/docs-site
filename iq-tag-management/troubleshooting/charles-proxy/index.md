---
title: Enhanced browser console debugging with Charles Proxy
description: This article demonstrates how to use Charles Proxy to obtain more advanced output from utag.DB.
url: https://docs.tealium.com/iq-tag-management/troubleshooting/charles-proxy/
---
By adding a rewrite setting to Charles Proxy, the regular errors from `utag.DB` will be displayed as browser level console warnings. This allows for the **Warnings** filter in the console to be used when filtering errors, warnings, and info output.

## Prerequisites

* [Charles Proxy Web Debugging Application](https://www.charlesproxy.com/download/) installed on your computer.
* [utag.DB output](/platforms/javascript/debugging/) is enabled in the browser.

## Create rewrite rules from XML file

1. Save the following XML as a file on your computer.  
    
    ```xml
    &lt;?xml version=&#39;1.0&#39; encoding=&#39;UTF-8&#39; ?&gt;
    &lt;?charles serialisation-version=&#39;2.0&#39; ?&gt;
    &lt;rewriteSet-array&gt;
      &lt;rewriteSet&gt;
        &lt;active&gt;true&lt;/active&gt;
        &lt;name&gt;uTag DB Upgrade&lt;/name&gt;
        &lt;hosts&gt;
          &lt;locationPatterns&gt;
            &lt;locationMatch&gt;
              &lt;location&gt;
                &lt;path&gt;/*/utag.js&lt;/path&gt;
              &lt;/location&gt;
              &lt;enabled&gt;true&lt;/enabled&gt;
            &lt;/locationMatch&gt;
          &lt;/locationPatterns&gt;
        &lt;/hosts&gt;
        &lt;rules&gt;
          &lt;rewriteRule&gt;
            &lt;active&gt;true&lt;/active&gt;
            &lt;ruleType&gt;7&lt;/ruleType&gt;
            &lt;matchValue&gt;;utag.o[&amp;apos;&lt;/matchValue&gt;
            &lt;matchHeaderRegex&gt;false&lt;/matchHeaderRegex&gt;
            &lt;matchValueRegex&gt;false&lt;/matchValueRegex&gt;
            &lt;matchRequest&gt;false&lt;/matchRequest&gt;
            &lt;matchResponse&gt;true&lt;/matchResponse&gt;
            &lt;newValue&gt;; utag.ut.typeOf = function(e) {return ({}).toString.call(e).match(/\s([a-zA-Z]&#43;)/)[1].toLowerCase();}; utag.DB = function(a, b) {   var t;   if (utag.cfg.utagdb === false) {     return;   } else if (typeof utag.cfg.utagdb == &amp;quot;undefined&amp;quot;) {     utag.db_log = [];     b = document.cookie &#43; &amp;apos;&amp;apos;;     utag.cfg.utagdb = ((b.indexOf(&amp;apos;utagdb=true&amp;apos;) &amp;gt;= 0) ? true : false);   }   if (utag.cfg.utagdb === true) {     var con = window.console;     if (utag.ut.typeOf(a) === &amp;quot;error&amp;quot;) {       utag.db_log.push(a);       t = &amp;quot;&amp;quot;;       if (a.stack &amp;amp;&amp;amp; a.stack.split) {         t = a.stack.split(&amp;quot;\n&amp;quot;)[1].replace(/^[\s\uFEFF\xA0]&#43;|[\s\uFEFF\xA0]&#43;$/g, &amp;apos;&amp;apos;).replace(/^at\s/, &amp;quot;&amp;quot;);       }       if (con) {         t = &amp;quot;utag - Error : &amp;quot; &#43; t &#43; &amp;quot; &amp;quot;&#43; a.message;         if (con.warn) {           con.warn(t);         } else if (con.log){           con.log(t);         }       }     } else {       t = (utag.ut.typeOf(a) == &amp;quot;object&amp;quot;) ? utag.handler.C(a) : a;       utag.db_log.push(t);       if (con &amp;amp;&amp;amp; con.log) con.log(&amp;quot;utag - &amp;quot;, t);     }   } };utag.o[&amp;apos;  &lt;/newValue&gt;
            &lt;newHeaderRegex&gt;false&lt;/newHeaderRegex&gt;
            &lt;newValueRegex&gt;false&lt;/newValueRegex&gt;
            &lt;matchWholeValue&gt;false&lt;/matchWholeValue&gt;
            &lt;caseSensitive&gt;false&lt;/caseSensitive&gt;
            &lt;replaceType&gt;1&lt;/replaceType&gt;
          &lt;/rewriteRule&gt;
          &lt;rewriteRule&gt;
            &lt;active&gt;true&lt;/active&gt;
            &lt;ruleType&gt;7&lt;/ruleType&gt;
            &lt;matchValue&gt;\}catch\((.*?)\)\{&lt;/matchValue&gt;
            &lt;matchHeaderRegex&gt;false&lt;/matchHeaderRegex&gt;
            &lt;matchValueRegex&gt;false&lt;/matchValueRegex&gt;
            &lt;matchRequest&gt;true&lt;/matchRequest&gt;
            &lt;matchResponse&gt;false&lt;/matchResponse&gt;
            &lt;newValue&gt;}catch($1){utag.DB($1);&lt;/newValue&gt;
            &lt;newHeaderRegex&gt;false&lt;/newHeaderRegex&gt;
            &lt;newValueRegex&gt;false&lt;/newValueRegex&gt;
            &lt;matchWholeValue&gt;false&lt;/matchWholeValue&gt;
            &lt;caseSensitive&gt;false&lt;/caseSensitive&gt;
            &lt;replaceType&gt;1&lt;/replaceType&gt;
          &lt;/rewriteRule&gt;
        &lt;/rules&gt;
      &lt;/rewriteSet&gt;
    &lt;/rewriteSet-array&gt;
    ```
    
1. Open **Charles Rewrite Settings** (**Tools &gt; Rewrite**).
1. Click **Import** (see image below).
1. Select the file and click **Open**.
1. Click **Apply** and **OK** to complete the import.
    ![](/images/iq-tag-management/charles-utag-db-upgrade.png)

1. Refresh the browser window loading your site with Tealium. You should now be able to see the warnings output in the console as shown in the [sample below]().

## Create rewrite rules manually

1. Open Charles Proxy.
1. From the menu, navigate to **Tools &gt; Rewrite**.
1. In the dialog, click the **Add** button on the left-hand side to add a new set. Title it `uTag DB Upgrade`.
1. Under the **Location** section, click the **Add** button to add a location.
1. Copy and paste the below code into the **Path** text field:
    ```
    /*/utag.js
    ```
1. Leave the rest of the fields blank and click **OK**.
1. Under the **Type/Action** section, click the **Add** button to add the first rewrite rule.
    1. In the **Type** dropdown, select **Body**.
    1. In the **Where** section, ensure **Response** is checked.
    1. In the **Match** and **Replace** sections, copy and paste the below code into the corresponding text fields.  
      For the **Match** section, place in the **Value** field
        ```
        ;utag.o[&#39;
        ```
        For the **Replace** section, place in the **Value** field:
        ```js
        ; utag.ut.typeOf = function(e) {return ({}).toString.call(e).match(/\s([a-zA-Z]&#43;)/)[1].toLowerCase();}; utag.DB = function(a, b) {   var t;   if (utag.cfg.utagdb === false) {     return;   } else if (typeof utag.cfg.utagdb == &#34;undefined&#34;) {     utag.db_log = [];     b = document.cookie &#43; &#39;&#39;;     utag.cfg.utagdb = ((b.indexOf(&#39;utagdb=true&#39;) &gt;= 0) ? true : false);   }   if (utag.cfg.utagdb === true) {     var con = window.console;     if (utag.ut.typeOf(a) === &#34;error&#34;) {       utag.db_log.push(a);       t = &#34;&#34;;       if (a.stack &amp;&amp; a.stack.split) {         t = a.stack.split(&#34;\n&#34;)[1].replace(/^[\s\uFEFF\xA0]&#43;|[\s\uFEFF\xA0]&#43;$/g, &#39;&#39;).replace(/^at\s/, &#34;&#34;);       }       if (con) {         t = &#34;utag - Error : &#34; &#43; t &#43; &#34; &#34;&#43; a.message;         if (con.warn) {           con.warn(t);         } else if (con.log){           con.log(t);         }       }     } else {       t = (utag.ut.typeOf(a) == &#34;object&#34;) ? utag.handler.C(a) : a;       utag.db_log.push(t);       if (con &amp;&amp; con.log) con.log(&#34;utag - &#34;, t);     }   } };utag.o[&#39;
        ```
    1. In the **Replace** section, ensure the **Replace first** option is selected.
    1. Your **Rewrite Rule** should look something like this:  
        ![](/images/iq-tag-management/screen-shot-2020-11-09-at-9.22.49-am.png)
    1. Click the **OK** button to save the rule.

1. Under the **Type/Action** section, click the **Add** button to add the second rewrite rule.  
    1. In the **Type** dropdown, select **Body**.
    1. In the **Where** section, ensure **Request** is checked.
    1. In the **Match** and **Replace** sections, copy and paste the below code into the corresponding text fields.  
        For the **Match** section, place in the **Value** field
        ```
        \}catch\((.*?)\)\{
        ```
        For the **Replace** section, place in the **Value** field
        ```
        }catch($1){utag.DB($1);
        ```
    1. In the **Match** section, ensure the **Regex** box is checked.
    1. In the **Replace** section, ensure the **Replace first** option is selected.
    1. Click the **OK** button to save the rule.
    1. Your **Rewrite Rule** should look something like this:  
        ![](/images/iq-tag-management/screen-shot-2020-11-09-at-9.03.19-am.png)

1. The `uTag DB Upgrade` set with the two included rewrites should look like this when complete:
    ![](/images/iq-tag-management/charlesproxy-utagdbrewrite-full.jpg)

1. Click **Apply** to apply the rewrite and then click **OK** to close the dialog.
1. Refresh the browser window loading your site with Tealium. You should now be able to see the Warnings output in the console as shown in the sample below.

## Output sample

Below is a sample of the enhanced output as shown in Google Chrome DevTools. You can see that instead of just showing as **Info** output, the error is showing as an expandable warning, which can be filtered by selecting the **Warnings** option in the dropdown next to the **Filter** input box.

![](/images/iq-tag-management/screen-shot-2020-11-09-at-9.07.27-am.png)
