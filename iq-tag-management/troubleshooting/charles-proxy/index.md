---
title: Enhanced browser console debugging with Charles Proxy
description: This article demonstrates how to use Charles Proxy to obtain more advanced output from utag.DB.
url: https://docs.tealium.com/iq-tag-management/troubleshooting/charles-proxy/
---
By adding a rewrite setting to Charles Proxy, the regular errors from `utag.DB` will be displayed as browser level console warnings. This allows for the **Warnings** filter in the console to be used when filtering errors, warnings, and info output.

## Prerequisites

* [Charles Proxy Web Debugging Application](https://www.charlesproxy.com/download/) installed on your computer.
* [utag.DB output](https://docs.tealium.com/platforms/javascript/debugging/) is enabled in the browser.

## Create rewrite rules from XML file

1. Save the following XML as a file on your computer.  
    
    ```xml
    <?xml version='1.0' encoding='UTF-8' ?>
    <?charles serialisation-version='2.0' ?>
    <rewriteSet-array>
      <rewriteSet>
        <active>true</active>
        <name>uTag DB Upgrade</name>
        <hosts>
          <locationPatterns>
            <locationMatch>
              <location>
                <path>/*/utag.js</path>
              </location>
              <enabled>true</enabled>
            </locationMatch>
          </locationPatterns>
        </hosts>
        <rules>
          <rewriteRule>
            <active>true</active>
            <ruleType>7</ruleType>
            <matchValue>;utag.o[&apos;</matchValue>
            <matchHeaderRegex>false</matchHeaderRegex>
            <matchValueRegex>false</matchValueRegex>
            <matchRequest>false</matchRequest>
            <matchResponse>true</matchResponse>
            <newValue>; utag.ut.typeOf = function(e) {return ({}).toString.call(e).match(https://docs.tealium.com/\s([a-zA-Z]+)/)[1].toLowerCase();}; utag.DB = function(a, b) {   var t;   if (utag.cfg.utagdb === false) {     return;   } else if (typeof utag.cfg.utagdb == &quot;undefined&quot;) {     utag.db_log = [];     b = document.cookie + &apos;&apos;;     utag.cfg.utagdb = ((b.indexOf(&apos;utagdb=true&apos;) &gt;= 0) ? true : false);   }   if (utag.cfg.utagdb === true) {     var con = window.console;     if (utag.ut.typeOf(a) === &quot;error&quot;) {       utag.db_log.push(a);       t = &quot;&quot;;       if (a.stack &amp;&amp; a.stack.split) {         t = a.stack.split(&quot;\n&quot;)[1].replace(https://docs.tealium.com/^[\s\uFEFF\xA0]+|[\s\uFEFF\xA0]+$/g, &apos;&apos;).replace(https://docs.tealium.com/^at\s/, &quot;&quot;);       }       if (con) {         t = &quot;utag - Error : &quot; + t + &quot; &quot;+ a.message;         if (con.warn) {           con.warn(t);         } else if (con.log){           con.log(t);         }       }     } else {       t = (utag.ut.typeOf(a) == &quot;object&quot;) ? utag.handler.C(a) : a;       utag.db_log.push(t);       if (con &amp;&amp; con.log) con.log(&quot;utag - &quot;, t);     }   } };utag.o[&apos;  </newValue>
            <newHeaderRegex>false</newHeaderRegex>
            <newValueRegex>false</newValueRegex>
            <matchWholeValue>false</matchWholeValue>
            <caseSensitive>false</caseSensitive>
            <replaceType>1</replaceType>
          </rewriteRule>
          <rewriteRule>
            <active>true</active>
            <ruleType>7</ruleType>
            <matchValue>\}catch\((.*?)\)\{</matchValue>
            <matchHeaderRegex>false</matchHeaderRegex>
            <matchValueRegex>false</matchValueRegex>
            <matchRequest>true</matchRequest>
            <matchResponse>false</matchResponse>
            <newValue>}catch($1){utag.DB($1);</newValue>
            <newHeaderRegex>false</newHeaderRegex>
            <newValueRegex>false</newValueRegex>
            <matchWholeValue>false</matchWholeValue>
            <caseSensitive>false</caseSensitive>
            <replaceType>1</replaceType>
          </rewriteRule>
        </rules>
      </rewriteSet>
    </rewriteSet-array>
    ```
    
1. Open **Charles Rewrite Settings** (**Tools > Rewrite**).
1. Click **Import** (see image below).
1. Select the file and click **Open**.
1. Click **Apply** and **OK** to complete the import.
    ![](https://docs.tealium.com/images/iq-tag-management/charles-utag-db-upgrade.png)

1. Refresh the browser window loading your site with Tealium. You should now be able to see the warnings output in the console as shown in the [sample below](https://docs.tealium.com/enhanced-browser-console-debugging-with-charles-proxy/).

## Create rewrite rules manually

1. Open Charles Proxy.
1. From the menu, navigate to **Tools > Rewrite**.
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
        ;utag.o['
        ```
        For the **Replace** section, place in the **Value** field:
        ```js
        ; utag.ut.typeOf = function(e) {return ({}).toString.call(e).match(https://docs.tealium.com/\s([a-zA-Z]+)/)[1].toLowerCase();}; utag.DB = function(a, b) {   var t;   if (utag.cfg.utagdb === false) {     return;   } else if (typeof utag.cfg.utagdb == "undefined") {     utag.db_log = [];     b = document.cookie + '';     utag.cfg.utagdb = ((b.indexOf('utagdb=true') >= 0) ? true : false);   }   if (utag.cfg.utagdb === true) {     var con = window.console;     if (utag.ut.typeOf(a) === "error") {       utag.db_log.push(a);       t = "";       if (a.stack && a.stack.split) {         t = a.stack.split("\n")[1].replace(https://docs.tealium.com/^[\s\uFEFF\xA0]+|[\s\uFEFF\xA0]+$/g, '').replace(https://docs.tealium.com/^at\s/, "");       }       if (con) {         t = "utag - Error : " + t + " "+ a.message;         if (con.warn) {           con.warn(t);         } else if (con.log){           con.log(t);         }       }     } else {       t = (utag.ut.typeOf(a) == "object") ? utag.handler.C(a) : a;       utag.db_log.push(t);       if (con && con.log) con.log("utag - ", t);     }   } };utag.o['
        ```
    1. In the **Replace** section, ensure the **Replace first** option is selected.
    1. Your **Rewrite Rule** should look something like this:  
        ![](https://docs.tealium.com/images/iq-tag-management/screen-shot-2020-11-09-at-9.22.49-am.png)
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
        ![](https://docs.tealium.com/images/iq-tag-management/screen-shot-2020-11-09-at-9.03.19-am.png)

1. The `uTag DB Upgrade` set with the two included rewrites should look like this when complete:
    ![](https://docs.tealium.com/images/iq-tag-management/charlesproxy-utagdbrewrite-full.jpg)

1. Click **Apply** to apply the rewrite and then click **OK** to close the dialog.
1. Refresh the browser window loading your site with Tealium. You should now be able to see the Warnings output in the console as shown in the sample below.

## Output sample

Below is a sample of the enhanced output as shown in Google Chrome DevTools. You can see that instead of just showing as **Info** output, the error is showing as an expandable warning, which can be filtered by selecting the **Warnings** option in the dropdown next to the **Filter** input box.

![](https://docs.tealium.com/images/iq-tag-management/screen-shot-2020-11-09-at-9.07.27-am.png)
