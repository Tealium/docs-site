---
title: Set up the data layer converter
url: https://docs.tealium.com/iq-tag-management/data-layer/data-layer-converter/set-up-data-layer-converter/
---
The data layer converter is added to your account by pasting JavaScript code into an extension and then adjusting parts of the code to accommodate your specific data layer conversion.

The added functionality is used in one of the following methods (or both):

* **Convert Page Data Object**  
Convert the source data object to the Universal Data Object (`utag_data`) on every page load.
* **Convert Tracking Calls**  
Convert the source data object on every call to `utag.view()` and `utag.link()` .

## Copy the code


```js
//Define the teal global namespace
window.teal = window.teal || {};
teal.ignore_keys = {};
teal.replace_keys = {};
teal.prefix = &#34;&#34;;

//In cases of a nested object, what should join the parent key and child key
teal.nested_delimiter = &#34;.&#34;;

//Ignore keys in the data layer that start with the following text.
//Expecting an object of strings
/*
teal.ignore_keys = {
  &#34;user&#34; : 1,
  &#34;util&#34; : 1
};
*/

//Specify a prefix for data layer elements being sent to the utag_data object.
//Instead of utag_data.productID, it could be utag_data.dl_productID
// teal.prefix = &#34;dl_&#34;;

//Keys to be removed from the new flattened key name
//For a flattened key, you have digitalData.page.pageInfo.pageName and you want digitalData.page.pi.pageName
/* teal.replace_keys = {
    &#34;pageInfo&#34;:&#34;pi&#34;
  };
*/

//For a flattened key, you have digitalData.page.pageInfo.pageName and you want digitalData.page.pageName
/* teal.replace_keys = {
    &#34;pageInfo&#34;:&#34;&#34;
  };
*/

//For a flattened key, you have digitalData.page.pageInfo.pageName and you want digitalData.pageName
/* teal.replace_keys = {
    &#34;page&#34;:&#34;&#34;,
    &#34;pageInfo&#34;:&#34;&#34;
  };
*/

/*****************DO NOT MODIFY BELOW***********************/

teal.flattener_version = 1.4;

// From https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/keys
// Add the Object.keys method for older versions of IE
Object.keys||(Object.keys=function(){&#34;use strict&#34;;var a=Object.prototype.hasOwnProperty,b=!{toString:null}.propertyIsEnumerable(&#34;toString&#34;),c=[&#34;toString&#34;,&#34;toLocaleString&#34;,&#34;valueOf&#34;,&#34;hasOwnProperty&#34;,&#34;isPrototypeOf&#34;,&#34;propertyIsEnumerable&#34;,&#34;constructor&#34;],d=c.length;return function(e){if(&#34;object&#34;!=typeof e&amp;&amp;(&#34;function&#34;!=typeof e||null===e))throw new TypeError(&#34;Object.keys called on non-object&#34;);var g,h,f=[];for(g in e)a.call(e,g)&amp;&amp;f.push(g);if(b)for(h=0;h&lt;d;h&#43;&#43;)a.call(e,c[h])&amp;&amp;f.push(c[h]);return f}}());

teal.ignoreKey = function(key,re){
  var should_ignore_key = 0;
  //Build a new array to avoid running through Object.keys multiple times
  if(typeof teal.ignore_keys_list === &#39;undefined&#39;){
    teal.ignore_keys_list = Object.keys(teal.ignore_keys);
    teal.ignore_keys_list.forEach(function(name){
      //Store a copy of the regex in the object
      teal.ignore_keys[name] = new RegExp(&#34;^&#34;&#43;name);
      if(key.match(teal.ignore_keys[name])){
        should_ignore_key = 1;
      }
    });
  }else{
    //Loop through the ignore_keys object to see if we should ignore this key
    teal.ignore_keys_list.forEach(function(name){
      if(key.match(teal.ignore_keys[name])){
        should_ignore_key = 1;
      }
    });
  }
  return should_ignore_key;
}

teal.getKeyName = function(key,re){
  //Create a new object to store regexs or use existing one
  teal.replace_keys_regex = teal.replace_keys_regex || {};
  //Build a new array to avoid running through Object.keys multiple times
  if(typeof teal.replace_keys_list === &#39;undefined&#39;){
    teal.replace_keys_list = Object.keys(teal.replace_keys);
    //Make a start of string and end of string regex
    teal.replace_keys_regex.startOfString = new RegExp(&#34;^[&#34; &#43; teal.nested_delimiter &#43; &#34;]&#34;);
    teal.replace_keys_regex.endOfString = new RegExp(&#34;[&#34; &#43; teal.nested_delimiter &#43; &#34;]$&#34;);
    teal.replace_keys_list.forEach(function(name){
      //Store a copy of the regex in the teal.replace_keys_regex object so that the regexs are only built once
      teal.replace_keys_regex[name] = new RegExp(&#34;[&#34; &#43; teal.nested_delimiter &#43; &#34;]?&#34; &#43; name &#43; &#34;[&#34; &#43; teal.nested_delimiter &#43; &#34;]?&#34;, &#34;g&#34;);
      key = teal.keyReplace(key,name,teal.replace_keys_regex[name]);
    });
  }else{
    //Loop through the replace_keys object to see what we should be replacing
    teal.replace_keys_list.forEach(function(name){
      key = teal.keyReplace(key,name,teal.replace_keys_regex[name]);
    });
  }
  return key;
}

teal.keyReplace = function(key,name,re){
  //Check to see if we are replacing the key name with a new value or if we are removing the key altogether
  if(teal.replace_keys[name] === &#39;&#39;){
    //The key needs to be removed completely
    key = key.replace(re,teal.nested_delimiter);
    //Check to see if the key starts with the nested delimiter and if so, remove it
    if(key.indexOf(teal.nested_delimiter) === 0){
      var cleanRegEx = new RegExp(&#34;^[&#34; &#43; teal.nested_delimiter &#43; &#34;]&#34;);
      key = key.replace(cleanRegEx,&#39;&#39;);
    }
  }else{
    //Make a copy of the original key to see how we need to update the key name
    var origKey = key;
    //Replace the key name
    key = key.replace(re,teal.nested_delimiter &#43; teal.replace_keys[name] &#43; teal.nested_delimiter);
    //Check for the start of the origKey to see of the nested delimiter is there
    if(!origKey.match(teal.replace_keys_regex.startOfString)){
      //Remove the nested delimiter from the start of the string
      var cleanRegEx = new RegExp(&#34;^[&#34; &#43; teal.nested_delimiter &#43; &#34;]&#34;);
      key = key.replace(cleanRegEx,&#39;&#39;);
    }
    //Check for the end of the origKey to see of the nested delimiter is there
    if(!origKey.match(teal.replace_keys_regex.endOfString)){
      //Add the nested delimiter to the end of the string
      var cleanRegEx = new RegExp(&#34;[&#34; &#43; teal.nested_delimiter &#43; &#34;]$&#34;);
      key = key.replace(cleanRegEx,&#39;&#39;);
    }
  }
  return key;
}

teal.processDataObject = function(obj,new_obj,parent_key,create_array){
  if(typeof parent_key === &#34;undefined&#34;){
    //This object isn&#39;t nested in another object
    parent_key = &#34;&#34;;
  }else{
    //Add the nested_delimiter to the parent key if the delimiter isn&#39;t already at the end
    teal.nested_delimiter_regex = teal.nested_delimiter_regex || new RegExp(&#34;[&#34;&#43;teal.nested_delimiter&#43;&#34;]$&#34;);
    if(!parent_key.match(teal.nested_delimiter_regex)){
      parent_key &#43;= &#34;&#34;&#43;teal.nested_delimiter;
    }
  }
  Object.keys(obj).forEach(function(key){
    var nested_key_name = parent_key&#43;key;
    //Format the new key name and take out any whitespace
    var new_key_name = teal.getKeyName((teal.prefix&#43;parent_key&#43;key).replace(/\s/g, &#39;&#39;));
    //Set the key_type to limit the number of typeof checks
    var key_type = teal.typeOf(obj[key]);
    if(key_type !== &#39;undefined&#39; &amp;&amp; key_type != null){
      if(key_type.match(/boolean|string|number|date/) &amp;&amp; !teal.ignoreKey(key)){
        //If obj[key] is a date, convert to ISOString
        if(teal.typeOf(obj[key]) === &#39;date&#39;){
          obj[key] = obj[key].toISOString();
        }
        //Check to see if we need to create an array for this data point
        if(create_array){
          //First check to see if this key exists
          if(teal.typeOf(new_obj[new_key_name]) !== &#34;array&#34;){
            //Make the key an array
            new_obj[new_key_name] = [];
          }
          new_obj[new_key_name].push(&#34;&#34;&#43;obj[key]); //Force value to be a string
        }else{
          //If the value of the key is a boolean or a string or a number and
          //the key shouldn&#39;t be ignored add to the data layer
          new_obj[new_key_name] = &#34;&#34;&#43;obj[key]; //Force value to be a string
        }
      }else if(key_type === &#39;object&#39; &amp;&amp; !teal.ignoreKey(key)){
        //Process this piece of the data layer and merge it
        teal.processDataObject(obj[key],new_obj,nested_key_name,create_array);
      }else if(key_type === &#39;array&#39;){
        teal.processDataArray(obj[key],new_obj,nested_key_name);
      }
    }
  });
}

teal.processDataArray = function(obj,new_obj,parent_key){
  var objLength = obj.length;
  if(typeof parent_key === &#34;undefined&#34;){
    //This object isn&#39;t nested in another object
    parent_key = &#34;&#34;;
  }else if(objLength &gt; 0 &amp;&amp; teal.typeOf(obj[0]).match(/boolean|string|number|date/)){
    //This is a normal array that doesn&#39;t need a nested delimiter
  }else{
    //Add the nested_delimiter to the parent key
    parent_key &#43;= &#34;&#34;&#43;teal.nested_delimiter;
  }
  //Format the new key name and take out any whitespace
  var new_key_name = teal.getKeyName((teal.prefix&#43;parent_key).replace(/\s/g, &#39;&#39;));
  for(var n = 0; n &lt; objLength; n&#43;&#43;){
    var key_type = teal.typeOf(obj[n]);
    if(key_type.match(/boolean|string|number|date/)){
      //If obj[n] is a date, convert to ISOString
      if(key_type === &#39;date&#39;){
        obj[n] = obj[n].toISOString();
      }
      //First check to see if this key exists
      if(teal.typeOf(new_obj[new_key_name]) !== &#34;array&#34;){
        //Make the key an array
        new_obj[new_key_name] = [];
      }
      //If the value of the key is a boolean or a string or a number and
      //the key shouldn&#39;t be ignored add to the data layer
      new_obj[new_key_name].push(&#34;&#34;&#43;obj[n]);
    }else if(key_type === &#39;object&#39;){
      teal.processDataObject(obj[n],new_obj,new_key_name,1);
    }
  }
}

teal.typeOf = function(e){return ({}).toString.call(e).match(/\s([a-zA-Z]&#43;)/)[1].toLowerCase();}

teal.flattenObject = function(obj,new_obj){
  //Make sure object exists
  if(typeof obj === &#39;undefined&#39;){
    return false;
  }
  //Check to see if we want to flatten the same object and keep the reference
  var mergeObject = false;
  if(obj === new_obj){
    mergeObject = true;
    //Start off a clean copy of the object
    new_obj = {};
  }
  //Make sure new object exists
  if(typeof new_obj === &#39;undefined&#39;){
    new_obj = {};
  }
  //Check to see if this object is an array
  if(teal.typeOf(obj) === &#39;array&#39;){
    //Store a safe copy of this object in case we are processing the b object
    var temp_array = JSON.parse(JSON.stringify(obj));
    var temp_array_length = temp_array.length;
    //Clean up the object
    obj = {};
    //Let&#39;s see if the obj and new_obj are the same.  If so, going to assume we are using the b object
    if(obj == new_obj){
      //Let&#39;s ensure that we have the a object
      if(typeof a === &#39;undefined&#39;){
        var a = &#39;view&#39;;
      }
      //Add the automatic utag data points
      utag.loader.RD(new_obj,a);
    }
    for(var i = 0; i &lt; temp_array_length; i&#43;&#43;){
        teal.processDataObject(temp_array[i],new_obj);
    }
  }else{
    teal.processDataObject(obj,new_obj);
  }
  if(mergeObject){
    //Need to delete everything out of obj and replace with new_obj
    Object.keys(obj).forEach(function(key){
      delete obj[key];
    });
    //Now that we have a clean original object, add everything from new_obj which allows the reference to be kept
    Object.keys(new_obj).forEach(function(key){
      obj[key] = new_obj[key];
    });
  }

  return new_obj;
}
```


## Add the extensions

Use the following steps to add the data layer converter code:

1. In the left sidebar, navigate to **Tag Management &gt; Extensions**.
1. Add a [JavaScript Code extension]().
1. In the **Title** field, enter `Data Layer Converter`.
1. In the **Scope** field, select **Pre Loader**.
1. In the **Draft Name** field, enter a name for your draft.
1. Paste the copied code into the **JavaScript** field for the extension.  
    ![](/images/iq-tag-management/whiteui-data-layer-converter-add-js-extension.jpg)
1. Click **Approve for Publish** and select the targets.

Use the following steps to add the code to trigger the data layer converter:

1. In the left sidebar, navigate to **Tag Management &gt; Extensions**.
1. Add a [JavaScript extension]().
1. In the **Title** field, enter `Convert to utag_data`.
1. In the **Scope** field, select **Pre Loader**.
1. In the **Draft Name** field, enter a name for your draft.
1. Copy and paste the following code into the JavaScript field for the extension:  
    ```js
    utag_data = teal.flattenObject(digitalData);
    ```
Update `digitalData` to the name of your data layer object.
1. Ensure that this extension is listed below the **Data Layer Converter** extension created in the previous step.
1. Click **Approve for Publish** and select the targets.
1. Select one or more publish environments and click **Apply**.  
    ![](/images/iq-tag-management/whiteui-tiq-data-layer-converter-approve-for-publish.jpg)  
1. Save and publish your changes.